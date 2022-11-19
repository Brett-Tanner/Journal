# November 2022

## Tues 1st
### Odin Project - Ruby on Rails - Private Events Project
#### What I did
- [] Style it all 
  - [x] Site-wide stuff
  - [x] Homepage
    - [x] Event partials
  - [x] Forms
    - [x] style Devise forms
    - [x] style new event form by making the classes/layout same as Devise forms
  - [] Event pages
  - [] User profiles
    - [] User partials
- [] and host so I can show Viktoria


#### What I learned
- Outline is the one you wanna override to cancel the border/outline on selected input fields in forms


## Wed 2nd
### Odin Project - Ruby on Rails - Private Events Project
#### What I did
- [] Style it all 
  - [x] Forms
    - [x] style Devise forms
    - [x] style new event form by making the classes/layout same as Devise forms
  - [] Event pages
  - [] User profiles
    - [] User partials
- [] and host so I can show Viktoria


#### What I learned
- need turbo_confirm in data hash, not just confirm, to display a popup

## Thurs 3rd
### Odin Project - Ruby on Rails - Private Events Project
#### What I did
- [x] Style it all 
  - [x] Event pages
  - [x] User profiles
    - [x] User partials
  - [x] Notices
- [x] and host so I can show Viktoria


#### What I learned
- I needed to remove the anchor element around the event details on the show page so people can select the text
  - so needed to render something slightly different in the event partial for Event#show compared to Event#index where it's in tiles that are links
  - You can set "name: true" as an option on render calls, then use "if local_assigns[ :name ]" to render a given chunk of html if called by a render with that option set
- Should specify "--database=postgresql" in future so there are less issues when hosting


## Fri 4th
### Odin Project - Ruby on Rails - [Active Record Callbacks](https://www.theodinproject.com/lessons/ruby-on-rails-active-record-callbacks)
Callbacks allow you to execute code every time an AR object is created/modified/destroyed etc.

