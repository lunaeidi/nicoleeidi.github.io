---
layout: post
title:      "How to create "next post" feature with AJAX in Rails "
date:       2018-09-11 21:22:26 +0000
permalink:  how_to_create_next_post_feature_with_ajax_in_rails
---


In your blog-style app, if you'd like to create a "next post" button that loads the next post's details onto the page all without a page refresh, keep reading. We're going to make use of HTML's data-* attribute, which we'll use to keep track of which post we're on. We'll also be using jquery's .attr() method.

Give your "next post" link a data-id attribute, and set that equal to the current post's id. 

Note: the below example code in the show view page, and @post had been defined in the controller's show action to be @post=Post.find(params[:id])

<a href="#" class="js-next" data-id="<%=@post.id%>">Next Post</a>

Next, we'll create a nextId variable by adding 1 to the current data-id, so that we have something with which to call the proper data. This is assuming we have created the .json routes and our serializers. 

let nextId= parseInt($(".js-next").attr("data-id")) + 1 

Inside the get request is where we'll replace the current content on the page with the data returned back to us from the request. We'll also need to replace our data-id attribute of our "Next Post" link so the cycle can continue. Here's an example: 

$.getJSON("/posts/" + nextId + ".json", function(data){
$(".postContent").text(data["content"])
$(".js-next").attr("data-id", data["id"]);
})



