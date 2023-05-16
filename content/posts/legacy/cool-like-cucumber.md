---
title: 'Cool Like Cucumber'
date: 2008-10-25T16:15:00.000-07:00
draft: false
url: /2008/10/cool-like-cucumber.html
tags: 
- cucumber
- rspec
- bdd
- ruby
- ruby on rails
---

Ever since I discovered [Fitnesse](http://fitnesse.org/) a few years back, I have been increasingly obsessed with the idea of executable specifications and testable requirements. As far as I am concerned, [Behavior Driven Development](http://en.wikipedia.org/wiki/Behavior_driven_development) (BDD) is a very appealing way to get the "people who need the software" and the "people who build the software" to understand each other.  
  
For about 2 years, give or take, many [Ruby on Rails](http://www.rubyonrails.org/) developers have been switching to [RSpec](http://rspec.info/), or at least paying lip-service (giving rspec?). This is simply because, as far as automated testing, ye olde test::unit is getting a bit long in the tooth. The somewhat less ambitious [shoulda](http://www.thoughtbot.com/projects/shoulda) project takes a much more minimal approach to RSpec, preferring to be a better test:unit and not going all the way to the executable specification. Maybe they did not drink the whole glass of kool-aid? Well, I did... a while back. But I digress.  
  
There have been various attempts to introduce a more readable, less "code-oriented" way to work with the users themselves to define the requirements for their solution. This led to RBehave, later merged into the RSpec story runner. Now, there is an even better tool emerging for human-readable yet testable requirements, called [Cucumber](http://github.com/aslakhellesoy/cucumber/tree/master).  
  
Cucumber is the brainchild of RSpec contributor and super smart fellow [Aslak Hellesoy](http://blog.aslakhellesoy.com/). Taking the basic idea of the StoryRunner and, ahem, "running with it", Aslak has not only rewritten the entire thing using the treetop parsing engine, but he has also improved on the paradigm both for expressing the user needs, as well as the coding required to turn the requirements into executable tests.  
  
Here is a small example:  
```
Feature: Log-in  
  In order to view my profile  
  As a Registered member  
  I want to be required to log-in  
  
  Scenario: Proper login  
    Given I am the registered member "quire"  
    And I am on the login page  
    When I fill in "email" with "quire@example.com"  
    And I fill in "password" with "quire69"  
    And I press "Login"  
    Then I should see "Account Activity"  
  
  Scenario: Bad password  
    Given I am the registered member "quire"  
    And I am on the login page  
    When I fill in "email" with "quire@example.com"  
    And I fill in "password" with "bad password"  
    And I press "Login"  
    Then I should see "Simply enter the credentials you signed up with."  
    And I should see "Couldn't log you in as 'quire@example.com'"  
    
  Scenario: Bad email  
    Given I am the registered member "quire"  
    And I am on the login page  
    When I fill in "email" with "quire@example.co"  
    And I fill in "password" with "password"  
    And I press "Login"  
    Then I should see "Simply enter the credentials you signed up with."  
    And I should see "Couldn't log you in as 'quire@example.co'" 
```  
  
Now THAT is a nice clear way to define what a system is supposed to do. Furthermore, actually implementing the "steps" that exercise the system functionality is very simple as well:  
```
Given /I am the registered member "quire"/ do  
  @user \= User.new({  :login \=> 'quire', :email \=> 'quire@example.com', :password \=> 'quire69', :password\_confirmation \=> 'quire69', :terms\_of\_service \=> true, :primary\_talent\_id \=> 1 })  
  @user.save!  
end  
  
Given 'I am on the login page' do  
  visits "/login"  
end  
  
Then 'I should be taken to my dashboard page' do  
  response.request.path.should \== user\_path(@user)  
end  

```  
  
Since [WebRat](http://github.com/brynary/webrat/tree/master) is fully integrated into Cucumber, and there are already a group of useful steps included, you can get surprisingly far while defining fairly few steps of your own. And when you do have to, working with Cucumber really is quite superior to the old StoryRunner.  
  
I am working on two projects right now that are using BDD and Cucumber, and we are very happy with it. We now have a lot of visibility into how complete a feature is, and it helps everyone understand what a feature does, and how it is supposed to work.  
  
Once again, great work from the RSpec crew. Thanks, guys!