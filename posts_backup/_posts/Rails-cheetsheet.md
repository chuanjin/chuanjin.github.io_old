title: "Rails cheetsheet"
date: 2015-02-10 20:57:35
tags: Rails
categories: R&D
---

**Ruby on Rails cheetsheet for my personal use**

    rails generate scaffold User name:string email:string
    rails generate scaffold Micropost content:text user_id:integer
	
	rails generate controller StaticPages home help
	rails destroy  controller StaticPages home help

	rails generate model User name:string email:string
	rails destroy model User

	(Note: Controller names are always plural, while Model names are singular.)

    (bundle exec) rake db:migrate
    (bundle exec) rake db:rollback
    (bundle exec) rake db:migrate VERSION=0
    (bundle exec) rake db:reset  (rake db:drop + rake db:create + rake db:migrate)

	(bundle exec) rake test
	(bundle exec) rake test:integration
	(bundle exec) rake test:models

	bundle install --without production



![](/images/crud.PNG)
image from [Codecademy](http://www.codecademy.com/en/learn/make-a-rails-app)

Reference:
http://www.pragtob.info/rails-beginner-cheatsheet/	
http://www.cheat-sheets.org/saved-copy/RubyOnRails-Cheatsheet-BlaineKendall.pdf
http://www.idiotinside.com/2014/09/29/60-cheatsheet-collection-for-full-stack-developers/