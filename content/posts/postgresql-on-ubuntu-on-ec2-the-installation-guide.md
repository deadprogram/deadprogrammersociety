---
title: 'PostgreSQL on Ubuntu on EC2: The Installation Guide'
date: 2009-08-15T01:27:00.000-07:00
draft: false
url: /2009/08/postgresql-on-ubuntu-on-ec2.html
tags: 
- xfs
- ec2
- postgres
- ebs
---

![](http://www.popgadget.net/images/russian-doll.jpg)For some time, I have had clients hosting a couple different applications on Amazon EC2 using Ubuntu. One of these apps uses PostgreSQL, and has been running without event for quite a while. Yesterday, I got to catch up for lost time, by spending the entire day wrestling with data recovery issues related to a failed apt-get upgrade on an important database server. Luckily, the awesome [Eric Hammond](http://twitter.com/esh) was around on IRC, came to my rescue, and coached my thru my self-inflicted pain.  
  
If you are not interested in PostgreSQL, you probably just stop here. Nothing to see folks, move along. However, if you are looking for the well-lit path to getting PostgreSQL installed on Amazon EC2 will all the trimmings, read on.  
  
I went to find various web pages to use as source material, expecting since the last time I went through this, someone would have written a nice definitive guide to installing PostgreSQL on Ubuntu, running it on a dedicated instance on Amazon EC2, and using Elastic Block Storage (EBS). Naturally, you want to be using the XFS file system too. However, no such luck: just a big collection of pages of instructions on the various parts, without any nice simple path to getting things working together.  
  
Hence, this post tries to provide a set of instructions for getting things working, and avoiding a couple of problems that I have run into while running Postgres in production for the last couple years.  
  
Step 0 - You are signed up for Amazon EC2, no? If not, there are plenty of pages with instructions on how to do so.  
  
Step 1 - Choose your AMI  
There are several AMI's available to you. I currently run Hardy 8.04 LTS x86 architecture in the USA, so I am using ami-5d59be34, but you may have other requirements. The [Ubuntu EC2 starter guide](https://help.ubuntu.com/community/EC2StartersGuide) has good info on your options.  
  
Step 2 - Launch your instance  
I like to use Elasticfox, cause I am super lazy. The command line works well, also.  
  
What size instance? This AMI supports small and medium. PostgreSQL is pretty efficient these days, and especially using a dedicated instance and not running anything but the database server improves raw database performance considerably. You would probably be pretty surprised how well a small instance can perform, but choose medium if you think you will have more significant needs.  
  
One key pattern I use for my EC2 hosted apps, is creating security groups in EC2 to separate my database servers from the public internet. I never use the default security group, but instead create a group for each tier of my application like "database", "web", "transcoder" and then allow specific groups to communicate with each other.  
  
Step 3 - Create the EBS Volume  
You can do this via Elasticfox, or via command line. Either way, make sure you do two key things: make sure you create the EBS volume in the same availabilty zone as your database server instance, and also make sure you create a volume with enough space. Here is how you would use the command line tools to create a 10GB volume in the 'us-east-1a' zone:  
`  
ec2-create-volume -z us-east-1a -s 10  
`  
One the volume is ready, attach it to the database instance. For example, this attaches an EBS volume named 'vol-VVVV1111' to the instance 'i-IIII1111' on device /dev/sdh:  
`  
ec2-attach-volume -d /dev/sdh -i i-IIII1111 vol-VVVV1111  
`  
  
Step 4 - Connect to the database instance  
You need to SSH in to configure you new instance. Remember, you cannot connect as 'root' user in Ubuntu, you need to connect using the 'ubuntu' user. [This page](http://alestic.com/2009/04/ubuntu-ec2-sudo-ssh-rsync) has good details about using sudo and SSH on the official Ubuntu EC2 AMIs.  
  
OK, so now you are connected via SSH to your server. Of course, start with the usual update/upgrade:  
`  
sudo apt-get update && sudo apt-get upgrade -y  
`  
  
Step 5 - Install XFS  
We will need to install the XFS file system. Actually, your could use some other file system, but XFS is quite mature and has good performance. Plus if you are crazy, you can scale up to a massive virtual RAID drive that will cost $4000 per month.  
  
`  
sudo apt-get install -y xfsprogs  
`Step 6 - Format the EBS volume using XFS  
We need to install a file system on the EBS volume before we can do anything with it. Here is an example:  
`  
sudo modprobe xfs  
sudo mkfs.xfs /dev/sdh  
  
echo "/dev/sdh /data xfs noatime 0 0" | sudo tee -a /etc/fstab  
sudo mkdir /data  
sudo mount /data  
`  
Now we have a /data directory that maps to our EBS volume. Anything we write to /data will be persisted, even if the database server instance itself terminates.  
  
Step 7 - Install PostgreSQL  
Now we need to get PostgreSQL installed. [This page](http://hocuspokus.net/2008/05/install-postgresql-on-ubuntu-804) has a very nice simple set of instructions on how to do that correctly for Ubuntu, but here is a synopsis especially for a headless server. First install Postgres:  
`  
sudo apt-get install postgresql postgresql-client postgresql-contrib  
`  
Now reset the password for the postgres account in the PostgreSQL server:  
`  
sudo su postgres -c psql template1  
template1=# ALTER USER postgres WITH PASSWORD 'password';  
template1=# \q  
`  
And then change the password on the user account to match:  
`  
sudo passwd -d postgres  
sudo su postgres -c passwd  
`  
  
Now we need to modify the postgres configuration file postgresql.conf. First, to allow other machines to connect to our instance, and also to have PostgreSQL use our nice shiny /data directory.  
  
`  
sudo nano /etc/postgresql/8.3/main/postgresql.conf  
`  
Change the line containing  
`  
data_directory = '/var/lib/postgresql/8.3/main'  
`  
to  
`  
data_directory = '/data/main'  
`  
Now change  
`  
#listen_addresses = 'localhost'  
`  
to  
`  
listen_addresses = '*'  
`  
and also change  
`  
#password_encryption = on  
`  
to  
`  
password_encryption = on  
`  
Save the file, then open the pg\_hba.conf file so we can control who can access the server:  
`  
# DO NOT DISABLE!  
# If you change this first entry you will need to make sure that the  
# database  
# super user can access the database using some other method.  
# Noninteractive  
# access to all databases is required during automatic maintenance  
# (autovacuum, daily cronjob, replication, and similar tasks).  
#  
# Database administrative login by UNIX sockets  
local all postgres ident sameuser  
# TYPE DATABASE USER CIDR-ADDRESS METHOD  
  
# "local" is for Unix domain socket connections only  
local all all md5  
# IPv4 local connections:  
host all all 127.0.0.1/32 md5  
# IPv6 local connections:  
host all all ::1/128 md5  
  
# Connections for all PCs on the subnet  
#  
# TYPE DATABASE USER IP-ADDRESS IP-MASK METHOD  
host all all 0.0.0.0/0 md5 # wide-open, you may want to make this more specific to your database  
`  
  
Step 8 - Move the database files  
We need to stop the PostgreSQL server, move the database files to our EBS volume, then restart the server.  
`  
sudo /etc/init.d/postgresql-8.3 stop  
sudo mv /var/lib/postgresql/8.3/main /data  
sudo /etc/init.d/postgresql-8.3 start  
`  
You are now running PostgreSQL on Amazon EC2 using EBS for your database, with the XFS file system. Congratulations!  
  
I will write a followup post on how to setup your database server for self-backing up using EBS snapshots, but that is all I have time for right now. Hopefully this pared-down set of instructions has been useful to you. Thanks again to Eric Hammond, and everyone else who's blogs were culled together into this post.