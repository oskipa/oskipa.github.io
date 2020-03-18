title: Interface > Manual > Code Docs > Code
subtitle: Improve your software by finding where user consult lower levels of abstraction 
category: log
tags: software engineering, documentation  
date: 2020-03-18
Status: draft

1. Levels of abstraction
2. Droping to a lower level of abstraction means that the higher one's can be improved
3. Cars as a model of good implementation of abstraction
4. Software compared to cars

## Another entry
user manual vs documentation

Always have a -h or --help
Explain what it does, show the template and show an example 

 


This post is about software. It is about how to find spots for improving your software interfaces. 

However, I want to talk about cars first because I think it is a model of successful user interface design and documentation.

The user interface for driving a car is well known. You sit behind the weel. You check visibility on your windshield.  You check the mirrors. You release the emergency break. You start the car. You get into the right gear. You use the weel to turn and the pedels to accelerate, break, or shift gears. You have some indicators like speedometer to tell you how fast you go and the fuel tank indicator to let you know when you need to refuel.

It is a common interface, so you can usually hop into any car and drive it. There are some complicated vehicles, like trailer trucks who need a more complex system, but the conventions are about the same.

If there is something that you can't figure out, you reach for the user manual. Let's say you got in a new car, and you can't find how to turnthe emergency lights on. You open the user manual, and find out that it is the yellow button by the radio.

If you need to replace a light, you can try doing it. If your experience fails and you can't figure out how to do it, you open the repair manual. You will open the hood and try to fix it. In extreme cases you need to look at the diagrams on how the car is put together.

But about 98 to 99 percent of the time, you will sit down and drive. You don't need to do any of the above.

The modern car is a success in user interface design. Over one hundred years we have developed a number of conventions. Once a person learns them, they can quickly adapt moving from one vehicle to another. User manual usually are used as references for learning specifics about the conventions. We consult them when we want to see what grade of oil to use, what the pressure of the tires should be. In some cases user manuals will have how to fix some known issues that have simple work arounds.


Let's get back to software. How can we apply the success of car design to sofware? Let's make a simple chart to illustrate the different levels of abstraction that the driver and our software users interact with.


-------------------------------------------------------------------
|Abstraction            | Car                           | Software|
------------------------------------------------------------------
|User Interface| Steering wheel, pedels | GUI, command line, API |
|User manual   | Owners manual | User guides, tutorials, readmes |
|Documentation | Repair manual | StackOverflow, library docs     |
|Implementation| Opening the hood to check the system| Source code|    

Cars are successful because the user is kept most of the time at the user interface level of abstraction. Learning more about the car is a user's choice. Yes, the ones that learn more about it will get better performance and gas millage. Yet if all what a user wants is go to work and come back, they can do it without having to do research. 

With software we are still in the process of creating many of these conventions. So it can be more jarring moving from one product to another.That said, windowed systems, spreadsheets, and lists, and swiping right or left are emerging conventions.

Dropping down to the user manual points out some kind of failure in the design or implementation. My smartcar will stop working if there are too many keps in the keychain. The car will stop and it won't start again. The user manual tells us to sing "This little sun of mine" to the car to encourage it to start again. After that song, the car will start.

And here is the first opportunity: can you design your software so that the training that people can start using your sofware without training. Figure out what conventions people expect. Stick to those.

If there is a problem and you need to drop to the next level of abstraction,  
 

If people are reading your source code to see why something isn't working, that means that your documentation can improve. 

Just as you should create a test and fix a bug, documentation should be upgraded at this points.
 



