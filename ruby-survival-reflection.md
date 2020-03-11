title: Survival Ruby Reflection
subtitle: Some basic Ruby reflection methods to make your life easier
category: log
tags: ruby, rails
date: 2020-03-10
Status: draft

Ruby has a strong reflection system. This is useful when you are debugging. You can read this blog post to learn more about it. Let me share some of the most useful

   my_object.inspect

This will give you a string representation of the object. Useful when debugging.

  my_object.respond_to? :method_name

This one will tell you if the object can respond to a method. So Let's say that you want to call `batman.swing`. But can you? You can query the object with `batman.respond_to?(:swing)` and it will answer with true or false. Notice how you need to use the colon for the method name when sent as a parameter.

   my_object.methods
   my_object.methods.sort
   (my_object.methods - Object.new.methods).sort
   
This will list all the methods that the object can respond to. The second one sorts the methods so it is easy to scan for one. The last version will remove all of the methods that are inherited by Object, the root parent object that most object descend from.

   my_object.method(:method_name).source_location

This is perhaps the most useful one when looking for code. This incantation will give you the source location for the method that the object responds to.

There are other useful one, but these should keep you productive.


