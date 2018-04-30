---
layout: post
title:      "How to Display Images Uploaded by Users "
date:       2018-04-30 15:00:57 +0000
permalink:  how_to_display_images_uploaded_by_users
---



The process of figuring out how to display the picture that a user uploaded through your form is quite an adventure. Switching from using Sinatra to Rails can be confusing at time when things work differently when you expect them not to, and this post will hopefully clarify things for you. This post will lead you step by step through how to implement this in both Sinatra and Rails. Doing this through Sinatra was relatively easy. Rails, however, is designed in a way in which it takes care of a lot of things for you, through using their built-in helper methods, specifically the form helper method here. I also couldn't much documentation at all on how to implement the process using Rails. Of course there's the paperclip gem for rails that is very popular, but if you're like me and like knowing the logic in what you're doing, and not jump to using gems to think for you, keep reading!

Even if you’re only interested in the Rails section, read through the Sinatra section as they share most things in common and things won’t be repeated in the Rails section. The Rails section will simply outline the additional things to look out for with Rails.

**Sinatra **

Using Sinatra, when your form is built with the standard html <form> tag,  displaying the images is relatively simple to implement. Create a column in your database imgration with the name pic and the datatype as varbinary. 
 In your form you must include this within the <form> tag:

accept="image/*" enctype="multipart/form-data"

And you must include an input tag with the type= file such as :

<input type="file" name="pic" >

Put in a binding.pry in your controller’s post action to check what params[:pic] is. Following the example of giving the name attribute of “pic”, params[:pic] would come out as an object that looks something like this:

{"filename"=>
"beige-bedrooms-french-inspiration-pictures-for-bedroom-family-in-feng-shui-over-bed-wall-uk-frames-walls-childrens-best-modern-ideas-master-clipart-decorating-above-water-picture-f.jpg",
"type"=>"image/jpeg",
"name"=>"pic",
"tempfile"=>#<File:/tmp/RackMultipart20180429-5161-1tdwrj0.jpg>,
"head"=>
"Content-Disposition: form-data; name=\"pic\"; filename=\"beige-bedrooms-french-inspiration-pictures-for-bedroom-family-in-feng-shui-over-bed-wall-uk-frames-walls-childrens-best-modern-ideas-master-clipart-decorating-above-water-picture-f.jpg\"\r\nContent-Type: image/jpeg\r\n"}

Your first instinct might be to save @<your model here>.pic as params[:pic], which could work, although there is a much easier way. If you save an object as an attribute of a model from the controller, you will notice it saves as a string and not the object which has attributes that can be called. This means you will not be able to call @room.pic.filename the way that params[:pic][:filename] retrieves the value of the filename key in the controller...
(Using the example of a room), if you go and check with pry what @room.pic is in the view, you see one big string of all the object keys and values squashed together.

Note: There is an easier way which is described below, this is just explained for you to understand what’s going on. The complex way is described first

{\"filename\"=>\"beige-bedrooms-french-inspiration-pictures-for-bedroom-family-in-feng-shui-over-bed-wall-uk-frames-walls-childrens-best-modern-ideas-master-clipart-decorating-above-water-picture-f.jpg\", \"type\"=>\"image/jpeg\", \"name\"=>\"pic\", \"tempfile\"=>#<Tempfile:/tmp/RackMultipart20180429-5161-1tdwrj0.jpg>, \"head\"=>\"Content-Disposition: form-data; name=\\\"pic\\\"; filename=\\\"beige-bedrooms-french-inspiration-pictures-for-bedroom-family-in-feng-shui-over-bed-wall-uk-frames-walls-childrens-best-modern-ideas-master-clipart-decorating-above-water-picture-f.jpg\\\"\\r\\nContent-Type: image/jpeg\\r\\n\"}"

In the controller, in the post route of the form, you must save the file to your public folder with:

@filename = params[:pic][:filename]
file = params[:pic][:tempfile]
File.open("./public/#{@filename}", 'wb') do |f|
f.write(file.read)
end

Now you should see the photos in your public folder, and the last step is to go to the view where you want them displayed and put an <img> tag with the src equal to the path of the photo. This is where it gets tricky, if you follow the method above of saving params[:pic] into your model. You would need to using the .split method to get the filename, take the first element of that array, and then use a string slicing method such as [14…-2] to get only the characters you want.
<img src="../../../public/<%=@room.pic.split(",")[0][14..-2]%>">


The simple way is to save overwrite the regular pattern of saving params[:pic] to @room.pic and to set @room.pic = params[:pic][:filename] . This way, the actual filename will be accessible from the view through @room.pic, and you won’t have to do the complicated string manipulations. You might be tempted at first to create an new instance variable such as @filename and set that equal to params[:pic][:filename] ;however, that will not work as you are defining it in the post route of the controller and for something to be visible in the view it needs to be defined in the route that matches the view.
You would implement the code above for saving the images to the public folder, then in the view you would simply put:

<img src="../../../public/<%=@room.pic%>">

**The difference with Rails**

Using the form_for rails helper, following the room example, you would do:

<%=form_for @room, html: {multipart: true} do |t|%>

And you would include this as the input for the form:

<input type="file" name="room[pic]" accept="image/png,image/gif,image/jpeg" >

(Notice that you want to name pic as a nested attribute of oom in the params, so the strong params will work.)

The difference that the Rails form helper causes is that params[:pic] is now a special Rails object called ActionDispatch::HTTP::UploadedFile. It has attributes of tempfile, original_filename, and some others, just like the object with Sinatra does, however the difference is that you can no longer follow the first method above, because if you save params[:pic] as room.pic and you check the value of room.pic in the view, you will only see the “ActionDispatch::HTTP::UploadedFile” as a STRING but without the attributes anywhere. You must follow the second way and do:

@room.pic= params[:pic].original_filename

Note that if you’re using strong params, @room.pic will automatically be saved as params[:pic], but you must overwrite that by adding an additional line, such as:

@room= current_user.rooms.new(room_params)
@room.pic= params[:room][:pic].original_filename

(Notice how in Sinatra [:filename] could be called like that but in Rails it must be called as .original_filename)
You must follow the same method of saving the file to the public folder, and you can view the image in the view with:

<img src="../../../public/<%=@room.pic%>">


