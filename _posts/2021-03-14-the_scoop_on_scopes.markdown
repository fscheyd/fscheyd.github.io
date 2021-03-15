---
layout: post
title:      "**The Scoop on Scopes**"
date:       2021-03-15 02:31:12 +0000
permalink:  the_scoop_on_scopes
---


Finishing up this, rather challenging, project to creat a Rails framework application has been just that. But along the way I learned some very important concepts. One in particular stood out to me more than anything else. That would be **Scope Methods**. This function is particularly useful because allows you to grab objects right out of  a database youve built and actually chain them throughout an application. 

**Scope methods** 

```class Lightsaber < ApplicationRecord
  scope :lightsaber_awesomeness, -> { where("awesome_level > 4") }
end```


Now, if you couldnt tell I love Star Wars. One of the coolest aspects of Star Wars hands down is the lightsabers. There are many characters who wield lightsabers, so it would stand to reason that I would have my favorites. Let's say I decided to create an application that allows users to rank, list information about, and talk about their favorite lightsabers. That's a lot of information to sort through within a database especially when writing the logic for certain functionalities can be cumbersome when using class methods. What scope methods allow a developer to do is literally be able to pull objects out of the database. 

If you look above I've created a scope method.  The scope method within the lightsaber model of this theoratical app guarentees an ```ActiveRecord::Relation``` and pulls out all of the lightsabers within that have an awesomeness level of four or higher. This is really useful when it comes to putting together methods because you can chain this onto other scopes.

```Lightsaber.lightsaber_awesomeness.lightside_user```

Or if your're a dark side user.

```Lightsaber.lightsaber_awesomeness.darkside_user```

For thie purposes of this I've implied that there was already a scope method pulling out if the lightsaber was for a light side user or a dark side user.  But what makes scope methods so useful is that they keep code clean. Whenever you see a scope method in code you can always expect what it will do because specific values can always be returned because scopes have specific criteria it needs for them to withdraw the objects for the purposes of app development.

Scope methods are very useful when trying to keep code clean  and keeping my apps DRY. Although A jedi might not need a scope to weild their lightsaber! May the force be with you!






