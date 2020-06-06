---
layout: post
title:      "'Rails Project - Chocolate Fans App'"
date:       2020-06-06 13:03:43 +0000
permalink:  rails_project_-_chocolate_fans_app
---




For my Rails project I decided to make Chocolate Fans App for all chocolate lovers. In app user can login, login via GitHub, logout. User can create new chocolates and add review for chocolates, as well as edit chocolate and edot review current user created. 
My favorite part that I learned working on rails project is using nested routs.
I chose to make nested review under chocolate.
In routs I added code:

```
 resources :chocolates do
    resources :reviews, only: [:new, :index, :create]
  end
```

In reviews_controller.rb new, create and index action have following code:

```

    def new
        # if it's nested
        if params[:chocolate_id] && @chocolate = Chocolate.find_by_id(params[:chocolate_id])
            @review = @chocolate.reviews.build
				#if not nested
        else
            @review = Review.new
        end
    end

    def create 
        @review = current_user.reviews.build(review_params)
        if @review.save
          redirect_to review_path(@review)
        else
          render :new
        end
    end


    def index
        #how do I chack if nested: chocolates/1/reviews, also chacks if is valid id not just nested
        if  @chocolate = Chocolate.find_by_id(params[:chocolate_id])
				# once we have nesed rout it's not :id it's chocolate_id
            @reviews = @chocolate.reviews
        else
        #if it's not nested: /reviews
            @reviews = Review.all
        end
    end
```
While working on the rails project, I tried a lot of different options in the code and got a lot of errors, just to see what will happen. Yes, it was challenging, but great fun!



