---
layout: post
title:      "Const in Javascript"
date:       2018-11-08 20:46:00 +0000
permalink:  const_in_javascript
---


Const is a new feature that came with ES6. It is used for declaring variables which cannot be reassigned. For example, once you declare const value= [1,2], you cannot reassign value, such as value= 7. However, this does not mean that it is immutable. You are still able to change the value of the array, such as pushing new values into it. Note that this doesn't apply to primitive data types as those are naturally immutable. Const is useful for protecting against accidental reassignment and provides for less unpredictable code. Const, as well as let, are block-scoped, whereas var is not.  
