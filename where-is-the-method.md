title: Where is the method? 
subtitle: How to find a method location in Rails 
category: log
tags: ruby, rails
date: 2020-03-10
Status: draft

You are an experienced developer. You probably have worked on a number of languages and framework. You are used to finding your way around the code quickly. You recently joined a Ruby on Rails team working on an existing application, and now you are lost.

Where are the 'require' statements? Where is this variable or method declared? How is this code getting this data? How is this working at all?

If you have found that you are asking yourself these questions, this content is here to help you. 

## Carefully read the error message

Usually the error message stack trace will have an entry with the file and line number where the error occurred. If lucky, it is breaking in your application code. Usually you will see many lines with rails code, and at some point your application code.

Open that file and look for that line. Sometimes you can see the error and fix it. 

Sometimes you will run into a mystery method that is not defined in that file. What do you do now?

## Search your code with ack!

Ack! is a grep-like tool for programmers. Install it and start using it. It is super useful for finding code. Sometimes doing a search on your code base is the quickest way to find where a method was defined.


## All the objects on in global scope 

If you have used an MVC framework before, you are used to some conventions, like having folders for models, views, and controllers. Use your experience to navigate code.

What will be surprising is that Rails doesn't use 'require' statements. Instead, Rails sucks all ruby classes declared under the `app` folder. Expect all of these classes to be in your global scope.

The above is a gross oversimplification. Yet it should be helpful as you start working in Rails. Assume those are there. Learn the specifics as you need.

If you are truly stuck on how something is put together, you have two choices. The first one is to read "The Rails Way" for the version of Rails that you are working on. You should think of this as a reference book that you consult when some area of Rails makes no sense.

If you are still mystified, then go and read the Rails source code in github. Do this if the behavior doesn't seem to match documentation or answers on Stack Overflow.

## Gem code is under .bundle

If you are looking for code and you can't find it in your source code, then it may be in a gem, the name for a Ruby library. Listing your directory with `ls` won't show the folder where they are.

If your application is using Bundler, you will be able to `ls -a` and see the hidden directory called `.bundle`. You can navigate this directory and find the gems that Rails is using.

## Learn about Ruby's method dispatch

The very basics of Ruby's method dispatch is that you call the method from an object. If it can't find it, it will start going up the object's ancestors until it finds where it is declared or it finds out it cannot find it anywhere.

The above is a very simplified version. Yet it should be useful to begin with. As soon as you can, read a more detailed explanation here.

If you have more time, read these chapters of "Metaprogramming in Ruby 2". They go into a lot of depth on Ruby's object model and method dispatch. I found the explanations superb. 

## Learn basic Ruby reflection

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

## Use the debugger

Ask what debugger the project uses. It will most likely be Pry or Byebug. They are both command line debuggers. If you come from a language that commonly uses an IDE, a command line debugger is essentially a command line shell where you step through the program. You can also query what variables are declared, see which objects are available, and inspect the variables.  

If your team doesn't have a debugger, spend some time and install one. Install Byebug, which is the default debugger for Rails. It also runs via TCP sockets, so you can configure it to run on a specific port so that you can log into the debugging session from a different shell. This is useful if your application is using something like Foreman.


If you put all of these together, you should be able to quickly find the method is causing you problems.
