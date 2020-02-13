---
layout: post
title:      "'Sinatra Portfolio Project - Colouring Gallery App'"
date:       2020-02-13 18:50:21 +0000
permalink:  sinatra_portfolio_project_-_colouring_gallery_app
---


For my Sinatra portfolio project, I decided to create Colouring Gallery App, application for fans of adult colouring books (I’m among them). Inspiration for logic how to create my project I found in videos Sinatra Live Build Journal App by Howard De Vennish (can be found on https://instruction.learn.co/student/video_lectures#/). 

In Colouring Gallery App, a user can sign up, login, logout, create new picture, and edit and delete pictures they own.

To built application I followed next steps:
-	Used ActiveRecord for storing information in a database
-	Included two model classes: User and Picture
-	Included has_many relationship on my User model: User has_many Pictures
-	Included belongs_to relationship on Picture model: Picture belongs_to User
-	Included user accounts with unique login attribute: email
-	Ensured that the belongs_to resource has routes for Creating, Reading, Updating and Destroying: User has full CRUD on Pictures
-	Ensured that users can't modify content created by other users: by using helper method in controller to ensure edit and delete actions can only happen if current user owns the picture
-	Included user input validations: that user can't create a blank user or picture 
-	Displayed validation failures to user with error message using sinatra-flash to show flash messages.
-	Used CSS to style.

My 'favourite' method that I learned in Sinatra part of curriculum is # authenticate. Purpose of authenticate method is to validate password match. Method is added  by ActiveRecord and called on User model with following  line of code:
```
class User < ActiveRecord::Base
  has_secure_password
end
```
With has_secure_password Ruby adds an authenticate method to my class when the program runs.
Authenticate method was used in my project in post “/login” route.

```
post "/login" do
    @user = User.find_by(email: params[:email])
    if @user && @user.authenticate(params[:password])
       session[:user_id] = @user.id
       flash[:message] = "Welcome, #{@user.name}!"
       redirect "users/#{@user.id}" 
    else
       flash[:errors] = "Your credentials were invalid. Please sign up or try again."
       redirect "/login"
    end
end
```
Authenticate method works by taking a user’s input for password as an argument and turning the password into a salted, hashed version. After that compares this salted, hashed version with the user's stored salted, hashed password (password_digest) in the database. If the two versions match, #authenticate will return the User instance; if not, it returns false. 
If the User is authenticated, session[:user_id] will be set and post "/login" route will be redirected to the "users/#{@user.id}"  route, otherwise, will be redirect again to the beginning of /"login" route.


