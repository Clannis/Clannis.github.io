---
layout: post
title:      "External Code (Gems & Libraries)"
date:       2020-12-06 01:43:26 +0000
permalink:  external_code_gems_and_libraries
---


Throughout my experience following the Flatiron part-time online software engineering curriculum I have learn a heck of a lot. That's for sure. Coming in I knew a little python and a little more C++, but I never knew there was so much involved with making a web application work. The basic structure and functionality of an app is tough enough to learn, but once you get the hang of it, everything seems to just flow from your fingertips. The biggest hurdle to overcome is to know when to stop creating code that already exists. One of the topics I think is lacking in the curriculum is the introduction to useful ruby gems and js libraries. 

I know they talk about it in some of their lessons but I think there needs to be a deeper dive into how to locate those that exist so that you have an idea of what is out there. If you dont know what code is out there, how do you know not to implement it yourself? Ganted; they only have a limited amount of time to inject so much information into your head.

I still dont have a good central place to find open-source code, but I try and take advantage of npmjs.com and rubygems.org when I can. I seem to have the best results when just "google-ing" and following other peoples issues on stackoverflow.com. This isn't the best method, but so far it has worked for me. The biggest hurdle for me to overcome was to know to look in the first place.

When I run into a problem implimenting some code I now think to search the web to see if someone has already solved my perdicament. 10 out of 10 times I find that I'm not alone, and maybe 9 out of 10 times I find an answer as either code written by someone else or through the use of a gem or library. 

To give an example, I was having an issue on my final React/Redux project where my redux store would be wiped if I went to an external page and then used the browsers back function to get back to my page. My page outline would load, but there would be no "meat" to the page. 

I first thought I was doing something wrong and tried to see if I could fix the issue. After about 10 minutes of thinking of a few ways and about 20 minutes of coding, I couldn't fix my issue. This is when I turned to my good friend "The Internet". After some "google-ing" I found a js library "redux-persist". The implimentation of it was rather confusing, but after sitting down and really going through the docs I learned out to set everything up. 

First off, there are a ton of things to import. 

```js
import { persistStore, persistReducer } from 'redux-persist';
import storage from 'redux-persist/lib/storage';
import autoMergeLevel2 from 'redux-persist/lib/stateReconciler/autoMergeLevel2';
import { PersistGate } from 'redux-persist/lib/integration/react';
```
The persistReducer is the first on the list. 

```js
const persistConfig = {
  key: 'root',
  storage: storage,
  stateReconciler: autoMergeLevel2 
}

const pReducer = persistReducer(persistConfig, articlesReducer);
```
You first create a config object that is required to have the keys "key" and "storage". These two keys and values i just pulled over from the docs. I also opted for one of the extra optional keys: "sateReconciler" to specify that I want 2 levels deep in my state to be persisted or "merged". Since my state contains an array of objects I needed more than one level deep to be merged. If you dont need to merge 2 levels deep you can omit the stateReconciler key as the default stateReconciler is set to autoMergeLevel1 which will merge your state exactly one level deep. 

Next you have to pass both the config object and your root reducer for you app into the persistReducer() method. This will return an enhanced recuder.

```js
let store = createStore(pReducer, composeWithDevTools(applyMiddleware(thunk)))
let persistor = persistStore(store)
```
Next, you'll want to go ahead and create your redux store like normal but pass in the new enhanced reducer and any other middleware you want to use. Following that, you now have to pass that store into the persistStore() method to persist the store. 

```js
ReactDOM.render(
  <React.StrictMode>
    <Provider store={store}>
      <Router>
        <PersistGate persistor={persistor} loading={<Loading/>}>
          <App />
        </PersistGate>
      </Router>
    </Provider>
  </React.StrictMode>,
  document.getElementById('root')
);
```
Finally, you need to wrap your root component with PersistGate and pass in your persisted store as persistor. You can also pass in a component to the loading prop to display while the persisted store is being loaded as PersistGate will delay the loading of the UI until the store is fully loaded. If you dont want to pass in anything for the loading prop it can be left out entirely. 








I first thought I was doing something wrong and tried to see if I could fix the issue. After about 10 minutes of thinking of a few ways and about 20 minutes of coding, I couldn't fix my issue. This is when I turned to my good friend "The Internet". After some "google-ing" I found a js library "redux-persist". The implimentation of it was rather confusing, but after sitting down and really going through the docs I learned out to set everything up. 

First off, there are a ton of things to import. 

```js
import { persistStore, persistReducer } from 'redux-persist';
import storage from 'redux-persist/lib/storage';
import autoMergeLevel2 from 'redux-persist/lib/stateReconciler/autoMergeLevel2';
import { PersistGate } from 'redux-persist/lib/integration/react';
```
The persistReducer is the first on the list. 

```js
const persistConfig = {
  key: 'root',
  storage: storage,
  stateReconciler: autoMergeLevel2 
}

const pReducer = persistReducer(persistConfig, articlesReducer);
```
You first create a config object that is required to have the keys "key" and "storage". These two keys and values i just pulled over from the docs. I also opted for one of the extra optional keys: "sateReconciler" to specify that I want 2 levels deep in my state to be persisted or "merged". Since my state contains an array of objects I needed more than one level deep to be merged. If you dont need to merge 2 levels deep you can omit the stateReconciler key as the default stateReconciler is set to autoMergeLevel1 which will merge your state exactly one level deep. 

Next you have to pass both the config object and your root reducer for you app into the persistReducer() method. This will return an enhanced recuder.

```js
let store = createStore(pReducer, composeWithDevTools(applyMiddleware(thunk)))
let persistor = persistStore(store)
```
Next, you'll want to go ahead and create your redux store like normal but pass in the new enhanced reducer and any other middleware you want to use. Following that, you now have to pass that store into the persistStore() method to persist the store. 

```js
ReactDOM.render(
  <React.StrictMode>
    <Provider store={store}>
      <Router>
        <PersistGate persistor={persistor} loading={<Loading/>}>
          <App />
        </PersistGate>
      </Router>
    </Provider>
  </React.StrictMode>,
  document.getElementById('root')
);
```
Finally, you need to wrap your root component, if using react, with PersistGate and pass in your persisted store as persistor. You can also pass in a component to the loading prop to display while the persisted store is being loaded as PersistGate will delay the loading of the UI until the store is fully loaded. If you dont want to pass in anything for the loading prop it can be left out entirely. 







