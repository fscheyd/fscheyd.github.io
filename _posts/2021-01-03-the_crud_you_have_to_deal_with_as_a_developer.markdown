---
layout: post
title:      "The CRUD you have to deal with as a developer."
date:       2021-01-04 00:08:55 +0000
permalink:  the_crud_you_have_to_deal_with_as_a_developer
---


### Freedom Scheyd

Developing the second project for the flatiron bootcamp has proven to be  very interesting. Particularly within the context of how one develops the code for the application we are tasked with building. I decdided to develop a simple application that allows a user to create a profile for a TTRPG character and log the information for the monsters said character might have seen. For this project the term 'minimum viable product' is the theme. The limited breadth of my knowlege and the challenges I've faced for this project has required me to create a passable application with the least amount of time spent creating it. With that this post is to dive into one of the major concepts in this project that have helped me the most. And that is **CRUD**. Crud stands for: Create, Read, Update, and Delete.

On just about every website you'll see these functions employed in every aspect. Particularly with this project I saw this as the girth of the content I was to understand This post is pretty much broken up into 2 components: the understanding of CRUD and then the application within this project. The cool thing is that these concepts are used far and wide.Whether it is facebook, or gmail, or even, one on my personal favorites, dndbeyond, there are requests constantly being sent and pulled by you, the user, and you dont even realize it. Lets break it down.

## Create

You can break up create into 2 concepts: New and Create. When you first make an account on a website the first thing you'd do is make an account. In order to do so there has to be a form displayed for you to fill out. You'd enter email, name, password, etc. Now in order to take in this information the code will present the form for you, the user, to input. Utilizing something like:

```get /user/new``` 

The code will pull the data from the html file, or ```new.erb``` and present a form for you to submit. Once the information has been filled out the information is submitted or posted into the code and thus the database.

```post /user``` 

Essentially it sends a post request to the software to process the information. Now it probably will not redirect you to a brand new page with a form like before, instead a user would be redirected to a ```show.erb``` or ```index.erb``` but the database input has been created!

## Read

The next aspect to understand when it comes to this CRUD is the read aspect. similarly it can easliy be broken down into two concepts. They are index and show. Index is great because it can show you all of the things. Simply put a get request is made using the:

```get /user``` 

method. Then you input that it is to pull from the index.erb now the application can present all of the information that was input. But sometimes you want to go a little deeper. Thats where the show part of this comes in handy. 

Show takes in the information both from the index and the user, and will actaully allow the application to pull up specific details out of the database application that was created. 

```get '/user' do
            index.find_by(id:params)
end```

This is an example of what this sort of method would actually look like. Looking into this the get request is made utilizing the user information, then the data is passed through the index to pull information that meets the parameters of the authenticated user looking to pull information from the application. This is an awesome functionality when it comes to building out developed applications. But with this is needed the ability to actually change the information. 


## Update
This part of the CRUD concept allows users to change information within the database. This particualrly was important for my project because a character in a TTRPG might actually learn new information that their character did not know before.  Like Create and Read, this can be broken up into 2 ideas. Edit and Update not going too far into the code conceptually what this does is simple, it 'edit's' the information. this requires a view or in this case an 

```edit.erb```.

From here the information is processed using ```/put``` or ```/patch```. This part doesnt require a new view as the information replaces the outdated information that was updated by this function, so the app can be routed back the the ```show.erb```. Now onto the last bit of CRUD.


## Delete
Often times we mess up, (i.e. my sinatra project) so we have to remove data from a database. So we'll have to take an instance and wipe it from the application. 

```instance = Model.find_by(id: params)
instance.destroy```

In the case of my application, if a user inputted the wrong infromation for a creature they've seen they might need to delete that. This function serves that purpose. It'll actually go into the database and make sure it is never seen again. A little dark? Anyways I digress.

## My Project
Why CRUD is so important is because with our minds on these functions it helps build out the routes for a sinatra application. It actually for me helped to understand simpler ways to code things and find solutions that I wouldn't have been able to see. Mostly when I would be stuck I could revert to these concepts and the solution would ```show.erb``` itself. 

The hardest part for me was routing my usder controllers becuase the infromation was more conceptual. It's easy to list out certain details for a monster and they would only be relavant in the instance of a particular user. But the user itself requires filling out a form, routes that deal with the instance of an incorrect form, and even the creation of a new user. Having the ability to see past these issues using CRUD helped the development for the code in my sinatra project.  The applications are limitless, and allowed me to create a beautiful creature collector for your TTRPG use. Thank you very much.

