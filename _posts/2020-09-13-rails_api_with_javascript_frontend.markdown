---
layout: post
title:      "Rails API with JavaScript Frontend"
date:       2020-09-13 17:13:36 +0000
permalink:  rails_api_with_javascript_frontend
---


Render JSON from a Rails controller
To render JSON from a Rails controller, I specified json: followed by data that can be converted to valid JSON. In my project I used Fast JSON. Also, I added  JSON Viewer Chrome extension. This makes JSON data much easier to read.
-	First, I installed gem fast_jsonapi and run bundle install 
-	This provides access to a new generator, serializer that create Serilizer classes : rails g serializer <your_resource_name>
-	I have 3 models and I added 3 serializers. 
-	With fast JSON API serializers I had to specify what attributes I want to include.
-	With these serializers, I could start to define information about each model and their related models I want to share in my API.
In my app relationships aree that country has_many beaches: and beach belongs_to country.
In BeachSerializer that relationship is represented by adding country to beach attributes. With belongs_to relationship that is possible.
```
class BeachSerializer
  include FastJsonapi::ObjectSerializer
   attributes :name, :location, :description, :image_url, :country_id, :user_id,  :country  
end
```

```
class Api::V1::BeachesController < ApplicationController

    def index
        beaches = Beach.all 
        render json: BeachSerializer.new(beaches) 
    end
end
```
By using fast JSON my data are represented on folowing way:

{
  "data": [
    {
      "id": "1",
      "type": "beach",
      "attributes": {
        "name": "Kassiopi",
        "location": "Corfu",
        "description": "This relatively remote but beloved beach is ideal for those who love diving from the rocks in a pool-like sea.",
        "image_url": "https://iltesorivillas.com/wp-content/uploads/2017/12/rsz_il_tesori_villas_kerkyra-2.jpg",
        "country_id": 1,
        "user_id": 1,
        "country": {
          "id": 1,
          "name": "Greece",
          "created_at": "2020-09-10T18:46:56.607Z",
          "updated_at": "2020-09-10T18:46:56.607Z"
        }
      }
    }
		
I implemented fast JSON because I think that this way of representing data and relationships between models are very readable. I am shue that in my future projects I will continue to use it.
		

