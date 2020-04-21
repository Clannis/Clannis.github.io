---
layout: post
title:      "First Project Hurdles"
date:       2020-04-21 23:03:47 +0000
permalink:  first_project_hurdles
---


Working through the CLI Gem project, to me, wasn't all that difficult. At least on the coding aspect. I came into the project with a firm idea of how I was going to collect and display the data; however, the more I built on the program the more my plan seemed to change. I never physically wrote down/typed out an outline to work through and come up with possible problems down the line. I just jumped into coding with both feet, since that is what I enjoy doing (the actual coding). Don't get me wrong, I came out with a decent program, but had I taken the time to go over exatly what data I was working with and created an outline, I wouldnt have spent so much time and struggle refactoring my code again and again as I came up with new ideas on how to manipulate the data. I'm definetly going to take this as a learning experience and change the way I approach programing. I have always been the kind of person who jumped in head first and it has worked out great for me up until now. I'm not saying it didn't work for me this time, but I would have saved myself such a large headache and time.

Going on with that. If I would have reseached how the API I was using was going to provide access to the data more thoroughly, I probably would have selected another data source. 

I was looking to display characters that appeared in a movie and the only data that held this information in any fashion was a hash of character quotes. This quote hash held what the quote was, who said it, and in which movie it was said. So the only way to provide a character to movie relationship was through the quote. This itself meant that I had to pull every quote, movie, and character from the API before I could sift through them and determine which movie had which character and vice versa. This bogged down my aplication uneccessarily in my opinion, but this is the only way that i could provide the functionality that my application required.

Another issue was the inconstancy with the data provided. Most of the data was there but there was a big portion that either came in as "", " ", nil, or something else. Trying to catch these inconsistancies was horrible. It took me days to realize that since I was using mass assignment to set my object variables that some of the data pulled from the API didnt have the data I was looking for at all. I provide a URL to find more information about a character if the user wishes, but since not all of the data points contained this information, I had to individually create the data within each obect manually if it didnt come in from the API. 

In the end the biggest learning experience for me was to PLAN PLAN PLAN!!!!
