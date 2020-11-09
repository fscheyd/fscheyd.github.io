---
layout: post
title:      "See ya later Iterator!"
date:       2020-11-09 19:02:30 +0000
permalink:  see_ya_later_iterator
---


**A breif detailing of the iterators .each, .collect, .map, .select, .find_all in ruby.**

The purposes of creating application is the ability to break down information and be able to use it in an applied setting. Often there are large amounts of data which have to be sorted through, like for banks it would be account numbers or balances. For a video game it could be character stats and ability improvements and whatnot. All of this boils down to taking in values storing them and altering them if needed. Throughout this will be samples of code which are more or less not really applicable in a real setting but more just a visual representation of the concept.

Ruby does a wonderful job of allowing this necessary function to be quite simple with these basic iterators: .each, .collect, .map, .select, .find_all. 

```.each ```

This function is great because it takes the input of, let's say, an array and will make whatever changes we tell it to. 

```
array.each do |stuff|
      puts stuff ** more_stuff
end
```

The output for this would be a whole lot of stuff, but the return would be the original stuff that we input into the code. This actually brings us to the next function, .collect.

You see with .each the return value will be that of the original array. With .collect and .map it will actually take the input and it will actually return a new array of information based on we tell the code to do. It takes the outputted information and stores it in an array so we dont have to write the code out ourselves.

```
array.collect do |stuff|
      puts stuff ** more_stuff
	    stuff ** more_stuff
end
```

This will return a new array with all the extra more stuff multiplied by the original stuff. Also note that .map is the same method as .collect but with a different name. Sometimes in coding we don't need an entire array of information returned but just certain elements. That is where the .select and .find_all methods of iteration.

```array.select {|stuff| stuff.morestuff?} => [more stuff, more stuff]
array.find_all {|stuff| stuff.morestuff?} => [more stuff, more stuff]```

Using these functions will return specific pieces of data based on the input array.  For example a list of years and it could pull years that had a superbowl. What makes these two snippets of code different is how they work with hashes as opposed to arrays. When using .select, and .find_all, what makes them different is how they return information. If we use .select on an array we return the original input. So looking at the example of superbowl years if we used select we'd return:

```{:1991 => "superbowl year: NY Giants", :1992 => "superbowl year: Washinton Redskins", 1993 => "superbowl year: Dallas Cowboys"}```

But if we used .find_all what returns is pairings of key to value in an array. This is what that would look like:

```[[:1991, "superbowl year: NY Giants"], [:1992, "superbowl year: Washinton Redskins"], [1993, "superbowl year: Dallas Cowboys"]]```

Each of these tools are very valuable in the context of code and iterating over arrays, and hashes. I hope this post helps you along in your discovery of programing in Ruby.
