---
layout: post
title:      "Alternative to Deleting Database Entry"
date:       2018-10-16 23:05:39 -0400
permalink:  alternative_to_deleting_an_entry_in_a_database
---



It might seem natural to want an option that allows for deletion of an entry in a database. For example if you had a blog app, and a user wanted to delete their post, you might think to allow deletion of the entry from the database. This can cause problems though. One problem might be if you had a “next” button that redirects the user to the next pose, that next entry in the database would be missing. Another is if a user tries to go to, for example, poses/5, it would throw an error if that was deleted. An alternative could be to add a column to the database such as "isDeleted", which would initially be set to false. This could be thought of as a soft delete, as it is switched to true when someone "deletes" it. Queries of the database can later be filtered through this flag. 
