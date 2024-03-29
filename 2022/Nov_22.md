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

- If you want to evaluate Ruby/Rails code in your .css, you need to make the file .css.erb
  - but this'll stop autocomplete for css, so do it last/only when you need to test that part

## Sun 20th
### Odin Project - Ruby on Rails - [CSS Bundling](https://www.theodinproject.com/lessons/ruby-on-rails-css-bundling)
The cssbundling-rails gem provides a way of installing the most commonly used CSS pre-processors/bundlers. There are individual gems for these but this way is apparently easier.

- Requires node.js to work
  - build script handles processing your CSS, eg. for Tailwind it makes sure only the T classes you actually used in you project are built
    - is found in package.json
  - make sure the build script is running when needed by starting your app with ./bin/dev
    - runs rails server and JS/CSS watch commands

- Installs tools and files needed to get the option you chose running
- Adds required import statements
- Gives you instructions on the build script needed

- Has installation support for 5 of the most common CSS tools
    1. [Bootstrap](https://getbootstrap.com/) This is probably one of the most famous libraries used to get going with the look and feel of a new application when you need a proof of concept.

    2. [Bulma](https://bulma.io/) An alternative to Bootstrap. Has opinionated styling to get you up and running when you don’t have good CSS knowledge to design your own sites.

    3. [Dart Sass](https://sass-lang.com/dart-sass) The current hot flavour of processing sass files. A way to add additional CSS features to extend what you can do.

    4. [PostCSS](https://postcss.org/) A tool for transforming CSS by using Javascript. It allows you to do things like use future CSS features not supported in all browsers or use one of the many PostCSS plugins to enhance your CSS.

    5. [Tailwind](https://tailwindcss.com/) A utility-first CSS framework. It works similarly to Bootstrap in that you add CSS to your application by adding classes to your HTML. Where it differs is Tailwind is not a way to avoid understanding CSS but instead allows you to build up your design by using reusable classes that do only one thing. It’s moving the CSS to the markup instead of under a class name in your CSS files. You’ll either love it or hate it.

- Installation
  - For a new Rails app
    - rails new myapp --css [tailwind|bootstrap|bulma|postcss|sass]
  - For an existing app
    - add gem 'cssbundling-rails'
    - run bundle install
    - use the generator like "rails css:install:[tailwind|bootstrap|bulma|postcss|sass]"


## Mon 21st
### Odin Project - Ruby on Rails - [JS Bundling](https://www.theodinproject.com/lessons/ruby-on-rails-js-bundling)
Provides installers to setup esbuild, rollup or webpack to allow bundling, which is then stored in app/assets/builds

- Bundling seems to be mostly used for compatibility with frameworks, modules etc. that require it. With HTTP2 making a lot of small requests is not as much of a performance problem as it used to be.

- In the absence of those compatibility issues, importmaps are better because you don't have to redownload/parse the bundle every time something changes

- [esbuild](https://esbuild.github.io/)
  - lightweight/fast
  - lacks features compared to others
- [Rollup](https://rollupjs.org/guide/en/#introduction)
  - uses JS syntax for importing/exporting functions
- [Webpack](https://webpack.js.org/concepts/)
  - static module bundler
  - creates a dependency graph and uses it to make 1 or more bundles of everything your app needs

- Also use ./bin/dev to watch for JS changes
- Install bundler with "./bin/rails javascript:install:webpack|esbuild|rollup"
  - but better to just do it from the start with "rails new app_name -j webpack|esbuild|rollup"
  - with esbuild you need to add this "./bin/rails stimulus:manifest:update" to index.js or controllers won't be bundled

### Odin Project - Ruby on Rails - [Turbo](https://www.theodinproject.com/lessons/ruby-on-rails-turbo)
- Single Page Applications
  - A web app that loads only a single document. The page is dynamically rewritten with new info.
  - Rails has a built-in way of creating SPAs with Hotwire, itself comprised of Turbo, Stimulus and Strada (Strada is unreleased and deals with mobile responsiveness)

- Turbo
  - Uses 4 techniques to create the appearance of a speedy SPA without JS
    - **Turbo Drive:** Handles page navigation without full reloads, as I learned [here on the 15th](https://github.com/Brett-Tanner/Journal/blob/2227706add12e50687b9228851a1cc478a857ecd/Oct_22.md)
    - **Turbo Frames:** Let you update content within only defined region of your page
    - **Turbo Streams:** Automatically inserts new posts etc. at the start of a feed without needing a refresh
    - **Turbo Native:** Lets you do the same stuff on mobile

- Turbo Frames
  - One or multiple regions of the page which can be changed in response to a request
  - Any links or forms inside the frame will make a special request that only affects the contents of the frame
  - Designated by wrapping the area in a turbo-frame HTML tag
    - which can be done with turbo_frame_tag, taking a string argument which becomes the id of the HTML tag
    - can auto increment the ids by putting them in an each block and making the variable the name you want to increment
      - it'll name each frame that variable with an incremented number appended
  - One benefit over just using partials is you don't have to duplicate stuff in controllers, you can just have the frame make a call to the controller action you need in the src attribute
  
  - You can update the data in a frame by putting a link inside it that points at another page with a frame that has the same id
    - the current contents of the frame will be replaced by the contents of the frame on the other page
    - by default, anything outside the frame will not change at all during this process
      - but it's possible to change that using data-turbo-action to advance the browser history and update the url
    - You can break out of a frame and reload the whole page by adding data-turbo-frame: "_top" to the link
    - You can also do the opposite, update the frame with a link outside it, by including data-turbo-frame: "frame_id" on the link

  - If frames are given a "src" attribute they'll be loaded from that source after main content of the page has loaded
    - A placeholder can be wrapped inside this frame to be displayed until the real content is loaded from the src link
    - an src frame (and only that type of frame) can have the loading: lazy option set, so that it loads only when it comes into view

- Turbo Stream
  - Sends new content to the page wrapped in a turbo-stream element
    - the element takes 2 main options, action and target
      - target gives the id of the element it's going to update in the DOM
      - action determines how it updates that element. There are 7 choices:     
        1. Append
        2. Prepend
        3. Before
        4. After
        5. Replace
        6. Update
        7. Remove
  - streams can be sent in response to a browser request or broadcast over a websocket connection
    - for browser requests, can be delivered as "view_name.turbo_stream.erb" files

  - You can add turbo-streams to a controller like this, similar to how you add json/xml responses for an API
  ```
  def create
    @post = Post.new(post_params)

    respond_to do |format|
      if @post.save
        format.turbo_stream
      else
        format.html { render :new, status: :unprocessable_entity }
      end
    end
  end
  ```
    - the corresponding turbo-stream view could then be as simple as <%= turbo_stream.append "posts", @post %>
    - You could also chain multiple turbo-stream actions in a single view, to affect multiple areas of the page (like post list and count)


## Tues 22nd
### Odin Project - Ruby on Rails - [Stimulus](https://www.theodinproject.com/lessons/ruby-on-rails-stimulus)
Stimulus gives you a way of creating and using reusable controllers that add a bit of extra interactivity to your page. It is a HTML first framework which does not typically render HTML, rather attaches behaviour to your existing HTML.

- Uses data-attributes to attach to and configure behaviour on your HTML, eg.
```
<div data-controller="clipboard">
  PIN: <input data-clipboard-target="source" type="text" value="3737" readonly>
  <button data-action="click->clipboard#copy">Copy to Clipboard</button>
</div>
```
  - data-controller lets Stimulus know which controller you want to use
  - data-clipboard-target lets Stimulus know where the input for the controller action is coming from
    - first you have to add it to the controller by adding it to the "static targets" array, which will create three references to it
      - you can access the target in your action using this.nameTarget
      - or multiple with this.nameTargets
      - or ask if they're available with this.hasNameTarget
  - data-action has the equivalent of an event listener in click, followed by controller#action
    - [full list of events you can listen for](https://developer.mozilla.org/en-US/docs/Web/Events)

- Stimulus Controllers
  - To create a new controller, create a file in the app/js/controllers folder with a filename like name_controller.js
  - An empty controller looks like this, actions are written between the last curly braces
  ```
  import { Controller } from "@hotwired/stimulus"
  export default class extends Controller {}
  ```

- State
  - the controller can have its own state, though you usually want to avoid this
    - anything you define on "this" is available to any action in the controller
    - you can also declare specific value attributes to listen to for changes like "static values = { count: {type: Number, default: 0} }"
      - then you can define a function to be called on any change in the form "countValueChanged"
    - if you want to declare a constant for use in the controller, do it between the import and export using const

- Class Attributes
  - If you want to use the same controller to toggle different classes based on the element, set them on the element with "data-toggle-change-class="class_name""
    - the call them in the #toggle action with this.changeClass

- Lifecycle functions
  - connect() {} is called whenever an element with data-controller attribute matching the controller's name appears in the DOM
  - initialize() {} is called once when the controller is first instantiated
  - disconnect() {} is called when the controller is disconnected from the DOM

- camelCase v kebab-case example
```
<div data-controller="reset-input">
  <input 
    data-reset-input-target="twoWords"
    data-action="keyup->reset-input#updateButton"
  >
</div>
```

## Wed 23rd
### Odin Project - Ruby on Rails - [Stimulus Exercises](https://www.theodinproject.com/lessons/ruby-on-rails-stimulus#exercises)
- [x] Example controller
- [] Toggle controller (make it reusable in the following ways)
  - [] Make it show another element, like a dropdown menu
  - [] Make it hide itself and show another element when clicked
  - [] Clicking a checkbox highlights the element containing the checkbox
- [] Controller for text inputs with a limited length that warns them when close/over

- [] Project: In a new Rails app, create a car model that :has_many variants; make up some attributes. Then create a form to edit a car in which you can dynamically add more variants using :accepts_nested_attributes_for and a Stimulus controller (that adds the form fields you need for a new variant entry). Bonus points for destroying existing records when submitting.


## Thurs 24th
### Odin Project - Ruby on Rails - [Stimulus Exercises](https://www.theodinproject.com/lessons/ruby-on-rails-stimulus#exercises)
- [x] Toggle controller (make it reusable in the following ways)
  - [x] Make it like a dropdown menu
  - [x] Make it hide itself and show another element when clicked
  - [x] Clicking a checkbox highlights the element containing the checkbox
- [x] Controller for text inputs with a limited length that warns them when close/over

- [] Project
  - [] create a car model that :has_many variants; make up some attributes
  - [] create a form to edit a car in which you can dynamically add more variants using :accepts_nested_attributes_for 
  - [] and a Stimulus controller (that adds the form fields you need for a new variant entry, presumably a button for when the current ones are full)
  - [] Bonus points for destroying existing records when submitting.

### What I learned
- You can have an element be both action and target

- Input listens when you type, change listens when you submit the change

## Fri 25th
### Odin Project - Ruby on Rails - [Stimulus Exercises](https://www.theodinproject.com/lessons/ruby-on-rails-stimulus#exercises)
- [] Project
  - [x] create a car model that :has_many variants; make up some attributes
  - [x] create a form to edit a car in which you can dynamically add more variants using :accepts_nested_attributes_for 
    - [] and a Stimulus controller (that adds the form fields you need for a new variant entry, presumably a button for when the current ones are full)
    - [] bonus points for destroying existing records when submitting (with blank fields for a variant)

### What I learned
- You can't name columns type, it's reserved for storing classes in case of inheritance
- I forgot the form builder automatically names the submit button to something appropriate, so no need to override it

- Located [this](https://www.stimulus-components.com/docs/stimulus-rails-nested-form/) which I can steal ideas from for the "add variant" button
  - was struggling with how to setup the targets, my best idea without looking at it was to make fields_for a target, count how many variant forms were in it and use that number to generate the ids for the next one


## Sat 26th
### Odin Project - Ruby on Rails - [Stimulus Exercises](https://www.theodinproject.com/lessons/ruby-on-rails-stimulus#exercises)
- [x] Project
  - [x] create a form to edit a car in which you can dynamically add more variants using :accepts_nested_attributes_for 
    - [x] and a Stimulus controller (that adds the form fields you need for a new variant entry, presumably a button for when the current ones are full)
    - [x] bonus points for destroying existing records when submitting

### What I learned
- How the stimulus component I shamelessly copied works

  - To add variants
    - The form itself has the controller defined
    - You make a template wrapper around your fields_for, set the options like "form.fields_for :variants, Variant.new, child_index: 'VARIANT'", and make it the templateTarget
      - I think Variant.new is the object to use
      - child_index specifies the name used to increment them
        - then the controller uses the current time to ensure it's unique
      - render the actual fields as a partial
      - Then because a template isn't rendered (it's instead used as a template to be inserted later, duh) you need to do the fields_for again without the extra options to actually render any existing variants
    - You need an empty div as the targetTarget
      - controller inserts the new fields (from your template) before that
  
  - To remove variants 
    - it searches for the nearest wrapper (which goes around a set of variant fields)
    - if it's a newly created one, it simply removes it
    - if it was a pre-existing variant, it hides it and sets its destroy hidden field to "1", meaning the variant will be destroyed

- **Remember you need to allow the :id and :_destroy attributes in your params hash if you don't want exponential duplicates/an inability to delete respectively**

### Odin Project - Ruby on Rails - [Stimulus Exercises](https://www.theodinproject.com/lessons/ruby-on-rails-mailers)
Email in Rails is conceptually pretty similar to rendering views

- Overview
  - Uses ActionMailer gem
  - Mailer is similar to a model and controller baked into one
    - can generate with "rails generate mailer ..."
    - set up methods for each type of email you wanna send
      - in those, you identify the key fields/variables to be used in the email
  - Email itself is a view, in app/views but ina folder named after the mailer
    - needs two versions, HTML and text as a fallback/to get past spam filters
  - Sending mail is a two step process, first build with the mailer method then send with #deliver_now pr #deliver_now!

- Callbacks exist, and are run in relation to the generation of the email rather than when it's sent (before/after/around_action)

- You'll want to use an addon to handle sending your mail, all the ones they list are for Heroku tho

- The [Letter Opener](https://github.com/ryanb/letter_opener) gem displays emails in the browser when they would be sent (in dev) so you don't spam people

- Email Wisdom
  - It's SLOW, like 1-2 seconds per email. Don't have your main app do it if you're sending a bunch
  - Make sure to use full urls (not _path helper) since users'll be accessing externally, specify the host as a variable
  - No access to stylesheets, so styling must be inline or in style tags
  - Attaching images can be a pain
  - [You can preview emails](https://guides.rubyonrails.org/action_mailer_basics.html#previewing-emails)

- Mailer
  - default sets the default values for all emails sent from this mailer
  - mail() specifies headers like subject and recipients     
    - there is also attachments(), which can be made #inline
  - to send an email with the name as well as address, use email_address_with_name(address, name) in your to: 

- Integration
  - You can send an email to a new user by adding "UserMailer.with(user: @user).welcome_email" in the User.create action
    - any key/value pair passed to #with become params for the mailer action
  - can be added to queue using #deliver_later

- Can send via your own Gmail with this in your "config/environments/$RAILS_ENV.rb"
```
config.action_mailer.delivery_method = :smtp
config.action_mailer.smtp_settings = {
  address:              'smtp.gmail.com',
  port:                 587,
  domain:               'example.com',
  user_name:            '<username>',
  password:             '<password>',
  authentication:       'plain',
  enable_starttls_auto: true,
  open_timeout:         5,
  read_timeout:         5 }
```

- [Mailer testing guide](https://guides.rubyonrails.org/testing.html#testing-your-mailers)


## Sun 27th
### Odin Project - Ruby on Rails - [Project: Confirmation Emails](https://www.theodinproject.com/lessons/ruby-on-rails-sending-confirmation-emails)
#### What I did
- [x] Generate the mailer
- [x] Install the letter-opener gem
- [] Create the action to send the confirmation email (RailsGuide steps [here](http://guides.rubyonrails.org/action_mailer_basics.html))
- [] Build HTML and plaintext views
- [] Test by making a new Event on the site
  - [] and from rails c

#### What I learned
- It's really hard to have a gf, a social life and be productive



## Mon 28th
### Odin Project - Ruby on Rails - [Project: Confirmation Emails](https://www.theodinproject.com/lessons/ruby-on-rails-sending-confirmation-emails)
#### What I did
- [x] Create the action to send the confirmation email (RailsGuide steps [here](http://guides.rubyonrails.org/action_mailer_basics.html))
- [x] Build HTML and plaintext views
- [x] Test by making a new Event on the site

### Odin Project - Ruby on Rails - [Advanced Topics](https://www.theodinproject.com/lessons/ruby-on-rails-advanced-topics)
- Advanced Routing
  - Turns out if you wanna link to the #show of a certain resource, you can just put the object itself rather than a _path helper in link_to

  - Singular resources
    - Unlike resources :posts for example, sometimes it makes sense for there to only be one of a resource
    - You create it with "resource :dashboard" for example, both singular
    - Only generates 6 routes since you don't need an index anymore, and doesn't include an id param because there's only one resource
  
  - Nested Resources
    - Some resources make sense to have nested inside another resource, for example lessons could be nested in courses
    - You need to include ids for both in the url
    - Code for it in routes.rb looks like this
    ```
      # config/routes.rb
    TestApp::Application.routes.draw do
      resources :courses do
        resources :lessons
      end
    end
    ```
    - You will be taken to the controller of the deepest nested resource, and it's that id which will simply be id in params
    - You can choose to nest only certain routes and have others not nested
      - Simple rule for deciding this is if you need the parent's id in your action you should probably nest

  - Member and collection routes
    - If you want to add a non-REST route to an individual member of your model (:id delineated) then use a member block inside the resources block
      - and define the route itself with the HTTP verb and action like you would without resources
    - If you want to add a non-REST route to the collection as a whole, same thing but with collection inside the resources block

  - Redirects/Wildcard routes
    - If you wanna have a simple URL that redirects to a more complex route, you can use redirect as follows
    ```
      # config/routes.rb
    TestApp::Application.routes.draw do
      get 'courses/:course_name' => redirect('/courses/%{course_name}/lessons'), :as => "course"
    end
    ```
    - Using single quotes is important
    - Capture params from the original url using %{}
    - can use as: => "" to set the alias for use with helpers
    - [There are lots of fun ways to make non-resourceful routes](https://guides.rubyonrails.org/routing.html#non-resourceful-routes)

  - Namespacing
    - You can group controllers by type, for example all the controllers that relate only to admin duties, using namespacing
    - you do this by putting the resources declarations for those controllers inside a namespace :admin block
      - if you want to still route the action to the admin controller but without prepending admin, use "scope module: admin" instead and specify only the actions you want namespaced
      - to not route it to the admin controller but still have the prefix, instead use a "scope '/admin'" block
    - has the effect of prepending admin to all the routes for those controllers, and routing them to Admin::OtherController

  - Concerns
    - Can be used to add a collection of routes to multiple different parents, for example you can use commentable as below within articles and posts
    ```
    concern :commentable do
      resources :comments
    end

    concern :image_attachable do
      resources :images, only: :index
    end

    ```

- [Metaprogramming Rails](https://www.theodinproject.com/lessons/ruby-on-rails-advanced-topics#metaprogramming-rails)
  - Seems a bit beyond anything I'll need for now, but basically lets you rewrite parts of Ruby/rails or do weird stuff like send variables to a method that doesn't exist
  - For example, you can use it to [DRY](https://rails-bestpractices.com/posts/2010/07/24/dry-metaprogramming/) your code

- Design Patterns
  - Can be useful as a set of best practices, but also considered overly prescriptive by some
  - SOLID is a common one
    - Single Responsibility Principle: classes should only have a single responsibility
    - Open/Closed Principle: Objects should be open to extension but closed to modification
    - Liskov Substitution Principle (replacing an object with one of its sub-types shouldn’t break anything)
    - Interface Segregation Principle (writing many client-specific interfaces is better than one behemoth general-use interface… think APIs)
    - Dependency Inversion Principle (instead of high level constructs depending on lower level ones, make them rely on abstractions instead)
  - [Gang of Four](http://www.blackwasp.co.uk/GofPatterns.aspx) are also common


- I18n: Internationalization
  - [Tutorial here](http://www.sitepoint.com/go-global-rails-i18n/) if it ever becomes relevant


## Tues 29th
### Odin Project - Ruby on Rails - [Websocket & Action Cable](https://www.theodinproject.com/lessons/ruby-on-rails-websockets-and-actioncable)
Usually a client/server interaction consists of request, response, then the connection closing. Websockets allow you to keep that connection open so the client can be updated with relevant information, and Action Cable brings Websockets to Rails.
- Action Cable creates a separate server within your app for Websocket
- Connection is kept open so server can send info without it being specifically requested
- Before Websockets we used
  - polling: making requests at set intervals to check for new content, then immediately returning a blank response if nothing
  - long polling: making requests for new content, which the server keeps open until there is new content to send. Once received, the client immediately makes a new request which is a again kept open until new content appears

- Action Cable
  - The client of an Action Cable connection is a "consumer", they have one connection which just deals with authentication/authorisation
  - Through their connection they can subscribe to multiple channels, containing one logical piece of work
  - They then become known as a subscriber, and the connection is a subscription
  - Once subscribed, each channel can stream "broadcastings" to the subscriber, the content you want them to get in real time

- Server-side Concerns
  - Auth/Connection
    - You put the logic for authenticating/authorising users in "app/channels/application_cable/connection.rb"
    - Set how to auth with identified_by :variable_to_identify_by
    - For example with Devise, though you can't access its methods directly (it's on a different server), you can through Warden's ENV
    ```
    def find_verified_user
      if verified_user == env['warden'].user
        verified_user
      else
        reject_unauthorized_connection
      end
    end
    ```
  - Channels
    - Similar to what a controller does, but over Websockets
    - "app/channels/application_cable/channel.rb" is the parent class they all inherit from, so put logic they all need in here
  - Subscriptions
    - Clients can subscribe to one or more channels
    - You can broadcast updates to those channels, which the channels with forward to their subscribers

- Client-side Concerns
  - You need an instance of the connection on client-side too, boilerplate for this is in "app/javascript/channels"
  - "app/javascript/channels/consumer.js" is imported to each channel, and used to create subscribers

- Creating Channels
  - use "rails generate channel", there're a lot of files that get modified
  - will generate with subscribe (to set up the stream) and unsubscribe (for cleanup) methods

- Client/Server Interactions
  - Streams
    - Can set up streams with stream_for or stream_from
      - stream_from identifies the stream from a string, while stream_for identifies it from a model
    - You can also pass params to generate a stream like so
    ```
    def subscribed
      stream_from "room_#{params[:room]}"
    end

    def subscribed
      room = Room.find(params[:id])
      stream_for room
    end
    ```

  - Broadcasting
    - Once the Websocket server is set up, you just need to broadcast to it from wherever is appropriate, usually a controller
    - If you used stream_for you can broadcast like "NameChannel.broadcast_to(object the channel was created from, data to be broadcast)"
      - The data can be a list of key/value pairs, or anything that responds to #to_json since that's how it's sent
    - However if you used a string with stream_from, you need to use "ActionCable.server.broadcast('message', @message)"

  - Client Subscriptions
    - In "app/javascript/channels/room_channel.js", consumer.subscriptions.create is called
      - this is where you can pass any params you want to use as key/value pairs, e.g. "consumer.subscriptions.create({channel: 'RoomChannel', room: 1}"
        - the first must always be channel: 'ChannelName'
        - the params are useful for having different streams within the same channel, e.g. different languages in a programming channel
      - the second argument to create is an object containing connect, disconnect and received(data) functions
        - You'll usually modify received(data) to do something like appending the data to the DOM 

  - Other details
    - You commonly want to [rebroadcast](https://guides.rubyonrails.org/action_cable_overview.html#rebroadcasting-a-message) a message sent by one client to all clients, including the sender
    - You need to be careful when sending dynamic parameters from the client or you might end up subscribing to the same stream multiple times, as detailed in this [Stack Overflow](https://guides.rubyonrails.org/action_cable_overview.html#rebroadcasting-a-message) post
    - Action Cable needs Redis to run on a hosting service
    - Connection only remains active while the HTTP request is unbroken, refreshing the page or navigating to a new one will break it and require re-establishment
    - [Full-stack examples can be found here](https://guides.rubyonrails.org/action_cable_overview.html#full-stack-examples) 
    - And [full walkthrough](https://github.com/TheOdinProject/curriculum/blob/main/ruby_on_rails/mailers_advanced_topics/actioncable_lesson.md)


## Wed 30th
### Odin Project - Ruby on Rails - [Rails Final Project](https://www.theodinproject.com/lessons/ruby-on-rails-rails-final-project)

#### What I did
- [x] Create the app with PG database
- [] Plan out the db schema
- [] Set up tests and run them continuously using [Guard](https://github.com/guard/guard), like [this](https://www.learnenough.com/ruby-on-rails-4th-edition-tutorial/static_pages#sec-guard)
  - [] Integration to make sure pages load correctly
  - [] Unit to make sure model associations work correctly
- [] Install Devise & generate Users resource
  - [] Redirect all to login page if not logged in
- [] Implement friend requests
- [] Implement notifications
- [] Create Posts resource
  - [] Create Comments resource
  - [] Create Likes join table??
  - [] Create Post partial that displays content, author, comments and likes
- [] Make the Posts index a timeline of all current_user posts and those of their friends
- [] Create User#show which displays their personal info, posts and a photo
- [] User#index shows all Users and a button to send them a friend request
- [] Use Omniauth so users can sign in with their real FB account
- [] Set up a mailer with
  - [] A welcome email
  - [] Notification emails
- [] Deploy
  - [] Figure out how to send emails without SendGrid/Heroku

##### Extra Credit
- [] Allow posts to have uploaded images
- [] Use ActiveStorage to allow Users to upload more than just a profile pic
- [] Use polymorphic associations to make Posts text OR photos
- [] Fashion is my profession


#### What I learned
- Found this potentially helpful [SO answer](https://stackoverflow.com/questions/49213989/implement-a-friendship-model-with-has-and-belongs-to-many-in-rails) about making friends
- Had a lot of good ideas about setting up the db which I need to [read](https://guides.rubyonrails.org/association_basics.html#polymorphic-associations) more about, like understanding polymorphic associations properly so I can use them to make comments commentable/likeable as well as posts
  - In addition to making posts able to be both text and images of course, which at this stage seems to be a different use case of them from what I mentioned above