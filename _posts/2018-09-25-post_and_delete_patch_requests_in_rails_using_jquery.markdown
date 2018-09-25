---
layout: post
title:      " Post (and delete/patch) requests in Rails using jquery"
date:       2018-09-25 21:33:53 +0000
permalink:  post_and_delete_patch_requests_in_rails_using_jquery
---


In the last post we talked about how to include authenticity tokens for HTML forms within a Rails app. Now we will talk about how to include authenticity tokens with sending a manual post request. (This also applied to delete and patch requests.) In Rails, just like our forms needed an authenticity token, so do our manual post requests. We will cover an example using jquery.

var token = $('meta[name="csrf-token"]').attr('content'); 

You will want to define a token, as defined above. And then refer to the token in the delete request.
  
	
	$.ajax({
	    url: `http://localhost:3000/poses/${DI2}`,
	    type: 'post',
	    beforeSend: function (xhr) {
	        xhr.setRequestHeader('X-CSRF-Token', token)
	    },
	    data: {},
	    contentType: false,
	    processData: false
	});

