---
title: 'Version Control For Lean Startups Using Git'
date: 2010-01-26T20:49:00.000-08:00
draft: true
url: 
tags: 
- lean software
- lean startup
- version control
- git
---

Lean software development is all the rage among the startup scene, and git is the version control system with the power. So how can a lean startup take best advantage of git to provide speed, flexibility, and security? Here are some of the practices that seem to make sense to allow the greatest simplicity, while still giving some flexibility.  
  
Use a git provider  
Use one of the git providers. Github private repos, Unfuddle, and other services I do not know as much about provide a place to keep the remote repo that your team will be using to integrate their work. Choose a provider with a solid backup plan, and decent management tools to streamline the process of giving or revoking access to team members.  
  
Continuous Integration  
There are several continuous integration tools that can access git repositories. Integrity is a preferred tool, but CruiseControl.rb, Hudson, and many others can pull code from your remote  
  
Continuous Deployment  
Eric Reis has written compellingly on the benefits of Continuous Deployment. Using git along with hosting providers such as Heroku or Engine Yard allow you to deploy right from your git repo using git itself.