---
layout: post
title: Rails Tutorial Book Chapter 1 Notes
category: rails-notes
---

Chapter 1 is one of the chapters I come back to most often. I usually don't remember how to do specific "set-up" type tasks, which this chapter addresses.

#### About Development Environments
The book discusses a topic called "development environments" - essentially just the way a computer needs to be set up to start making an app in rails. The book plugs their affiliate "web IDE" called Cloud9, warning readers against setting up their own environment locally. I personally used Cloud9 for about a year before switching to my own local environment to have greater control over my text editing and console configurations, but Cloud9 is a perfectly viable option for most people.

#### Command Line
The book then shifts into a quick mini-lesson about the command line. This is also something important to pick up on, and something which I use every day. This stuff will come up time and time again, so it's best to get used to it as early as possible.

#### Initializing a New App
The book goes into detail about what is happening when creating a new app, and how to do it, but I mainly come back to this section when I forget how to do it. Commands are executed in the command line to create an app, along with editing some files to get your "hello world". To boil it down, the steps are:

1. ***Create app from command line**
```bash
$ cd ~/environment # get to the right directory
$ rails _5.1.6_ new hello_app # where _5.1.6_ = version, hello_app = name
```

2. Create an action in the controller(`app/controllers/application_controller`)
```ruby
class ApplicationController < ActionController::Base
  protect_from_forgery with: :exception

  def hello
    render html: "hello, world!"
  end
end
```

3. Change the routing(`config/routes.rb`)
```ruby
Rails.application.routes.draw do
  root 'application#hello'
end
```

#### Git

###### Note on Github/Bitbucket
This book uses bitbucket as a hosting service for git repositories, which is functionally parallel to Github, which you are more likely to have heard of before. Their justification is that Bitbucket offers unlimited private repositories, and Github does not; however, Github has updated their site to allow infinite private repositories as well. Because of this, I would recommend using Github as it is a larger platform for developers.

###### Git

The [git tutorial in this section](https://www.railstutorial.org/book/beginning#sec-version_control) is actually extremely useful as an introduction to git, so its certainly worth a read. This book also assumes command line git(which I prefer), as opposed to the desktop app However, I'll boil it down to the steps I come back to:

1. Set up config(**only need to do once**)
```bash
$ git config --global user.name "Your Name"
$ git config --global user.email your.email@example.com
```

2. Initialize repository
```bash
# Make sure your current working directory is the location of your app.
# Otherwise, use $ cd ~/path/to/your/app/
$ git init
$ git add -A
$ git commit -m "initialize repository"
```

3. Create new repository on github
- click the plus button on top right

4. Copy the URL(should end in .git)

5. Tell git to push to your repository
```bash
$ git remote add origin YOUR_URL
$ git push -u origin master
```

#### Heroku
Heroku is a great way to put whatever app you are building onto the actual internet. If this is your first time doing this, I would recommend walking through the steps outlined in the book [here](https://www.railstutorial.org/book/beginning#sec-deploying). Otherwise, the steps I will put here are for creating another app after already having created one.

1. Modify Gemfile
- add the following to Gemfile
```ruby
group :production do
  gem 'pg', '0.20.0'
end
```

- remove `gem 'sqlite3'` from the top of the file, put into the test/development group
```ruby
group :development, :test do
  gem 'sqlite3'
end
```
2. Save and commit changes
```bash
$ bundle install --without production
$ git commit -am "update gemfile"
```

3. Initialize heroku app
- ensure that your current directory is the same as your rails app
```bash
$ heroku create
```

4. Deploy the application
```bash
$ git push -u heroku master 
```
*note*: try running `$ heroku buildpacks:set https://github.com/bundler/heroku-buildpack-bundler2` if this step fails

#### Lockup
This isn't in the book, but I believe this is important if you are building an app for a customer. The [Lockup Gem](https://github.com/gblakeman/lockup) is a gem you can add to your rails app which secures your app behind a passcode, but only requires each user to do so once per machine. This ensures that no one should have access to your app unless they are supposed to, even when hosted online.

Follow the steps [here](https://github.com/gblakeman/lockup#installation).
Make sure that your place `gem 'lockup'` within the production group, like so:
```ruby
group :production do
  gem 'lockup'
end
```
Also, I have found more success placing `ENV["LOCKUP_CODEWORD"] = 'secret'` within `config/environments/production.rb` than any other option. 

You may also need to run `$ bundle install --with production`
