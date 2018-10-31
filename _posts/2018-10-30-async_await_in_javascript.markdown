---
layout: post
title:      "Async/ Await in Javascript "
date:       2018-10-31 03:14:40 +0000
permalink:  async_await_in_javascript
---

You've probably used callbacks and promises, but have never tried the new asyncronous function in Javascript. 

Async/Await is a language feature that is a part of the ES7 standard. It was implemented in version 7.6 of NodeJs. It is the next step in the evolution of handling asynchronous operations in JavaScript. It gives you two new keywords to use in your code: “async” and “await”. Async is for declaring that a function will handle asynchronous operations and await is used to declare that we want to “await” the result of an asynchronous operation inside a function that has the async keyword.

A function call can only have the await keyword if the function being called is “awaitable”. A function is “awaitable” if it has the async keyword or if it returns a Promise. Callbacks and Promises are not interchangeable and you have to wrap a callback based function inside a Promise and return that Promise. Functions with the async keyword are interchangeable with functions that returns Promises which is why I stated that a function that returns a Promise is “awaitable”.

This makes async actions with multiple steps much neater to write than callbacks or promises. 
