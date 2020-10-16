---
layout: post
title:      "JS Free For All"
date:       2020-10-13 15:34:01 -0400
permalink:  js_free_for_all
---


After spending months on months of learning the MVC separation of concerns file structure for RoR, jumping into JS and seeing a lack of convention seems absolutely absurd. For the backend portion of my project, I have a plethora of files organized in another plethora of folders and sub folders. For the JS frontend portion of my project, I have a total of seven (7) files in two (2) folders. The main bulk of the front end is strictly isolated to one index.js file. This one file controls all of my DOM manipulation and only talks to the other class files and adapter (fetch calls) files sparingly. The index.js file has 591 lines of code that makes it difficult to locate any specific block of code. Fortunately, I am the only person working on this code so I am fairly familiar with how the code runs and roughly where code is. If any other person were to look at this code, I am fairly certain that they would have some difficulty following the work flow or locating the code that they want to. There should be a formalized structure to the framework to organize code and separate certain responsibilities to separate files. I am hoping that the next section of the curriculum will help to rectify this concern of mine. 

Another issue I have found is the super repetitive nature of JS. The bulk of the DOM manipulation code is structured as: 

1. Create/Grab DOM element
2. Add class or id for CSS
3. Add/Manipulate inner Text/HTML
4. Change CSS or append new Element

This is repeated over and over through my code. I feel there should be some of the “Rails Magic” introduced to this to lessen the amount of code to write. I think there should be some sort of built in function where you can pass in arguments for “type of HTML Element”, “class name(s)”, “element content”, and “parent node”. 

```
newElement = document.addElement("elementType", "class names", "innerInfo", parentNode)
```

This presumably one line of code could cut the amount of code needed by 75%, thereby streamlining the creation process. Maybe React or other frameworks that are out there will do this. I guess I will find out come our next Module.
