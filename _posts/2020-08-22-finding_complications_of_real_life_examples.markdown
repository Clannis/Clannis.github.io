---
layout: post
title:      "Finding Complications of Real Life Examples"
date:       2020-08-22 23:06:34 -0400
permalink:  finding_complications_of_real_life_examples
---

## RoR Portfolio Project

For my Ruby on Rails Portfolio Project I decided to create a web app that allowed users to create an object for their dogs and sign up those dogs into a training session. At first this sounded so simple, but the more I got inot the associations between objects the more complicated this became. In real life, it is easy to associate a dog with a training class and all that comes with: instructor, time, location, tricks to be learned. Through Active Record there are a lot more items to keep straight. 

A user can have many dogs that can have many training sessions that belongs to a trainer and course but must be unique to its start time and trainer and that course has many tricks. That sounds complicated on its own, but **IT GETS WORSE**. A user isn't the only login-able object. Trainers, as you may think, can log in and use CRUD commands on courses, training sessions, and tricks. They are the admin user. To differentiate the admin user I could have added a boolean admin attribute to the users object, which would make login so much easier, but in this scenario a trainer doesnt have any dogs or a dog doesnt belong to a trainer. 

So, when a user or trainer logs in I have to set the session id to either a trainer_id or user_id and depending on the existance of one or the other allows the existance of links and buttons for CRUD commands to certain objects. A user cant edit courses and trainers cant edit dogs. This logic seems rather simple but most of it is done for the view itself (showing or not showing links on pages that both types of users have access to). 

This basically equates to creating double the views, but in order to follow RESTful routing conventions, it meant that I had to make many helper methods depending on what logic was required. With refactoring I was able to standardize some of the logic and minimize the number of helper methods needed. It didn't make sence to create a helper method to remove logic from the a view to be only used once in the entire application. If that were the case I dont see the need to move the logic outside of the view. It only succeeds in complicating the flow of the information. 

These complications came from just producing a fuctional application. There were more that were produced from following the extra requirements of the project. In order to add nested routing many links needed to be changed. But these links are already under logic depending on who was logged in. Now I have to add logic to change link routing depending on who is logged in or the existance of what objects exist and are related to the object that is logged in. As you can see, we are getting into multiple nested logic statements. The number of possiblities is exponentially increasing and each posibility needed to be accounted. 

After completing all of the requirements and having the application fully functional the only thing that was left was to make it look pretty. **Enter CSS**. Well, I would like to say that but I ran out of time to put in a lot of CSS before the project deadline. Luckily CSS is not one of the projects requirements. I will however come back at a later time and spruce up the visuals so that using this project for my portofolio is more apealing to those demo-ing it. All-in-all I am very happy with the outcome. I feel that I have gained a great appreciation for some of the web applications I have used throughout my time online. There is way more work that goes into a simple looking web app than I originally had throught.
