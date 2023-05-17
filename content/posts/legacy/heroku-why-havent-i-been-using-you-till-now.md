---
title: 'Heroku, Why Haven''t I Been Using You Till Now?'
date: 2009-04-14T11:23:00.000-07:00
draft: false
url: /2009/04/heroku-why-havent-i-been-using-you-till.html
tags: 
- sinatra
- heroku
- ruby
- cloud computing
- ruby on rails
---

[![](http://www.dinaview.com/wp-content/uploads/2008/06/hero.jpg)](http://www.dinaview.com/wp-content/uploads/2008/06/hero.jpg)

Last night, I finally got around to deploying something on [Heroku](http://heroku.com/), an interesting service founded by my formerly LA-based Ruby programming chums [Adam Wiggins](http://adam.blog.heroku.com/), James Lindenbaum, and Orion Henry. I had played with their previous incarnation of the service, now known as "Heroku Garden" but only recently have I gotten to know a little bit more about the incredible offering they have evolved into.  
  
Basically, the Heroku crew have addressed the question "how can I deploy my [Ruby on Rails](http://rubyonrails.org/), [Sinatra](http://www.sinatrarb.com/), or other [Rack](http://rack.rubyforge.org/)\-based web application into a dynamic cloud of servers with ridiculous ease?" They have done this with an ingenious architecture that takes advantage of [Amazon's EC2](http://aws.amazon.com/ec2/) to provide their internal infrastructure. This allows Heroku to concentrate on their most important core value proposition, of a simple way to take your Ruby code and just push it into the cloud.  
  
Notice I said "push". Heroku requires that you use [git](http://git-scm.com/) for source control of your application. You are using git for everything now, right? If not, git with it! Sorry, could not resist that. Anyhow, by simply adding a remote master to your existing git repo that points to Heroku, along with a few Ruby gems that they provide, you can deploy your app just by pushing your current branch to the Heroku master.  
  
Doing this, causes your app to get packaged up into "slug". Once you have an active slug, it will be be deployed to a "dyno" within the Heruku grid, which is what a virtual node within their architecture is called. As your app requires more resources, the slug can be deployed to more dynos within "less than 2 seconds for most apps". That is way faster than starting up a new Amazon EC2 instance yourself, and having this extra layer has a number of other interesting benefits as well.  
  
Heroku has a quick start guide, which pretty much runs down what you need to do. I had found a slightly more [simplified quickstart here](http://heroku.com/pages/quickstart). I already had an existing Sinatra-based app that I wanted to test on Heroku, so here were my steps:  
  
1\. Install heroku gem  
```
sudo gem install heroku
```  
2\. Setup Heroku account info, and upload public key  
```
heroku keys:add 
```  
This will prompt you for your Heroku account info. If you have not created one yet, better jump over to [http://heroku.com/signup](http://heroku.com/signup) and create one  
  
3\. Create Heroku app from my existing app  
I just changed so my current directory was the app I wanted to add to Heroku, then entered:  
```
heroku create myappname
```  
This creates the new app on Heroku, and creates a remote branch so you can deploy just by pushing the code.  
  
4\. Deploy my code  
```
git push heroku master
```  
That's it! If you have a really simple app, with no database access, you are done. What, you are deploying a Ruby on Rails app and need a database setup? OK, then...  
  
5\. Run database migrations  
```
heroku rake db:migrate
```  
  
NOW, you are fully deployed and running on Heroku. Unless you are not. I still had a minor problem with my app. I was writing my log file into "logs/production.log" but Heroku does not normally allow write access to disk. The two exceptions to this are the "tmp" directory and "log" directory (notice singular). They do provide an easy way to view your most recent log entries, by typing```
heroku logs
```which is how I figured out my problem with the log directory.  
  
So, here is my total time required to deploy this app on Heroku:  
\- Reading quickstart = 3 minutes  
\- Installing gem and entering account info = 2 minutes  
\- Making my app a Heroku app = 1 minute  
\- Deploying my app for the first time to Heroku = 2 minutes  
\- Figuring out what I had done wrong from the Heroku documentation = 10 minutes  
TOTAL = 18 minutes  
  
Here were my bonus steps:  
\- Reading Heroku docs on using a custom domain with Heroku = 1 minute  
\- Realize I need to rename my app using Heroku command line = 1 minute  
\- Rename my app using Heroku command line = 1 minute  
\- Setting my DNS settings to point to Heroku = 5 minutes  
\- Telling Heroku about my custom domain = 1 minute  
TOTAL = 9 minutes  
  
So there you have it... a fully deployed app, living in the Heroku grid and consequently the Amazon EC2 cloud, in less than 30 minutes, having never used their tools before, including troubleshooting a minor configuration problem. That may seem unfair... and it is. That is exactly the kind of unfair I like on my side!  
  
Much credit should go to the Heroku team for creating something extremely cool and functional. Important details are still not available, like pricing etc., but at least for now Heroku, is a great way to easily get your app up into the cloud within literally minutes.  
  
What is the future for Heroku? Funded by [Y Combinator](http://ycombinator.com/), they have been quietly working away, and now with Sinatra team leads [Blake Mizerany](http://twitter.com/bmizerany) and [Ryan Tomayko](http://tomayko.com/) onboard as well, I think we will be hearing a lot from this exciting little company.