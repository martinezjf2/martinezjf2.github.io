---
layout: post
title:      "Vacation Planner"
date:       2020-04-12 21:12:50 +0000
permalink:  vacation_planner
---


It all started with the corneal gem to create an application. There were several things that were either confusing or that are useful to understand and not forget about them. Here are some things that we wil dicuss about, 



* How to install the corneal gem and its purpose? 
*  Understanding which either models or controllers get the ActiveRecord or the Sinatra Functionality
* How do we get our tables started with adding our columns with data?
*  How does the Helpers class play a huge part within making our application more secure, and of course,



These are simple things that were implied towards the projects, and I will probably forget. So that we can all remember, we will discuss these concepts, and of course use these resources and links provided for examples. 



### *How to install the corneal gem and its purpose?* 

Corneal is a gem used for scaffolding out a Sinatra project. A gem for future Learn students so they could easily get started building their projects. Although built with them in mind, this can get you off and running with any Sinatra app.

Install the gem, run `corneal new APP-NAME`, **make sure run `bundle install`**, and you're all set! This will create your directories and your Gemfile will have the majority of the gems needed to make an application. It uses a file structure similar to what you would see with Rails. Of course, if you want to add gems, you can surely do so, by putting them in your gemfile and running a gem install. You can start up your server with shotgun and verify everything is working. It is as simple as that.


To see the github repo [Click Here](http://github.com/thebrianemory/corneal)

For a video on how to use the corneal gem [Click Here](http://instruction.learn.co/student/video_lectures#/353)


### *Understanding which either models or controllers get the ActiveRecord or the Sinatra  Base Functionalities*

One of the biggest confusions that I have had within the project was which files gets the ActiveRecord::Base functionalities and which files get the Sinatra::Base functionalities. 

The classes that inherit from Sinatra::Base and define the HTTP interface for our application are called Controllers.
In a single controller application, a single file defining the controller, like app.rb, will suffice. That controller will define every single URL and response of our application. Controllers define an HTTP method using the sinatra routing DSL provided by methods like get and post. When you enclose these methods within a ruby class that is a Sinatra Controller, these HTTP routes are scoped and attached to the controller.

```
class MyToDoApp < Sinatra::Base
 
  get '/' do
    "Hello, World!"
  end
 
end
```


Active Record is a Ruby gem, meaning we get an entire library of code just by running gem install activerecord or by including it in our Gemfile. These classes have gained a whole bunch of new methods via its inheritance relationship to ActiveRecord. Let's look at a few of them [Click Here](https://learn.co/tracks/online-software-engineering-structured/orms-and-activerecord/activerecord/activerecord-mechanics)

```
class Student < ActiveRecord::Base
end
```


 ### *How do we get our tables started with adding our columns with data?*
 
 By running  `rake db:create_migration NAME=create_products` we can create a new migrations file within our directory within the db/migrate section. In this case we created a `create_products` table, but we can create tables depending on what we are building. Here in this file we will create our table by the following code below:
 ```
class CreateProducts < ActiveRecord::Migration
  def change
    create_table :products do |t|
      t.string :name
      t.text :description
    end
  end
end
```

After, we run `rake db:migrate` within our terminal and we should expect a new file which is schema.rb, displaying our tables

```
ActiveRecord::Schema.define(version: 2008_09_06_171750) do
  create_table "products", cascade do |t|
    t.string   "name"
    t.text "description"
  end
```


### *Adding a column to the table*

It is best practice when adding a new column to a table to create a new file and add the column within that new file instead of adding it within the schema or the primary files. The reason of this you want to keep track of what has been done and keep things organized. Here we are adding a column to our products table, column name will be `part_number` and the type will be string.

```
class AddPartNumberToProducts < ActiveRecord::Migration
   def change
      add_column :products, :part_number, :string
   end
end
```

If any questions about adding or removing, or need more details about migrations, For more information, [Click Here](https://edgeguides.rubyonrails.org/active_record_migrations.html)


### *How does the Helpers class play a huge part within making our application more secure?*

This class will help us determine if either,

1. A user is logged in
2. If the user is the current user 

We created two class methods to distinguish and help us throughout the application to figure out the current user and if a user is logged in. Within the class method, `def self.current_user(session)` will help us find the User by the user's id and will be set within the session when the user is logged in. Session cookies allow a website to keep track of your movement from page to page for that specific session (from the time you log in to the time you log out or close the browser). Session cookies simply allow you to navigate through a site without repeatedly having to authenticate yourself on every new page you visit within the web application domain. Session cookies expire every time you log out or navigate away from the website.

```
class Helpers
  def self.current_user(session)
    User.find_by(id: session[:user_id])
  end

  def self.logged_in?(session)
    session[:user_id] ? true : false
  end
end
```

Lastly, the class method, `def self.logged_in?(session)` will tell us if there is a session, by using a [Ternary Operator](https://www.rubyguides.com/2019/10/ruby-ternary-operator/), this will tell us if there is or there is not a session. Therefore, true or false.












