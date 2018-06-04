---
layout: post
title:      "State Management in React vs Redux "
date:       2018-06-04 18:50:56 +0000
permalink:  state_management_in_react_vs_redux
---


When's the best time to use Redux to maintain your application states and when's the best time to leave them in your React components? Both options are possible ; however, I learned what makes the most sense through making my sudoku react app. When new to react, you'll probably want to play around and implement the state features that React comes with. This will show you the types of problems that Redux was built in order to make a lot easier.  

Without having to go through learning redux, there still is a way to pass states between containers, but it quickly becomes very tedious as states will need to be passed between many many containers, and if you change something in one place, you would need to change it in each other place you typed it. This is very prone to errors and a big mess when trying to debug.

A general rule I learned to follow is to stick to using React states for containers in which the state only involves one container,  and to use redux for state management in which the state needs to be accessed by multiple containers.

Using redux, the state is all maintained in just one place, and makes debugging a very easy process. 
