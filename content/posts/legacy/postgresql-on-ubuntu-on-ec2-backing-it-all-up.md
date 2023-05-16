---
title: 'PostgreSQL on Ubuntu on EC2: Backing It All Up'
date: 2009-10-10T11:19:00.000-07:00
draft: false
url: /2009/10/postgresql-on-ubuntu-on-ec2-backing-it.html
tags: 
- ubuntu
- ec2
- postgres
---

[![](http://1.bp.blogspot.com/_1luLRXKoJM8/SJPNIpIJamI/AAAAAAAAGnQ/QgxlU54iRrU/s400/dean%2Bback.jpg)](http://1.bp.blogspot.com/_1luLRXKoJM8/SJPNIpIJamI/AAAAAAAAGnQ/QgxlU54iRrU/s400/dean%2Bback.jpg)This post continues what I started with ["PostgreSQL on Ubuntu on EC2: The Installation Guide"](http://deadprogrammersociety.blogspot.com/2009/08/postgresql-on-ubuntu-on-ec2.html). Once you have your PostgreSQL database server instance running, you will need to backup two different things: your database data, and the instance itself. The database data will be backed up using Elastic Block Storage (EBS) snapshots. Once we have the instance running the backups correctly, we will then create an Amazon Machine Image (AMI) that will allow you to launch a new instance to replace the database server in case it goes down.  
  
**Backing Up The Database**  
First, we need to connect to our database server instance via SSH using the ubuntu user.  
  
We will need to install some dependencies to get our backup script to run:  
`  
sudo apt-get install build-essential  
sudo apt-get install ruby1.8-dev  
sudo apt-get install rubygems  
sudo gem update --system  
`  
  
You will need to tweak RubyGems so that the update works correctly, as [described here](http://www.videc.at/2009/04/30/rubygems-undefined-method-manage_gems-for-gemmodule-nomethoderror/).  
  
Now you can install Gemcutter, which is the new ultra cool repository for gems:  
`  
sudo gem install gemcutter  
sudo gem tumble  
`  
  
Finally we are ready to install the Amazon EC2 rubygem:  
`  
sudo gem install amazon-ec2  
`  
  
Now we can create our backup script. Save this code into the ~/ directory under the name backup\_database.rb. You will need to substitute the Amazon ACCESS\_KEY\_ID and SECRET\_ACCESS\_KEY, as well and entering the correct EBS volume for the DATABASE\_VOLUME constant:  
`  
#!/usr/bin/env ruby  
  
require 'rubygems'  
require 'AWS'  
  
ACCESS_KEY_ID = 'YOUR_ACCESS_KEY'  
SECRET_ACCESS_KEY = 'YOUR_SECRET_ACCESS_KEY'  
DATABASE_VOLUME = 'vol-XXXXXXXX'  
  
puts "Starting database snapshot..."  
ec2 = AWS::EC2::Base.new(:access_key_id => ACCESS_KEY_ID, :secret_access_key => SECRET_ACCESS_KEY)  
ec2.create_snapshot(:volume_id => DATABASE_VOLUME)  
puts "Database snapshot completed."  
`  
  
Due to the finicky way that Ruby runs as part of a cron job, we are best off creating a shell script that then runs the Ruby backup script. Save this code into the ~/ directory under the name backup\_db.sh:  
`  
#!/bin/sh  
cd /home/ubuntu  
ruby /home/ubuntu/backup_database.rb  
`  
  
Don't forget to make the backup shell script executable:  
`  
chmod +x /home/ubuntu/backup_db.sh  
`  
  
Now we just need to configure this script to run as part of a cron job, so that the backups take place automatically. The crontab command brings up the list of configured cron tasks for the current user:  
`  
crontab -e  
`  
  
This example crontab entry runs the backup daily at midnight, but you may want it to run more frequently:  
`  
0 0 * * * /home/ubuntu/backup_db.sh  
`  
  
At this point, you should have a fully functional automated backup system. Verify after midnight that the script has run as you expect, by looking to see if a new snapshot has been created, using Elastifox or however you administrate your EC2 instances.  
  
**Creating The AMI**  
Creating the AMI to backup the entire database instance is pretty easy. First, you need to upload the PEM files. Remember you are authenticating as the "ubuntu" user:  
`  
scp -i id_rsa-gsg-keypair pk-YOUR.pem cert-YOUR.pem ubuntu@domU-12-34-31-00-00-05.usma1.compute.amazonaws.com:  
`  
  
Use your SSH connection into the database server instance to copy the PEM files to the /mnt directory:  
`  
sudo cp /home/ubuntu/*.pem /mnt  
`  
  
Now create the bundle. Make sure you use your Amazon account number (without dashes) as the value for the -u parameter. This can take quite a while, so do not get impatient:  
`  
sudo ec2-bundle-vol -d /mnt -k /mnt/pk-YOUR.pem -c /mnt/cert-YOUR.pem -r i386 -u YOURUSERACCOUNTNUMBER  
`  
  
You can now upload the bundle to your Amazon S3 account, in preparation for making available as an AMI. Use something versioned for the -b parameter which is the name of the bundle:  
`  
sudo ec2-upload-bundle -b my-database-server-1.0-ami -m /mnt/image.manifest.xml -a YOUR_ACCESS_KEY -s YOUR_SECRET_ACCESS_KEY  
`  
  
Final step is going back to your local machine, and making the newly created bundle available to be used to start a new instance:  
`  
ec2-register my-database-server-1.0-ami/image.manifest.xml  
`  
  
You can now now launch a brand new database server instance based on this AMI, and it will be a clone of your existing database server. This is the procedure you would follow if you need to restore your database server instance from backups.  
  
**Restoring Your Database Server From The Backups**  
In the case that something goes terribly terribly wrong, you can get back to normal as follows:  
\- startup a new EBS volume from your most recent snapshot backup,  
\- start up a new server from your database AMI  
\- configure your new server instance to use the new volume started from the backup data  
\- switch your elastic IP to point to the new server, or update the references in your application to point to the new server  
  
This concludes part 2 of the great PostgreSQL config post for the EC2 cloud. Hopefully it will help you with a nice simple way to take the basic PostgreSQL instance that you got up and running on Ubuntu/EC2 using the directions in the [part 1 post](http://deadprogrammersociety.blogspot.com/2009/08/postgresql-on-ubuntu-on-ec2.html), and add the confidence that backed up data and a completely reproducible configuration provides.