---
layout: post
title:      "localStorage v. sessionStorage for JWT Tokens"
date:       2020-12-07 02:24:43 +0000
permalink:  localstorage_v_sessionstorage_for_jwt_tokens
---

For my final portfolio project, I used a JS library "redux-persist" to store my redux store into localStorage to enable client side routing to work even after leaving the site. Say you accidentally opened a new page in the existing tab for my website and immediately decided to go hit the back button to return to my site. Without "redux-persist" the page would fail to load. With all the info stored into localStorage, the page would always load without problem.

I also used localStorage to store a JWT token client side for user login and verification. When storing the token into localStorage, the browser will remember the users authentification signature. It can then retrieve it and send it to the server when a command requires user authentication on the server. This also works on the frontend to restrict certain page access unless a token is stored into localStorage.

The difference between localStorage and sessionStorage subtle but distinct. localStorage will hold onto whatever information you put into it until it is deleted. Say you log into a site and store the client side authentification (JWT Token) into localStorage; even if you close your tab or browser, you will remain logged in when you visit the site again because the browser remembered you. However, if you store the client side user authentication into sessionStorage, the browser will wipe that information anytime the tab or browser is closed.

This difference allows you for more control and security when used for user authentication. If you have a "remember me" check box on your log in form, you can tell the program to store the user authentication into localStorage when checked to keep the user logged in even if they leave your site, or if the user leaves it unchecked, you can tell the program to store the user authentication into sessionStorage to automatically log the user out when they leave your site.

The only caveat to using both storage locations is that whenever your program calls for the data it has to look in two locations. For my project I utilized the following code snippets to accomplish this:

Set user token to localStorage or sessionStorage depending if user wants to be remembered
```js
action.rememberMe ? localStorage.token = action.token : sessionStorage.token = action.token
```

Look for user token in both locations

```js
let userToken = ""
 if (localStorage.token) {
     userToken = localStorage.token
 } else {
     userToken = sessionStorage.token
 }
```

With the above code the user can log out on leaving the site or remain logged in and perform all functions they want without any difference in user experience.
