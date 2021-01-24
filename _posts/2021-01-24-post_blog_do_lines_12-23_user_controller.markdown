---
layout: post
title:      "post '/blog' do |lines 12-23 user_controller|"
date:       2021-01-24 19:13:49 +0000
permalink:  post_blog_do_lines_12-23_user_controller
---

Hello reader, in this blogpost we're going to take a look at one of the post requests in the sinatra project that I have coded. This post request in particular is the login request that redirects the user to their index page when they successfully log in, or renders the login page with errors when they don't enter the correct information. Below is the whole request, and below that I will be breaking down the code line by line. 

```post '/login' do
        user = User.find_by(character_name: params[:character_name])
        if user && user.authenticate(params[:password])
            session[:user_id] = user.id
            redirect to "/monsters"
        else
            @errors = "Sorry the input was invalid."
            erb :"/users/login"

        end
    end```
		
	
So my project is an app that a user would use to store monsters a character would have seen within the game of Dungeons & Dragons. Now in order to be able to use the application, a user has to log in. As is the case with many applications e.g. facebook, gmail, dndbeyond, etc. This is accomplished when the user fills out the login form and clicks enter. The application sends a post request to the application.
		
```post '/login' do```
		
This is where we define the post request, or where we tell the application to post the form that the user inputted. The data will pass through the rest of the request to determine if the submitted data is valid. /login is the path that we're are taking for this route. Looking below we see the first snippet of code within the request.
	
```user = User.find_by(character_name: params[:character_name])```

Here we assign a local variable: ```user``` to be the value of the the current user. To do this we call the User class in my user model and use the ```.find_by``` method to find the first record matching the specified conditions, we gain this method through the User class in my models, and the associations we've created. Utilizing params, a hash granted to us by sinatra, we limit the data to just the character name, which has a set presence and uniqeness for validation purposes. We then call on the variable in this conditional statement below.
		
```if user && user.authenticate(params[:password])```
		
Essentially we created an if statment that calls on the user variable we set above. If the user variable returns true based on the parameters, or if the character name is found in the character name hash it will check out and move onto the next part of the statement. The conditional statment then checks to see if we can authenticate the user by accessing the encrypted password hash, and if the input is correct we will return self, and BOOM! We have access to our user id and we store the user ID to the session hash. The session hash is then stored into a cookie thats managed by rack under the hood.
				
```session[:user_id] = user.id```
	
Cookies are used to persist state, or keep the data across many HTTP requests. So now when the information passes through the rest of the User Controller, the cookie which contains the session hash with the current user and persists the data(with the current users information attached to a cookie) through and redirects to the montser page.
		
```redirect to "/monsters"```
		
What I'm doing here is issuing a new request to get the index page with the user's authenticated information stored in a cookie. Long story short: if the user is ```logged_in? ```(which is determined by a conditional in my monster controller) then we'll have access to the user's individual monster index page, and all the scary beasts that their character has seen! Awesome!
		
```else
            @errors = "Sorry the input was invalid."
            erb :"/users/login"```
	
In the event the if statement returns falsy, or nil, the else statment instantiates a variable called errors which we assign the message "Sorry the input was invalid." We get this variable from ActiveRecord, and are generated when the validations aren't met. The validations are checked any time we try to save (or use the .valid? method). In this instance we're trying to save the current user in the session cookie and validate it with the User model. Since the input was invalid the login page gets re-rendered and shows the login view with the error message above the login form. After this we have to close our statements and requests with end, which is simply ruby syntax.
				
```end```

This end closes out our conditional statements. And the following end closes our request. I hope you enjoyed this breakdown of my User controller ```post '/login/ do' route``` Sometimes when it comes to understanding a conept better breaking things down line by line can offer the most insight.

    ```end```
