title: When you Are New To Rails 
subtitle: Some pointers for developers new to Rails 
category: log
tags: ruby, rails
date: 2020-03-09

Are you an experienced developer? Have you been tasked to help out in a Rails project? Do you feel confused because there are no 'require' statements and variables seem to mushroom out of nowhere? Does Rails seem too magical to you? 

If this describes you, don't worry. I have gathered this quick list of pointers to help you find your bearing. Hopefully they will make Rails more logical and less magic.

### Rails loads all objects found under the 'app' directory into the global scope

This is why you don't see 'require' statements. Most objects are available in the global scope.

Why? Think of it as a radical kind of Don't Repeat Yourself (DRY). Whether you think this is a good idea doesn't matter. This is a Rails convention.

The title statement may be a gross oversimplification. Yet it will be helpful if you assume this is true unless proven wrong. 

### Carefully read the error messages 

Ruby errors are usually useful. They tell you what went wrong along with the location where the problem happened.

Ruby's error stack trace will usually give you the file and line number where the failure has happened. This is key for solving problems. The stack trace will usually have a mix of code from our application and from Ruby libraries, commonly called gems. 

Read them like this: starting from the top, scan line by line until you recognize a file from your application. Identify the file and line number, and start your debugging there. 


### Learn about Ruby's method dispatch and reflection

Ruby does what you expect until it doesn't. It will all seem magical and confusing unless you understand how method dispatch works.

Method dispatch is Ruby's process of looking for a method definition to execute it. When you call 'batman.punch', method dispatch is trying to find where the '.punch' is. It start looking for a definition in the object's class, and then it goes up the object's ancestors. That is the basic idea.  

 The basic idea is also wrong. It is more complicated than that. Read this blog post to get an accurate picture: [How Ruby method dispatch works](https://blog.jcoglan.com/2013/05/08/how-ruby-method-dispatch-works/)

Ruby has a strong reflection system. You can query a lot of information from an object. Using reflection methods is more useful if you understand how method dispatch works. But even if you don't, the following two methods will be useful right away.  

    batman.inspect

'.inspect' gives you a string representation of the 'batman' object. Useful in the interactive ruby shell (irb), in the debugger, or  when printing to the log or a debugger via a 'puts object.inspect'.
 
    batman.methods
    batman.methods.sort

'.methods' gives you an array of all of the methods that the 'batman' object can respond to.  If you add '.sort', then they will be sorted alphabetically.

If you want more in depth information, read chapters 2 and 3 from the book [Metaprogramming Ruby 2](https://pragprog.com/book/ppmetr2/metaprogramming-ruby-2)

### The docs: Ruby Doc, Rails Guides, The Rail Way, and the source code

[Ruby Doc](https://ruby-doc.org/) should help you if you have questions about the language. The documentation is well written and useful. Ruby is programmer friendly, so if want a method to do something to an array, it most likely exists. I often consult [Array](https://ruby-doc.org/core-2.7.0/Array.html), [Hash](https://ruby-doc.org/core-2.7.0/Hash.html), [String](https://ruby-doc.org/core-2.7.0/String.html), and [Enumerable](https://ruby-doc.org/core-2.7.0/Enumerable.html).

[Rails Guides](https://guides.rubyonrails.org/) should be your first option to learn anything about Rails. For example, if you are learning about Active Record or how to make a configuration change, you should consult this site first.

You can't find what you are looking for?

[The Rails Way](https://leanpub.com/tr5w) should be your next stop. Look for the correct Rails version for your application. It has clear and in-depth explanations on how the different parts of Rails work. 

Still mystified or confused?

Read [Rails' source code](https://github.com/rails/rails). It is recommended for you to look the source code up if all of the above have failed. Read it if you are curious on how something is put together. Read it if you need to check exactly when some feature was added or removed. 


### Use a debugger

Ruby has two popular command line debuggers, Pry and Byebug. When you add their name your code, it will open an interactive, command line  shell where you can inspect values, query the variables available in the global space, and do a lot more. 

If you have learned about Ruby's method dispatch and Ruby's reflection methods, the debugger will help you understand how everything gets put together.

The debugger is perhaps the best tool to understand Rails: use it.

Identify which debugger your app is using. Learn how to use it, and learn some of its commands. If there isn't one installed, spend some time to get Byebug set up.


