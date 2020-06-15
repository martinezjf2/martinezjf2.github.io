---
layout: post
title:      "My Challenge with Omniauth"
date:       2020-06-15 03:30:53 +0000
permalink:  my_challenge_with_omniauth
---


## *Ruby on Rails Project*


Throughout the Ruby on Rails project, I have definitely felt that this was a challenge. We are about four months until graduation. From not knowing anything about programming with the Ruby language, to now knowing how to start a project with the Rails framework. So far, I feel confident on thinking as a developer, and yet again, there is much more to learn from. Within my project, i was thinking of an application where i can write notes of all the books that i have read, basically an application that also benefits me, to save important context that i have learned about. My main focus within this project was implying the Omniauth gem. This was a challenge.


## *What is the Omniauth Gem?*


As stated on [learn.co](https://learn.co/tracks/online-software-engineering-structured/rails/auth/omniauth) , OmniAuth is a gem for Rails that lets you use multiple authentication providers alongside the more traditional username/password setup. When implementing this gem, it is important to know several things to make sure that your link to sign in with the provider functions properly. Not only requiring the omniauth gem and the omniauth-"provider" , within your gemfile, but also the 'dotenv-rails' gem. This gem is one of the best ways to ensure that environment variables are correctly loaded into the ENV hash in a secure manner.



## *Setting it up*


First we want to go to the [facebook developer](developers.facebook.com) site and create a new app. Click on www icon and type in https://localhost:3000/ as the Site URL. Click Save. Then you want to go to the settings under Facebook Login and type https://localhost:3000/auth/facebook/callback on the Valid OAuth Redirect URIs. Make sure you save these changes. After all that is done you want to go to your basic settings and copy your key and ID. In your application, we want to create a .env file on the root directory and paste you key and id like this:


`FACEBOOK_KEY=12345678987655`

`FACEBOOK_SECRET=1nj2bj42i2bng22421v43h3bh43h`


VERY IMPORTANT: Make sure to name this file within `.gitignore` file. We want to make sure that every time we push our data to the repository, we do not want to upload our facebook id and key. So that being said, the code above is a made-up key and secret.


## *Routes*

Within your routes.rb you want to make sure that you set a get request for the login for facebook. So I put this code within my routes

`get '/auth/facebook/callback', to: "sessions#fb_create"`

## *SessionsController*

At first, i created a private method in order to access the data within the request

`private`

    def auth
        request.env['omniauth.auth']
    end
	
	
Within my create action is where i implemented my code to create or find the user's email. If it was not found, then it would be created. In my case i had to split the name into a first name and a last name in order for my validations would pass so it can be created. 


``` 

def fb_create
       @user = User.find_or_create_by(email: auth[:info][:email]) do |u|
            u.first_name = auth[:info][:name].split[0]
            u.last_name = auth[:info][:name].split[1]
            u.username = auth[:info][:name]
            u.password = 'omniauth_password'	
						
          if @user
            session[:user_id] = @user.id
            redirect_to books_path(@user)
						
          else
            redirect_to login_path
          end
end ```

## *Link_to*

Having the link to will be important in this process making sure you require it within your view. Making sure you have a text and a path to redirect it towards. For example:


`<%= link_to('Log in with Facebook!', '/auth/facebook') %> `

## *Last Step*

Testing out your link. Making sure that all these steps are followed and making sure that the controller and routes are set up properly. Hope this helps. Thank You!



Several things to keep in mind: 

* install the omniauth gem in gemfile
* install the omniauth-facebook gem in gemfile
* install the dotenv-rails gem in gemfile
* create a .env file within the root directory (which will contain the secret and the ID)
* make sure you have the route set up in the routes
* make sure your link_to is set up properly
* make sure you have the omniauth.rb within the initializers directory


