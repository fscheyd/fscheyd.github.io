---
layout: post
title:      "Deep Dive into ActiveRecord Associations"
date:       2021-01-22 23:06:34 +0000
permalink:  deep_dive_into_activerecord_associations
---



After wrapping up the ActiveRecord/Sinatra Project one concept in particular stood out as one of the most important concepts in terms of functionality and use/versatility: ActiveRecord Associations. In this blog post we're going to take a deep dive into how ActiveRecord associations function and the different methods they'll provide to an application, as well as how they communicate with a database in a sinatra application.

So to start by providing some context, I am an avid fan of table top gaming. D&d is my favorite game to play, and many of my friends tend to play as well. Within the game you play as a character. That character might have a limited knowlege in comparison to the player who is playing the character, and that character can only act on information that they know, and not what the player knows. So for my project I built a creature collector that stores the creatures the character has seen and the limted information that they may have. Utilizing ActiveRecord I was able to build a very simple application that accomplishes this. 

In ruby we code using object oriented programming, it is a paradigm based on the idea of which an 'object' contains data in the form of attributes, and procedures which is referred to as methods. But when information is passed through the code, it is not stored. We utilize database code such as SQL to store the information. In order to allow these two aspects of our code to communicate, we utilize Object Relational Mapping or ORMs. In the case of Ruby and Sinatra we're using ActiveRecord.  

What ActiveRecord does is that it takes in information that has been stored as data in a database using rows and columns and interacts with something that requires SQL as if it were an object.  So lets take a look, instead of using something like this query: ```SELECT * FROM users``` and then converting the results into an array we can produce an array of user objects with a snippet of code that looks like this ```User.all```. Basically what we did is we took the information from the User class that is inheriting from ActiveRecord, and we utilized one of the given methods from this to make an array of all the users in an application. We get a whole bunch of these through ActiveRecord! Here are a few:

```Object.column_name
Object.create
Object.find
Object.find_by
Object.save```

Now lets dive deeper.

For this project an app was built utilitizing the framework of the Model-View-Controller, or MVC. This is particularly useful becuase it gives certain files certain jobs, and allows the data to flow seamlessly. Breaking it down we have these three components, using the analogy of a restaurant:

* Models: This is the basic foundation or the 'logic' of an application. This is where data is can be changed or saved. This could be compared to the chefs in a kitchen taking in orders and processing them and cooking them in a timely mater.

* Views: The Views are what the individual utilizing the application interacts with. It often contains different forms and links that the user will use to submit information to be stored in the application database. This is where the visual code is kept(e.g. HTML, CSS, Javascript), and will be the only thing that the user side of the app will interact with. Think the storefront, or the tables in which a customer will order from.

* Controllers: In a restaurant we have chefs, and customers accounted for so far in the MVC framework, what we dont have (arguably the most difficult position in my personal experience) is the waitstaff. That is what the Controllers do. They relay information and route the data that the user inputs to be handled by the Models or the logic of the application. 

Let's look closer at the models because thats where our associations lie. 

My application had two tables of information in the db file. The users and the monsters. The User table had the character name, the user's email address, and the password. The monster table had within it the monster name, monster type, the challenge rating, any apparent weaknesses, and lastly the user ID which the monster belonged to. In order to allow my application to interact with this information I built 2 model files within my code: Monsters.rb and Users.rb, and within these models I entered in my macros. What macros do is super wonderful because it streamlines the coding process for us, and it is always better to work smarter not harder.  Macros are methods that write out code for us so we don't have to.  Here are some of the macros that are available to us in ActiveRecord:

```class Object
    
		belongs_to
		has_one
		has_many
		has_many :through
		has_one :through
		has_and_belongs_to_many
		validates 
		has_secure_password

end```

Each of these macros have a particular use, but within my project models I only used 4 ```belongs_to```, ```has_many```, ```validates```, and ```has_secure_password```.  Each of them served very important uses, when it came to the application, some more for security, and determining correct input of a form; but for today we're going to focus on the asociations.  Associations allow us to form relationships between data on different tables. Here is my user model class:

```class User < ActiveRecord::Base

    has_many :monsters
    has_secure_password
    
    validates :character_name, presence: true
    validates :character_name, uniqueness: true
    validates :email, presence: true

end```

Right off the bat you can see that I inherited from ActiveRecord::Base, which grants me access to the functionality of ActiveRecord within the Object. The first method that can be seen is ```has_many :monsters```. Pretty much what was built here is the idea that a user utilizing this application to track the monsters in their game has access to a list of monsters that they've inputted into the application's database. To round off the other side of this relationship here is my monster model class:

```class Monster < ActiveRecord::Base

    belongs_to :user
    validates :name, presence: true
    validates :monster_type, presence: true


end```

This relates the table of monsters that I related to the user who had inputted them. With these macros present I now have access to all sorts of methods that I can use within my controllers to route information and protect the users data. here are a few just to name them:

```current_user
monster_count
find
find_by
get_type_of_first
save
delete```

It can easily be seen the functionality that associations provide, because if one were to hard-code these ideas out one could easily lose track of the application's functionality in trying to match the database's information with each other manually. Essentially it results in a very dense pile of code that is hard to sort through in the event of a significant error. It really lends an aspect of fluidity to the code that is created. one of my favorite examples was in this post request in my monster controllers.

```monster = Monster.new(params[:monster])
        if monster.save
            redirect "/monsters/#{monster.id}"
        else
            @errors = "[" + monster.errors.full_messages.join(", ") + "]"
            erb :"/monsters/new"
        end```
				
So I set a variable of monster to call on the Monster class within my models which contains the logic of my monster database, and I called on the ```.new``` method which was given to us through the utilization of my ActiveRecord associations, which creates a new monster if the input meets the paramaters of a monster. Now the conditional was created so that way if the monsters paramters are met it will save and redirect to the now monster page with an id, and in the situation that there is incorrect input, the user renders the new monster form with an error message displaying that the input was incorrect.

ActiveRecord is very awesome when it comes to building out applications that requires access to stored information, and it is very valuable provided the logic of how the code flows is understood. I hope this deep dive into the adventure of ActiveRecord helps all the programmers with their code.  Happy adventuring!


		



