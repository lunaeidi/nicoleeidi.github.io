---
layout: post
title:      "Is your POST HTTP request showing up as OPTIONS? "
date:       2018-10-24 02:59:11 +0000
permalink:  is_your_post_http_request_showing_up_as_options
---


The other day I tried to send a POST request to my Node.js API to test out my application and see if a new user would get created properly and stored in the database, and when I was surprised to see that it was being sent as OPTIONS and getting no response.  

It turned out this was something called a "preflighted" request implemented by CORS. CORS first sends an HTTP request by the OPTIONS method to the resource on the other domain in order to determine whether the actual request is safe to send. Cross-site requests are preflighted like this. A request is preflighted if any of the following conditions is true:

1) If it uses any of the following methods: put, delete, connect, options, trace, path
2) If apart from the headers set automatically by the user agent (for example, Connection, User-Agent, or any of the other header with a name defined in the Fetch spec as a "forbidden header name"), the request includes any headers other than those which the Fetch spec defines as being a "CORS-safelisted request-header".
3) If the content-type header has a value other than the following: application/x-www-form-urlencoded, multipart/form-data, text/plain

4) If one or more event listeners are registered on an XMLHTTPRequestUpload object used in the request. 
5) If a ReadableStream object is used in the request. 

In the next post we'll talk about how to make our requests CORS simple requests to prevent this issue from happening. 

