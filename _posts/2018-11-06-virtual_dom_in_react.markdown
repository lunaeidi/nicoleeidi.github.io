---
layout: post
title:      "Virtual DOM in React"
date:       2018-11-07 03:59:46 +0000
permalink:  virtual_dom_in_react
---


Manipulating the DOM is slow, especially with huge amounts of DOM manipulation in modern websites. For example we had a list of 100 items, and we changed the value of one of the items. Using vanilla JS, the entire list would be rebuilt even if only one item was changed. 

React's concept of the virtual DOM fixes this issue. For every DOM object, there is a virtual DOM object, which can be thought of as a lightweight copy. Manipulating the virtual DOM is much faster than the DOM because nothings gets drawn on the screen. Once the virtual DOM is modified, React compares the updated virtual DOM with a snapshot it took of the virtual DOM right before the update. React deduces exactly which virtual DOM objects have changed and it only updates those objects on the real DOM. Using React, if you had a list of 100 items and changed one item, only that one item would get rebuilt on the DOM. 

