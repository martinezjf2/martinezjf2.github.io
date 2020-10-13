---
layout: post
title:      "Serializers"
date:       2020-10-13 00:00:14 -0400
permalink:  serializers
---



One of the best things that I have learned far as so many great things I have learned, is the use of serializers. This will help you to establish your associations within your models in your database.

## What are serializers exactly?

Active Record Serializer is a gem we can install within our gem file which will provide a convention-based approach to serializing resources in a Rails-y way.

How is that different than when we created our own serializer by hand and used it in the controller? Remember:

```render json: @teacher.to_json(only: [:name, :degree, :university_id],
                          include: [university: { only: [:name, :state]}])```

We had to explicitly tell Rails what data to return whereas ActiveModel Serializers will take care of this for us.

## Installation


 In order for us to implement this, we will first have to install the gem in our gem file and bundle install to complete the installation. 

`gem 'active_model_serializers'`

This gem has a generator that we can use to establish our serializer from our terminal. Next we will run this command to create a new serializer. In this case we will add two serializers:

`rails g serializer teacher`

`rails g serializer university`

The serializers will be automatically added to a serializers folder within the app directory.

## Associations

Let’s assume the attribute for a teacher are name, degree, and university id. Let’s assume that university has attributes of a name and a state.  Apart of created our has many associations within our models, we will also establish what content we want to see when we render json within our controllers. In other words, instead of implementing this: 



`def show`

   ` @teacher = Teacher.find(params[:id])`
		
   ` render json: @teacher.to_json(only: [:name, :degree, :university_id],`
	 
           ` include: [university: { only: [:name, :state]}])`
					 
 ` end`
	
	

We will clean up our code with our serializers. We can set up what attributes we want to see, and associate them with each other by nesting them. Let’s start!

## Setting it Up!

Lets first set up our teacher serializer:



`class UniversitySerializer < ActiveModel::Serializer`

  `attributes :id, :name, :state`
	
`end`



Lets set up our university serializer:



`class TeacherSerializer < ActiveModel::Serializer`

 ` attributes :id, :university_id, :name, :degree`
	
`end`

When we go to /universities/1 we should receive something like this:


`{`

`  id: 1,`
	
 ` name: “Nassau Community College”,`
	
 ` state: “New York” `
	
`}`

## Relationships

How can we nest our associations so instead of fetching data several times to different url’s,  we can simply just make one fetch request? Making a has_many relationship within our serializers.
Lets say our teachers belong to a university:


`class TeacherSerializer < ActiveModel::Serializer`

  `attributes :id, :university_id, :name, :degree`
	
  `belongs_to :university`
	
`end`


This will result our json object to be rendering the teachers’ and universities data as of like this:



`{`

 ` id: 1,`
	
 ` name: “John Johnson”,`
	
 ` university_id: 1,`
	
` degree: “Bachelor in Computer Science”,`
 
`  university: {`
	
   ` id: 1,`
	 
		
    ` name: “Nassau Community College”, `
		
		
    ` state: “New York” `
		
`  }`
	
`}`


And our code within our controllers will end up to be cleaned up like this: 



`def show`

   ` @teacher = Teacher.find(params[:id])`
		
		
    `render json: @teacher`
		
		
 ` end`
	


Interesting right?

