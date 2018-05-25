---
layout: post
title:      "Helpful Tricks to Implement AJAX features into a Rails App "
date:       2018-05-25 17:43:16 +0000
permalink:  helpful_tricks_to_implement_ajax_features_into_a_rails_app
---



When adding AJAX features into my Rails app, I came across a few obstacles which led me to find valuable solutions, which I share below. These tips are under the assumption that you're using the active_model_serializer gem, you have generated serializer files, and you have modified the appropriate actions in your controllers to include "render json:...", so that you have places available to render the serialized data. 

One obstacle I came across was when implementing the feature of posting and displaying a review of a post with AJAX. I wanted the review to say "<username> says ...", not "<user_id> says ...", because it would be pretty weird to see "1 says great post!"  I realized you can't call an active record method to query the database such as "u= User.find(1)"  and "u.username" from within the javascript code, so I needed a way to make that information already available in the place which I'm calling the data from for the AJAX request (which is the serializer). 

Solution -If you want an attribute that  you feel you can't access from within the JS code, you can make a method for it in the serializer page, and add it as an attribute to the serializer. I made the following method in the review's serializer page: 
def username
u=User.find(object.user_id)
u.username 
end 

*Note: The object.userid comes from the serializer's access to the instance of the review being created, and, as you can see if you place a binding.pry in the method in the serializer, and check the value of self, you'll see it has an @object method, which has an attribute of userid. *

Now from within the AJAX call I could call data["username"]. (data being the data returned from the AJAX call- the data on the .json route). Always remember that the power of data is in your hands; you can always manipulate the data to provide what you need. 

To Be Continued... 