- AR Object Life Cycle
  -  **Initialization -** When first built or when loaded into memory from the db
  -  **Validation -** When AR checks if the object is valid
  -  **Saving -** Any time the object is saved, not just on first creation
  -  **Creating -** When it is created and saved for the first time
  -  **Updating** 
  -  **Finding -** Querying existing objects (like #find, #all)

- Creating callbacks
  - You create a callback in the form "before/after/around"_"life cycle stage"
  - before and after are obvious, but around means you write code that yields to the original action at some point, then continues after. Not especially common.
  - [Full list of available callbacks here](https://guides.rubyonrails.org/active_record_callbacks.html#available-callbacks)

- Using Callbacks
  - You use them by putting a method name (as a symbol) or a block next to "before_action" for example (as above)
  - the actual method you want to call is usually implemented as a private method
  - avoid updating or saving variables in callbacks
  - callbacks work through model relations
    - so an "after_destroy" on an author can display something in the console when each of the author's articles is destroyed

- Specifying Characteristics
  - if you want to restrict it to specific controller actions use the on: option and a single symbol or array of symbols listing the actions you want to use it with
  - you can use the if: and unless: options to conditionally run the callback by passing a condition or method that evaluates to true or false

- Transaction Callbacks
  - Transactions are a bundle of actions that succeed or fail together
  - you can target the success with after_commit and failure with before_rollback
    - those are mostly used when interacting with things that are not part of the database transaction
  - callbacks are wrapped into a transaction with your validations, other callbacks and the db operation to be executed. To deliberately rollback the transaction, use "throw :abort"

- Callback classes
  - Can be declared as instance or class methods on their own callback class
  - then receive the model object as a parameter

- Guidelines for using callbacks
  - Only use if they can be run every time and in every environment the callback is triggered
    - otherwise consider moving to a [decorator](https://samuelmullen.com/2011/12/sending-notifications-using-decorators-instead-of-callbacks/) object
  - Don't create callbacks which do anything other than interact with the db, to do so is to exceed the model's responsibility
  - If you have to stub callbacks during testing (using any_instance for e.g.) then you're violating one of the first two rules
    - Not so much for unit testing tho


## Sat 5th
- Busy ;)


## Sun 6th
### Odin Project - Ruby on Rails - [Advanced Forms](https://www.theodinproject.com/lessons/ruby-on-rails-advanced-forms)
This is gonna be about handling multiple models with a single form, as well as pre-populating dropdown menus.

- Pre-populating dropdown menus
  - Use select_tag and options_for_select
  ```
  <%= select_tag(:author_id, options_for_select(@user_options)) %>
  ```
  - If you don't wanna use two helpers
  ```
  <%= select(:post, :author_id, @user_options) %>
  ```
  - Or if you're creating a new object in form_with
  ```
  <%= f.select(:author_id, @user_options) %>
  ```
  - options_for_select expects an array of arrays; each array should be ["option text", value to be submitted]
    - transform your object collection into arrays of ["name", id] using #map in the controller
    - or just .order(col with option you're selecting).to_a, since the id is included by default
      - then
      ```
      <%= form.collection_select :city_id, City.order(:name), :id, :name %>
      ```
      - same for radio buttons and check boxes

- Nested forms
  1. Prepare your model to know it needs to create an instance of another model if it's given the necessary parameters
    - do this using accepts_nested_attribute_for :association_name on the model
    - which gives a "name"_attributes= method on the model you applied it to
  2. Make sure you allow the nested params in your Strong Param controller method
    - add the name of the nested hash and the params inside it to the params.require
    ```
    params.require(:person).permit(:name, addresses_attributes: [:id, :kind, :street])
    ```
  3. Build the form in the view
    - use fields_for to make a second form_with inside your first e.g.
    ```
    <%= form_with model: @user do |f| %>
      ...
      <% 3.times do %>
        <%= f.fields_for @user.shipping_addresses.build do |sub_form| %>
          ...
          <%= sub_form.text_field :zip_code %>
          ...
        <% end %>
      <% end %>
      <%= f.submit %>
    <% end %>
    ```
    - if you don't use the 3.times line, it'll render the fields_for section once for each address
      - thus if you're creating a new User, you'd wanna build x empty shipping addresses in the controller so the form will automatically create them
      - if the associated object already exists, Rails will auto-generate a hidden field containing the id of that existing object
        - can be disabled with include_id: false option on fields_for
    - when adding fields on the fly you have to use JS, no built in support
      - make sure to use a unique key for each generated hash, current JS date is a common choice

  - can nest the params like name="person[address][city]"
    - if identical params end with empty brackets, they will be accumulated in an array
    - can combine these two concepts as follows to create an array of hashes
    ```
    <input name="person[addresses][][line1]" type="text"/>
    <input name="person[addresses][][line2]" type="text"/>
    <input name="person[addresses][][city]" type="text"/>
    <input name="person[addresses][][line1]" type="text"/>
    <input name="person[addresses][][line2]" type="text"/>
    <input name="person[addresses][][city]" type="text"/>

    ```

  - You can also nest the ability to destroy another object
    - set the option allow_destroy: true on accepts_nested_attribute_for
    - include the key "_destroy: 1" in the submitted params when you wanna delete the object
    - you'll need to include _destroy in your required params

  - For nested forms to work with many to many relationships you'll need to [specify they're inverses of each other](https://thoughtbot.com/blog/accepts-nested-attributes-for-with-has-many-through)

  - To prevent certain fields being blank you can pass a reject_if: proc to accepts_nested_attribute_for
    - will be called with each hash of attributes submitted
    - if it evaluates to true, the object will not be built
    - can pass :all_blank instead to reject submissions where all fields other than any _destroy values are blank 
    - can set the index of multiple hashes from fields_for by using the index: option, e.g. if the record already exists you could set index: Record.id

- [Simple form](https://github.com/heartcombo/simple_form) allows you to use more feature-rich templates for forms

- Blank submissions that delete
  - Sometimes you want a blank checkbox/text field to delete that value rather than not changing it
  - You can do this by creating a hidden field with value="" which ensures that value will be in your params no matter what
  - Then in the controller you set the relevant value to nil if the params value is ""


## Mon 7th
### Odin Project - Ruby on Rails - [Flight Booker](https://www.theodinproject.com/lessons/ruby-on-rails-flight-booker)

#### What I did
- [x] Plan out the db architecture

- [] Screen 1 - Search
  - [x] Create Airport model
    - [x] Use the seeds.rb file to create a bunch of airports
  - [x] Create Flight model
  - [] Set up Flight/Airport associations
    - [] Seed the Flights
  - [] Make the Flights index page the root
  - [] Create a search form on that page which uses a GET request back to the same URL
    - [] Add dropdowns

- [] Screen 2 - Pick a Flight

- [] Screen 3 - Passenger Info

#### What I learned
- You can use db/seeds.rb to fill in dummy data
  - you can also use delete_all as part of the seeds file (only in dev/test) to refresh the data in your db every time you run rails db:seed

- Seems when using pg for your db you need to create the db before migrating it


## Tues 8th
### Odin Project - Ruby on Rails - Flight Booker

#### What I did
Mostly had to study for my training exam at the new job this morning, and too tired tonight to get much done

- [] Screen 1 - Search
  - [] Set up Flight/Airport associations
    - [] Seed the Flights
  - [] Make the Flights index page the root
  - [] Create a search form on that page which uses a GET request back to the same URL
    - [] Add dropdowns

- [] Screen 2 - Pick a Flight

- [] Screen 3 - Passenger Info

#### What I learned
- Figured out that I only need to set a foreign key on the airport model, flights can just refer to the airport id once you set class_name
  - realised that arriving flights are linked to the destination airport, and departing flights are linked to the origin, so used them as the foreign keys
- Struggling to write the migrations for this one, will continue trying in the morning after a good night's sleep
  - Which ones do I need an explicit foreign key for and which can I just add_reference with the foreign key option?
  - I need two separate refs for the origin/destination airports, do I name them differently in the migration or just let the model handle it? If so how

## Wed 9th
### Odin Project - Ruby on Rails - Flight Booker

#### What I did

- [] Screen 1 - Search
  - [x] Set up Flight/Airport associations
    - [x] Seed the Flights
  - [] Make the Flights index page the root
  - [] Create a search form on that page which uses a GET request back to the same URL
    - [] Add dropdowns

- [] Screen 2 - Pick a Flight

- [] Screen 3 - Passenger Info

#### What I learned
- When you manually set the foreign key in a migration, the column option is for the name of the column in the originating table
- db:reset resets the ids so you can have static ones in your seed file


## Thurs 10th
### Odin Project - Ruby on Rails - Flight Booker

#### What I did

- [] Screen 1 - Search
  - [x] Make the Flights index page the root
    - [x] generate corresponding views/controllers
  - [] Create a search form on that page which uses a GET request back to the same URL
    - [] Add dropdowns

- [] Screen 2 - Pick a Flight

- [] Screen 3 - Passenger Info

#### What I learned
- Controllers are named with the plural version


## Fri 11th
### Odin Project - Ruby on Rails - Flight Booker

#### What I did

- [] Screen 1 - Search
  - [] Create a search form on that page which uses a GET request back to the same URL
    - Created the scaffold, but didn't connect it to anything
    - [] Add dropdowns

- [] Screen 2 - Pick a Flight

- [] Screen 3 - Passenger Info

#### What I learned
- Working 9 hour days is annoying

## Sat 12th
### Odin Project - Ruby on Rails - Flight Booker

#### What I did

- [x] Screen 1 - Search
  - [x] Create a search form on that page which uses a GET request back to the same URL
    - [x] Add dropdowns

- [] Screen 2 - Pick a Flight
  - [] Render search results in their own form
    - [] radio button next to each flight that lets them select it
    - [] submits to the #new action of BookingsController using GET
    - [] include hidden field storing the number of passengers

- [] Screen 3 - Passenger Info
  - [] Create Booking model
  - [] Create Passenger model
  - [] Set up associations between Bookings, Passengers and Flights
  - [] Create BookingsController and routes
    - [] Create #new action
      - [] displays currently chosen flight, airports and dates
      - [] fields to enter info for each passenger 
        - so need to create blank passenger object for each
        - use fields_for
    - [] set up #create to create both a new Booking and new Passengers
    - [] render booking's show page after the form is successfully submitted

#### What I learned
- Best way to populate select boxes is
```
form.collection_select :input_id/name, Model.order(), value to submit, value to display in list
```

- If you only want a certain column from your model, you can use ::select(:symbol)
  - can append ::distinct

- You can format the dates in a select box by creating a method on the model you're getting the dates from
  - the method can be named anything you want, but it must act on one of the values you're passing to collection_select
    - e.g. in my case I got a list of departure_time values, so my method was "departure_time.strftime("%d/%m/%Y")"

## Mon 14th
### Odin Project - Ruby on Rails - Flight Booker

#### What I did

- [] Screen 2 - Pick a Flight
  - [] Render search results in their own form
    - [x] radio button next to each flight that lets them select it
    - [] submits to the #new action of BookingsController using GET
    - [x] include hidden field storing the number of passengers

- [] Screen 3 - Passenger Info
  - [x] Create Booking model
  - [x] Create Passenger model
  - [] Set up associations between Bookings, Passengers and Flights
  - [] Create BookingsController and routes
    - [] Create #new action
      - [] displays currently chosen flight, airports and dates
      - [] fields to enter info for each passenger 
        - so need to create blank passenger object for each
        - use fields_for
    - [] set up #create to create both a new Booking and new Passengers
    - [] render booking's show page after the form is successfully submitted

#### What I learned
- You can pass variables through a render call by appending them as symbol options
  - e.g. to pass the "form" variable for a form_with, append "form: form"

- Hidden fields are added with form.hidden_field
  - first argument sets the id and name, you can set the value with the value: option

- My seeds file has not been creating passengers (I think, may have before I added this relation) and is not creating bookings
  - works fine when I create a Booking/Passenger manually in console though

## Tues 15th
### Odin Project - Ruby on Rails - Flight Booker

#### What I did

- [x] Screen 2 - Pick a Flight
  - [x] Render search results in their own form
    - [x] submits to the #new action of BookingsController using GET

- [] Screen 3 - Passenger Info
  - [] Set up associations between Bookings, Passengers and Flights
  - [x] Add the ability to check available seats
  - [] Create BookingsController and routes
    - [] Create #new action
      - [] displays currently chosen flight, airports and dates
      - [] fields to enter info for each passenger 
        - so need to create blank passenger object for each
        - use fields_for
    - [] set up #create to create both a new Booking and new Passengers
    - [] render booking's show page after the form is successfully submitted

#### What I learned
- #create on a model uses () before the array of hashes you dum dum

- You can use sum/count etc. by calling it on a Class or an AR relation (e.g. results of a #where/#order)
  - can pass it a col to work on or just the whole relation/Class

- Create blank passengers in an Array (since you can't increment variable names) then submit their values as an array as well using the passenger[][name]... etc. trick

- Probably need to change the Passenger/Booking association to be has_and_belongs_to_many
  - I don't see how else you can link multiple passengers to a single booking, there's no foreign key for bookings in the passenger table
  - On my first attempt, finding the flights/bookings for a passenger turns up nothing
    - Two initial theories
      - The passenger_id foreign key in Bookings is causing problems (Not this, but it's unnecessary anyway)
      - I need to add something to the has_many flights through bookings now there's a join table in the middle
    - **Tomorrow I'll try editing the migrations to do it this way from the start, then running db:reset**

- To remove an index for a foreign key, you can just remove the foreign key

## Wed 16th
### Odin Project - Ruby on Rails - Flight Booker

#### What I did

- [] Screen 3 - Passenger Info
  - [x] Set up associations between Bookings, Passengers and Flights
  - [] Create BookingsController and routes
    - [x] Create #new action
      - [x] displays currently chosen flight, airports and dates
      - [x] fields to enter info for each passenger 
    - [x] set up #create to create both a new Booking and new Passengers
    - [x] render booking's show page after the form is successfully submitted

#### What I learned
- Figured out why the HABTM relationship wasn't showing anything
  - My seeds file was creating the Booking table with a Passenger_id, but that does nothing with a HABTM model
  - So there was nothing linking the Bookings and Passengers
  - I have to update my seeds file to have the passengers created by a booking

- When you use fields_for and have already generated the new objects you need, it'll automatically create the correct number of fields. No iterating needed

## Thurs 17th
### Odin Project - Ruby on Rails - [APIs](https://www.theodinproject.com/lessons/ruby-on-rails-apis-and-building-your-own)
APIs are two programs communicating with each other, often largely without user input, and exchanging only data rather than HTML and CSS

- You can set up an existing Rails application as an API by making the controller return JSON/XML etc. if the client requests it
  - Client can request a certain format by appending .json or .xml to the URL
  - You do this using #respond_to, which takes a format argument
  - You add formats to be returned with format.json {render :json => @users} or format.xml {render :xml => @users}
    - remember to include format.html
    - the symbol calls #to_json on the object, which calls #as_json to retrieve the values then converts using ActiveSupport::json.encode
  - If you wanna constrict the info returned by your API, modify #as_json on your model
    - You can do this by overriding the model, or extending it with super
    ```
      # app/models/user.rb
    class User < ActiveRecord::Base

      # Option 1: Purely overriding the #as_json method
      def as_json(options={})
        { :name => self.name }  # NOT including the email field
      end

      # Option 2: Working with the default #as_json method
      def as_json(options={})
        super(:only => [:name])
      end

    end

    ```
    - See [#as_json docs](https://api.rubyonrails.org/classes/ActiveModel/Serializers/JSON.html#method-i-as_json) for more details/options

- The head method can be used to return just a header with an error message, for examples "head :not_found"
  - [Custom error pages are also possible](https://web-crunch.com/posts/custom-error-page-ruby-on-rails)

- Existing Devise auth will handle authentication, but since client is likely not a browser you can't use cookies
  - use custom tokens instead

- Service Oriented Architecture
  - Break individual services within your app out into separate applications on separate servers and have them communicate through internal APIs
    - Makes it easy to make major changes within a service, so long as the endpoints are the same
    - Can mix languages
    - Can mix internal and external apps


## Fri 18th
### Odin Project - Ruby on Rails - [External APIs](https://www.theodinproject.com/lessons/ruby-on-rails-working-with-external-apis)
- First steps
  - First you need to register with the API provider
    - will likely have some form of rate limiting before you need to pay
  - They'll give you an API key (fine to expose in your app) and sometimes a secret key (which you need to keep secret using environment variables or a gem like figaro)

- API rates & security tokens
  - There are different types of authorisation required for different requests e.g.
    - Showing tweets might require no authentication, but be heavily rate limited
    - Some other requests for public data will require your API key, and be limited by pricing tiers
    - Things like getting data on a specific user or modifying/deleting stuff will likely require your private key as well for auth
    - When you want to make requests on behalf of a user, you get them to sign in and the API provider sends you a token which you can use to identify the requests as coming from them
      - this puts their requests into a per-user bucket, which can lead to better rates

- OAuth Basics
  1. User tries to access a page on your app and you ask the user to login
  2. User chooses the “Login With Facebook” option
  3. User is redirected to a Facebook page asking them to review the permissions you are asking for and telling them to sign in. The URI will contain parameters that tell Facebook who your application is and possibly which URI they should submit their response to (or maybe you specified this as a part of your API registration process with them).
  4. User decides you seem like a fun application so they’ll allow you to see their email address and post to their timeline. User signs in to their Facebook account. Facebook creates an authorization code and sends it back to your application’s callback URI.
  5. The user waits while your application takes that authorization code and uses it to ask Facebook for the real good stuff. Facebook makes sure your application is the same one the user authorized, then POSTs back to you a unique authentication token for the user (which likely expires in 90 days) and any data you asked for up front (like email address).
  6. You store the user’s unique token in your database and use it, along with your application key(s), to make any subsequent requests on the user’s behalf.

  - In rails we use the [omniauth](https://github.com/omniauth/omniauth) gem for this
  - there are also individual gems which provide [authentication strategies for each major API](https://github.com/omniauth/omniauth/wiki/List-of-Strategies)
    - those are the ones you actually install I think

- SDKs
  - provide all the code necessary to access a company's API, usually in JS
  - makes it easier to access their API with simple JS methods but
  - enforces their conventions for any interaction with it and expands your codebase


#### What I learned
- When you define a method with self.method_name, any method inside it will be called on self
  - that's why the date formatting I was confused about worked, I think



### Odin Project - Ruby on Rails - [Beaver API](https://www.theodinproject.com/lessons/ruby-on-rails-kittens-api)

#### What I did

- HTML
  - [x] Generate Beaver resource
    - [x] Seed the beavers
  - [] Build basic controller methods and views
    - [] Add a "Delete Beaver" button to show/edit pages, as well as each beaver on the index page
  - [] Use flash hash to congratulate successful beaver creation/edits
    - [] Also to make fun of you for errors in the forms (like setting cuteness below 10)

- API
  - [] Install REST client
  - [] Make #index respond_to JSON
  - [] test using IRB
  - [] also make #show respond_to JSON

#### What I learned
- How are update and edit REST actions different again??
  - Edit renders the view, update performs the update
  - Like new/create


## Sat 19th
### Odin Project - Ruby on Rails - [Beaver API](https://www.theodinproject.com/lessons/ruby-on-rails-kittens-api)
#### What I did

- HTML
  - [x] Build basic controller methods and views
    - [x] Add a "Delete Beaver" button to show/edit pages, as well as each beaver on the index page
  - [x] Use flash hash to congratulate successful beaver creation/edits
    - [x] Also to make fun of you for errors in the forms (like setting cuteness below 10)

- API
  - [x] Install REST client
  - [x] Make #index respond_to JSON
  - [x] test using IRB
  - [x] also make #show respond_to JSON


### Odin Project - Ruby on Rails - [Flickr API](https://www.theodinproject.com/lessons/ruby-on-rails-flickr-api)
#### What I did
I'm adding functionality to the previous project rather than following the requirements strictly for this one 

- [x] Register an app with Flickr
- [x] Add a gem for the Flickr API
- [x] Store your secret key in an ENV
- [x] Figure out how to get a random Beaver photo
- [x] Include that beaver photo in the create form

#### What I learned
- Environment Variables
  - View all currently assigned ENV with printenv
  - set a new one with "export KEY=value"
    - but you may need to do that in your ~/zprofile to make it stick, not sure
    - or at least reboot the terminal if you have other windows open

- You can convert an .xml response from an API to a hash (and you need to) using Hash.from_xml(xml_response)

## Sun 20th
### Odin Project - Ruby on Rails - [CSS Bundling](https://www.theodinproject.com/lessons/ruby-on-rails-css-bundling)
- 