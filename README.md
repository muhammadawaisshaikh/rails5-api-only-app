# STEPS GET DONE

# 1. Creating and Setting Up
rails new ecommerce --api -d postgresql -T

# 2. Setting API subdomain in routes.rb
Rails.application.routes.draw do
  constraints subdomain: 'api' do
  end
end

# 3. Creating book model
rails g model Book title:string author:string weight:string publisher:string language:string pages:integer publication_date:datetime

# 4. for create the database
rake db:create

# 5. to create book table
rake db:migrate

# 6. Setting API Versioning
gem 'versionist' in GEMLFILE
RUN rails generate versionist:new_api_version v1 V1 --path=value:v1

# 7. adding api_versioning in namespace under routes.rb
api_version(:module => "V1", :path => {:value => "v1"}) do
end

# 8. for creating routes for books CRUD in routes.rb add:
resources :books

# 9. create the books controller inside version 1
path: app/controllers/v1/books_controller.rb

# 10. OPEN rails c
RUN Book.create(title: "Atlas Shrugged", author: "Ayn Rand", weight: "3.4 pounds", publisher: "Dutton", language: "English", pages: 1168, publication_date: "April 21, 2005")

# 11. Now just start your rails server and go to your postman and 
GET http://api.localhost:3000/v1/books

# 12. Creating the others actions (Create, Show, PUT/Patch, Delete)
mentioned in app/controllers/v1/books_controller.rb
