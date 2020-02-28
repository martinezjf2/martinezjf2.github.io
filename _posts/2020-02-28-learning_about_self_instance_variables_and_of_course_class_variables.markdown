---
layout: post
title:      "Learning about Self, Instance Variables, and of course, Class Variables"
date:       2020-02-28 18:31:21 +0000
permalink:  learning_about_self_instance_variables_and_of_course_class_variables
---



One of the biggest confusions that i have encountered within the Object Oriented programming within ruby and within my CLI Project was the scopes of the Instance and Class Variables. Also, the meaning of self was also a huge confusion and one of the reason for this blog post is to make sure students as well as i, fully understand this topic. The main thing to remember is that instance variables are accessible in all instance methods while class variables are accessible in all instance methods and class methods because they are available to the whole class.


> What are Instance Variables and what is their scope?

We define Instance Variable with an @ symbol. They hold information about an instance, usually an attribute of that instance, and can be called out throughout the class, without needing to be passed into other methods as arguments. As we stated before Instance Variables are accessible in all instance methods.

For Example:


```
 `def valid(input)
        if Countries::Country.find_by_name(input)
            @country = Countries::Country.find_by_name(input)
        else
            false
        end
    end'
```

In this case the Instance Variable would be the @country which is assigned to an instance of a country based on the user's input to see if the country does exist within the array.




> What are Class Variable and what is their scope?

Class Variables are defined with a(n) @@ symbol.  The difference between Class and Instance Variables is that Class Variables can be accessible within instance and class methods because they are available to the whole class. 

For Example:

```
class Countries::Country
    
    attr_accessor :name, :capital, :population, :timezones

    @@countries =[]


def self.all
        @@countries
    end
```

As you can see, the class variable is @@countries, which is set equal to an empty array. In order to access the class variable to other classes, we would have to create a class method such as `self.all,` in order to use the class variable through a method to other instance and class methods outside of the class.


>What is Self?

One of the most confusing concepts to understand is self.  In this example, we have two implications of the term self. But do they mean the same thing with the code we implement? 

If self is applied such as in a class method, such as `self.all`, this is referring to the class itself. 

Now such as in the example, would it be the same meaning if i applied this,?

`@@countries << self`

Not necessarily. What we are really saying within this code is that for every instance of country I recieve, I want to push it in within the class variable, which equals to an empty array. Self in this implication would refer to as an instance of a country.


```
def initialize(attributes)

        
    attributes.each do |key, value|
         begin
                 self.send("#{key}=", value)
         rescue NoMethodError
         end
						
     end
				
        @@countries << self
     end

def self.all
     @@countries
end
```


I really do hope this helps if anyone is stuck on these concepts. They are tricky to understand but it is possible to do so.  



