# October 2022

## Sat 1st
### Odin Project - Ruby on Rails
- Found a cool article with some HTML tips
    - lazy loading, which I've heard a lot about, can be set with the loading='lazy' attribute on elements
    - for 'ol' elements, you can specify the starting number with the start='num' attribute
    - you can use the meter element to display quantities, however its apparently difficult to style
    - you can make a native HTML search with suggestions like this
    ```
    <div class="wrapper">
      <h1>
        Native HTML Search
      </h1>
    
      <input list="items">
    
      <datalist id="items">
        <option value="Marko Denic">
        <option value="FreeCodeCamp">
        <option value="FreeCodeTools">
        <option value="Web Development">
        <option value="Web Developer">
      </datalist>
    </div>
    ```
    - when you open new tabs with target='_blank' it gives access to window.opener, apparently a security concern. Use re='noopener' to avoid this
    - You can open all links on a page in new tabs by default with base target="_blank"
    - spellcheck='false/true' attribute toggles spellcheck on/off for an input
    - can use the details element to make an easy dropdown accordion like
    ```
    <div class="wrapper">
      <details>
        <summary>
          Click me to see more details
        </summary>
        <p>
          I'm the details
        </p>
      </details>
    </div>
    ```
    - can use the 'download' attribute on links to download the file rather than navigating to it
    - set the thumbnail/waiting image for a video using poster='path'

- Started working on the blog app

#### What I did
- in case I forget in the future, I eventually want to automatically populate the blog posts with my daily journal entries
- created a MVC which handles articles, and used it to display a list of article titles in the db
- set the homepage of the site to that article list


#### What I learned
- Rails autoloads things, so DO NOT use require as a general rule
    - exceptions for files in the lib directory
    - and gem dependencies with require: false in the gemfile
- Model creation
    - create a model with 'bin/rails generate model Article title:string body:text'
        - an auto-incrementing numerical id is added by default
        - bin/rails accesses the scripts, generate model is the command
        - Article is the title of the model (always singular) which will be used to create the db table (in plural, so Articles)
        - title and body are the columns of the table, followed by their data types
        - I assume the |t| in the table creation method is the auto-incrementing id?
        - the t.timestamps call at the end creates two additional tables 'created_at' and 'updated_at'
    - Database migrations are used to alter the database. They're written in Ruby so they can be used with any type of database
        - after creating the model, you can create the table it describes by running bin/rails db:migrate
        - after that you can interact with your new table
- Rails console
    - Rails has a console, kinda like irb, which allows you to interact with your application code directly
    - launch with bin/rails console
- Database methods
    - you can initialize new objects just like vanilla Ruby, but this doesn't add them to the database
    - to do that you have to call #save on the object
    - #find(id) on the database returns the record with id as the id
    - #all on the db returns all records in the db as an ActiveRecord::Relation object, which is basically a super arra
- **Probably stop pushing my commits so often, it makes it really hard to redo stuff. I should only do it when a major feature is complete and tested**


## Sun 2nd
### Odin Project - Ruby on Rails
Slow day, I was at work til late with spaced out breaks, then board games at night

#### What I did
- Added a page for individual articles that shows the title, body and post/update date
- Made the article list on the index page link to individual articles

#### What I learned
- You can pass a model object as the second argument to link_to and it'll generate the link, rather than putting article_path for example


## Mon 3rd
### Odin Project - Ruby on Rails
#### What I did
- Added the ability to create new articles, update them and delete them.

#### What I learned
- It's better to redirect_to rather than render when you alter the database or state of the application, otherwise refreshing the page will resend the same request
- Rails has a form builder
  - instantiate it with form_with
  - pass the thing you want to build a form from using 'model: @thing'
  - to create elements you call the element on form e.g. form.label or form.text_area and append a symbol to show what value of the object you're trying to set e.g. :title
  - more details on form builders in Rails [here](https://guides.rubyonrails.org/form_helpers.html)
- You can validate form inputs using the corresponding Ruby file in models
  - validates :value_to_validate, presence: true/false, length: { minimum: 10 }, etc..
  - show errors in the view file using
  ```
  <% @article.errors.full_messages_for(:title).each do |message| %>
    <div><%= message %></div>
  <% end %>
  ```
  - full_messages_for returns an array of error messages for the form value passed
- Seems that if you call a method like #save or #update in an if statement, it actually puts the method into action. Seems logical, but I was calling it elsewhere then checking if the result was as expected in the past
- You can use turbo_method and turbo_confirm as arguments passed to the data: attribute of link_to to set the type of the request and require confirmation before it's completed, respectively
- When you rails generate a model, you get a migration file, a model file, testing harness for the model and a file that stores test data in the form of your model 
  - not sure if the test data is immediately usable though, it seems to be as variables rather than in the correct form
  - this is a framework tho, those variables could link to something of the correct type
  - if you use 'model_name:references' when generating, the new model will belong to the model prior
    - the flip side is adding has_many :object to the model for the thing it belongs to, which allows you to retrieve the 'many' using parent.many 
  - it will also include a new col that's the name of the model you're relating it to + '_id' and contains the foreign keys


## Tues 4th
### Odin Project - Ruby on Rails

#### What I did
- Added comment functionality
- Used partials to clean up the article show view
- Finished the 'paint by numbers' part of the project, time to add my own stuff
  - start by styling the homepage/article list


#### What I learned
- You can nest routes like by putting them inside a do/end block where resources :controller_name takes the place of the method name
  - This allows you to capture the relationship between two models in your routing
  - For example in this project, every comment requires a post in the URL to access
  - also creates routing helpers like article_comments_url and edit_article_comment_path, which take an instance of @article as the first param
- "rails generate controller name" creates the controller .rb file, a views folder, a test.rb file and a helper.rb file
- When you 'render' a list of things, it iterates over the collection and assigns each member to a local variable named the same as the partial
  - somehow rendering 'comments' uses the view called "comment", I assume rails fixes that for me
  - ah, maybe because the folder is comments, then each individual comment is rendered using the actual view partial called _comment

- Assets like stylesheets and images are recommended to go in the 'app/assets' directory these days, so they can be combined and minified
  - if you're using a pre-processor like Sass, you'll need to put those files in /assets
  - in production, the files in app/assets are compiled tp public/assets


## Wed 5th
### Odin Project - Ruby on Rails

#### What I did
- Decided how to style the blog
  - [x] Header with the site name as a link to the article list and new post button
  - [x] Use grid for the homepage
    - [x] Style the articles/cards like notes written on old paper
    - [] Small icons on the bottom for comments/edit/expand to its own page (still need to add the links)
    - [] Expand slightly on hover
    - [] When clicked, move to the top of the grid and take up the whole width of the container
      - [] how do I minimize it? either have an 'X' to click which returns it to normal (clears the classes I'd have to apply to make it big)
  - [] Articles on a navy/grey background (or the top of a desk?)
  - [] Edit button maybe on the letter element for the single article page if I can make it not look terrible
  - [] Add a loading animation when moving between pages
  - [] Use variants to have different layouts for mobile and desktop

#### What I learned
- You can limit the number of records printed/processed by inserting #limit(num) between the model and method being called


## Thurs 6th
### Odin Project - Ruby on Rails

#### What I did
- [x] Header with the site name as a link to the article list and new post button
- [x] Use grid for the homepage
  - [x] Style the articles/cards like notes written on old paper
  - [x] Small icons on the bottom for comments/edit/expand to its own page
  - [x] Expand slightly on hover
  - [x] When clicked, move to the top of the grid and take up the whole width of the container
    - [x] how do I minimize it? either have an 'X' to click which returns it to normal (you can just click on it again)
- [] First thing tomorrow is making the cols responsive so I don't have 3 columns on mobile

#### What I learned
- You can (in theory, my pages aren't long enough to test yet) link to an id on a page by using the 'anchor: id' element
- You set the z-index of an element with the z-index property, not order
  - higher numbers are closer to the surface
- Contrary to what RailsGuides says, JS goes in the javascript folder in app, not app/assets
- Had a fun time remembering 'defer' is an important attribute when you're generating your html
  - in Rails you add it with defer: "defer" after the link
- In CSS, you can use :not(class or id) to exclude classes or ids from the selector
- Ended up using scale3d() to transition the articles, since the transition looks more fluid and it resizes better when the window does


## Fri 7th
### Odin Project - Ruby on Rails

#### What I did
- tried a branch to tile the articles on the homepage using flex rather than grid, in an attempt to allow them to collapse to one/two columns when in half screen/on a mobile device
  - also considered solving it with media queries that reduce the number of rows in the grid, but I vaguely remember media queries making your page slower
- Also was first day of the worlds pass/new patch and I expected to have two free units at work, which didn't pan out. So I did barely anything today tbh other than some thinking on the train. Do have all tomorrow and Mon to work on stuff though


## Sat 8th
### Odin Project - Ruby on Rails

#### What I did
- [x] Header with the site name as a link to the article list and new post button
- [x] Use grid for the homepage
  - [x] Style the articles/cards like notes written on old paper
  - [x] Small icons on the bottom for comments/edit/expand to its own page
  - [x] Expand slightly on hover
  - [x] When clicked, move to the top of the grid and take up the whole width of the container
    - [x] how do I minimize it? either have an 'X' to click which returns it to normal (you can just click on it again)
- [x] Make the cols responsive so I don't have 3 columns on mobile
- [] Style the other pages to match
- [] Figure out why the comment count text is so annoying to make scale with its image

#### What I learned
- Not having a random h1 in the grid with all the divs makes it much easier to make a responsive grid
- Googling things is still a good idea if I can't figure something out at this stage, I did a lot of complex things including media queries when this [CSS Tricks article](https://css-tricks.com/look-ma-no-media-queries-responsive-layouts-using-css-grid/) would have helped me do it with 3 lines of code and just grid
  - summary is to use a combo of repeat, auto-fit and minmax on template-columns, **do not define rows**


## Sun 9th
### Odin Project - Ruby on Rails

#### What I did
- [x] Header with the site name as a link to the article list and new post button
- [x] Use grid for the homepage
  - [x] Style the articles/cards like notes written on old paper
  - [x] Small icons on the bottom for comments/edit/expand to its own page
  - [x] Expand slightly on hover
  - [x] When clicked, move to the top of the grid and take up the whole width of the container
    - [x] how do I minimize it? either have an 'X' to click which returns it to normal (you can just click on it again)
- [x] Make the cols responsive so I don't have 3 columns on mobile
- [] Style the other pages to match **(started this but late at night, so I just scaffolded until I ran into the stylesheet problem)**
- [] Figure out why the comment count text is so annoying to make scale with its image

#### What I learned
- Styles in the show.css are somehow applying to index.css despite not being linked to that view
- You can order results from your model by a column using #order('col_name' DESC(opt))


## Mon 10th
### Odin Project - Ruby on Rails

#### What I did
- [x] Header with the site name as a link to the article list and new post button
- [x] Use grid for the homepage
  - [x] Style the articles/cards like notes written on old paper
  - [x] Small icons on the bottom for comments/edit/expand to its own page
  - [x] Expand slightly on hover
  - [x] When clicked, move to the top of the grid and take up the whole width of the container
    - [x] how do I minimize it? either have an 'X' to click which returns it to normal (you can just click on it again)
- [x] Make the cols responsive so I don't have 3 columns on mobile
- [] Style the other pages to match
  - [] Show page (scaffolded)
  - Edit/new pages (probably same stylesheet since they're the same)

#### What I learned
- The issue with CSS for certain views applying to others was caused by sprocket, per this exceptionally helpful [Stack Overflow answer](https://stackoverflow.com/questions/33189474/my-stylesheets-in-rails-seem-to-be-overlapping)
  - The 'require_tree' setting in application.css (despite being commented out) combines all your css
    - one way to fix my issue is by removing that setting (deleting, not commenting out) then linking the stylesheets manually with 'stylesheet_link_tag'
      - not recommended because you will likely have to duplicate CSS, and will have completely different CSS for different parts of your app
    - the second, recommended way, is to structure your CSS with classes for the different views, then select them with both that class and the one you'd normally use
      - you do it like this
      ```
       div {
          background: green;

          p {
              background: red;

              &:hover {
                  background: blue;
              }

              &:active {
                 background: blue; 
              }
          }   
      }
      ```
      - which produces a result like this (but maybe only in SASS etc.)
      ```
      div {
          background: green;
      }

      div p {
          background: red;
      }

      div p:hover {
          background: blue;
      }

      div p:active {
          background: blue;
      }
      ```
  - I think I'll be manually linking them for this project to avoid redoing all my CSS, but I'll try to remember the correct way to do it in the future
    - actually, it seems that when you go from page to page the stylesheets persist, probably get added to the asset pipeline and kept there. 
    - So it's best to use the different classes for different views solution at all times 


## Tues 11th
### Odin Project - Ruby on Rails - Blog Project

#### What I did
- [x] Header with the site name as a link to the article list and new post button
- [x] Use grid for the homepage
  - [x] Style the articles/cards like notes written on old paper
  - [x] Small icons on the bottom for comments/edit/expand to its own page
  - [x] Expand slightly on hover
  - [x] When clicked, move to the top of the grid and take up the whole width of the container
    - [x] how do I minimize it? either have an 'X' to click which returns it to normal (you can just click on it again)
- [x] Make the cols responsive so I don't have 3 columns on mobile
- [x] Style the other pages to match
  - [x] Show page
  - [x] Edit/new pages (probably same stylesheet since they're the same)
- [] Add a full article list with infinite scrolling


#### What I learned
- You can delete all the data in your model with Model.delete_all
  - But it won't work if there are things those records relate to, so you need to delete anything connected to them first
- Following the [Rails deploy guide](https://render.com/docs/deploy-rails#update-your-app-for-render) works, just remember you need to change the database.yml like this if your dev version uses SQLite
```
group :development, :test do
 gem 'sqlite3'
end

group :production do
  gem 'pg'
end
```
  - Then 'bundle config set --local without production'
  - And 'bundle lock --add-platform x86_64-linux --add-platform ruby'
- Also make sure you include database name, username and password (as an env variable), guide seems to think it all comes from the url but doesn't seem to work that way

### Odin Project - Ruby on Rails - Active Record
- Active record is one of the 7 gems making up Rails. It handles the database stuff and is known as an 'ORM'
  - It means you can switch database types just by changing the database.yml file, which I've definitely experienced going from SQLite in dev to Postgres for Render
  - You can create a new object (row) like 'u = User.new(name: "Sven", email: "sven@theodinproject.com")'
    - Then add it with u.save
  - Or use u = User.create(name: "Sven", email: "sven@theodinproject.com") to do both steps together, which you apparently won't always want to do
- Migrations and the model file, along with some tests, are generated by rails generate model model_name
  - Can be passed options to set up the col names

- Migrations 
  - tell Rails how you want to set up or change a database
  - execute the migration using 'rails db:migrate'
    - Will run the up or change methods of all migrations not yet run
    - Or you can name a migration to run all up to that migration
  - roll back with 'rails db:rollback'
    - but apparently it's best practice to make a new migration removing the col unless you really screw something up to preserve the db
  - migrations can be re-run in the future to reproduce your db even in different db types
  - or if you want to blow the db up you can do that then re-run all the migrations you want to keep
  - If the migration name is of the form "AddColumnToTable" or "RemoveColumnFromTable" and is followed by a list of column names and types then a migration containing the appropriate add_column and remove_column statements will be created.
    - list the col_names and types in the form 'name:type'
      - type can be 'references' or 'belongs_to', which creates a column linking to the model given in name, e.g. user:references creates a user_id col
    - can do more than one at a time, just separate with spaces
    - can do a very similar thing with CreateXXXX to create a table XXXX
    - Can also create a join table with 'bin/rails generate migration CreateJoinTableCustomerProduct customer product'
    - chan use 'change_column' on the name or type, but it's irreversible

- Validations
  - Three ways of validating input
    - Using JS in the browser, benefit is it provides immediate feedback to the user but it's not secure so don't trust it
    - Server side code in your model that checks inputs against constraints, more secure but takes a round trip HTTP request to produce anything
      - Useful model validation helpers include:
        - acceptance: true/false is used when a user has to check a box to continue
          - can pass a message with the {message: ''} option, the default is 'must be accepted'
        - validates_associated also calls valid? on any associated objects
          - don't use it on both ends or you'll end up in an infinite loop
        - confirmation is for fields that must be entered twice to be confirmed
          - creates a virtual attribute that is the name of the attribute to be confirmed with _confirmation appended, so make sure you provide that as the name of the form field
          - also validate the 'presence' of that attribute, as the confirmation validation only runs if it's not nil
          - can also pass {case_sensitive: false} to stop the validation being case sensitive
        -comparison compares the first attribute to a second provided one with {comparison operator: :attribute to compare}. Compare options are these symbols or a proc:
          - :greater_than - Specifies the value must be greater than the supplied value. The default error message for this option is "must be greater than %{count}".
          - :greater_than_or_equal_to - Specifies the value must be greater than or equal to the supplied value. The default error message for this option is "must be greater than or equal to %{count}".
          - :equal_to - Specifies the value must be equal to the supplied value. The default error message for this option is "must be equal to %{count}".
          - :less_than - Specifies the value must be less than the supplied value. The default error message for this option is "must be less than %{count}".
          - :less_than_or_equal_to - Specifies the value must be less than or equal to the supplied value. The default error message for this option is "must be less than or equal to %{count}".
          - :other_than - Specifies the value must be other than the supplied value. The default error message for this option is "must be other than %{count}".
        - **and a lot of others [here](https://guides.rubyonrails.org/active_record_validations.html#validation-helpers), too many to be worth repeating in full here**
      - Common options for model validations are 
        - :allow_nil/:allow_blank, blank includes nil and any other lack of value like an empty string
        - message:, passed a string or proc which can contain value, attribute and model variables
          - procs are passed 2 arguments, the object being validated and a hash with the variables above in key/value pairs
        - :on determines when the check is run
        - :strict raises an exception when it fails
        - :if and :unless determine when the validation is run
          - you can apply those conditions to a bunch of validations using 'with_options if:/un;ess: condition' and a block
    - At database level, to avoid race conditions when your application is super big. Most certain way as your db is the arbiter of what's valid/unique
      - Validations return false if #update used, raise an exception if #update! used
    - To check if a given record is valid you can instantiate it with #new then run #valid? on it 
      - any errors can be accessed by calling #errors on the object after it was checked with #valid?
      - #errors[:attribute] is used to show the full errors for that attribute
    - You can display those errors in your view like [this](https://guides.rubyonrails.org/active_record_validations.html#displaying-validation-errors-in-views)

- Relationships
  - A user 'has_many' posts and a post 'belongs_to' a user
  - There's also 'has_and_belongs_to_many', for example a person has many games and games have many people playing them
    - this requires creating a join table to show the relationship between the records


## Wed 12th
### Odin Project - Ruby on Rails - Active Record
- Can update records once found using record.update(key: value)
- Added notes from more detailed reading on Active Record in yesterday's notes to avoid fragmentation
- If Rails doesn't have the right helper for your needs, you can execute arbitrary SQL with 'Model.connection.execute("SQL code here")
- 'rails db:setup' creates the db, loads the schema and initializes it with the seed data
- 'rails db:reset' drops the database then sets it up again
- Seeds
  - add some Ruby to generate seed data to db/seeds.rb like 
  ```
  5.times do |i|
    Product.create(name: "Product ##{i}", description: "A product.")
  end

  ```
  - then run 'rails db:seed'

- Ready for the 'Micro-Reddit' project tomorrow


## Thurs 13th
### Odin Project - Ruby on Rails - Micro-Reddit Project

#### What I did
- [x] Data model warmup
  1.  course_id PRIMARY KEY, title STRING, description TEXT
      lesson_title STRING lesson_body TEXT course_id FOREIGN KEY
    Lessons belong_to courses, and a course has_many lessons
    Validations
      - title and description/body must be present
  2.  u_id PRIMARY KEY, username STRING, email STRING, others FOREIGN KEY
    Have tables for all the demo info that are just a primary key and the city/age etc.
    Validations
      - username and email must be present
      - the demo data should be included in the current table if you're gonna do it that way (cities, states etc.)
      - Ages must be greater than 0 and less than 150 or so
  3.  u_id PRIMARY KEY, username STRING, pwd STRING
      pin_id PRIMARY KEY, url STRING, u_id FOREIGN KEY
      comment_text TEXT, c_id FOREIGN KEY, u_id FOREIGN KEY
    Pins and comments belong_to users, comments belong to pins as well
    Validations
      - Pins must have a URL and a u_id (if that's not already enforced by needing to be logged in to post one)
      - Comments must have a pin_id
  4. Only difference to 3 is comments have ids and can belong to other comments, so each comment has a foreign key which can point to the comment it replied to or be null
    - would it be better to just change the existing foreign key to accept comment ids as well, then just rebuild the comment tree by following it up like a linked list? Probably depends on use cases/how well that would perform in certain situations
- [] Plan out the micro-reddit models



## Fri 14th
### Odin Project - Ruby on Rails - Micro-Reddit Project

#### What I did
- [x] Plan out the micro-reddit models
  - Users table
    - id PRIMARY KEY
    - username STRING
      - Validations
        - presence
        - uniqueness
        - length: between 3 and 20 characters
        - format: only allow alphanumeric characters
    - password STRING
      - Validations
        - presence
        - length: more than 8 characters
        - confirmation: must match the value from the confirm password field
        - format: use the regex to check it's not all letters or numbers
  - Posts table
    - id PRIMARY KEY
    - title STRING
      - Validations
        - Max length: 50 characters
        - presence
    - body TEXT
      - Validations
        - presence
  - Comments table
    - id PRIMARY KEY
    - body TEXT
      - Validations
        - presence
    - post FOREIGN KEY
    - author FOREIGN KEY


- [x] Generate User model
  - [x] apply validations
  - [x] check they work

- [x] Generate Post model
  - [] apply validations
  - [] check they work

- [] Generate Comment model
  - [] apply validations
  - [] check they work

#### What I learned
- Remembered I have a Useful Ref bookmark for common Regex patterns and used that to validate passwords
- Some regex modifiers like $ and ^ require you to set the option "multiline: true" as they apparently pose a security risk
  - should probably look into why that is when I get to making something people may actually use
- In SQL, STRING is limited to 255 characters while TEXT is 30 000
- Struggled with adding a foreign key to the Post table linking to a user
  - from some quick testing it seems primary keys aren't being auto-generated for the users table
  - honestly I think I overthought it and messed around with too much stuff, just doing it using user:references and adding a has_many :posts to the User model did the trick
  - also remember that to create a new post you wanna call @user.posts.create(), not just Post.new. 
    - Not realizing that may also be why I had issues before



## Sat 15th
### Odin Project - Ruby on Rails - Micro-Reddit Project
- [x] Generate Post model
  - [x] apply validations
  - [x] check they work

- [x] Generate Comment model
  - [x] apply validations
  - [x] check they work

Finished the project

### Odin Project - Ruby on Rails - The Asset Pipeline
- Asset pipeline feeds any assets in after the initial load of HTML is received by the browser
  - Reason for existing is that you want separate files for human readability, but one file to minimize the number of http requests
    - also minifies them into one file for each type (e.g. application.css), which can remove whitespace and apply other optimisations
      - As I discovered in the last project, require_tree in that file includes all the files of that type in the directory (other commented out lines also do stuff)
      - Could use require_directory for only a specific directory, tree is recursive but directory only does the one
  - Apparently it's now best practice to include JS with the Webpack gem now, rather than the asset pipeline
  - The solution I ended up using to have different styles for the same class in different views by adding a class named the same as the view is called namespacing
  - To render HTML in strings that are part of your view, tell the view it's safe with 'raw' before the string

### Odin Project - Ruby on Rails - Importmaps
- Importmaps are new in Rails 7, used to include 3rd party JS packages in your Rails application
  - Allow you to import JS modules using 'bare module specifiers' like "import React from 'react'" and 'pin' them to their name
    - this doesn't work without importmap because you need to provide a local path or URL, the importmap_rails gem does the mapping for you
    - config is found in config/importmap.rb
      - but usually you'd use ./bin/importmap package_name to pin, unpin or update packages in your importmap
        - you can append --download to download the package to your vendor folder, rather than using a CDN in production
          - or --download to the unpin command
  - Can append preload: true to the pin to load it before the contents of the importmap
- They work best when you're using minimal 3rd party packages. Dependency management can be tricky as it'll lock dependencies for packages you use as the version required by that package, and adding subsequent packages which depend on different versions of that dependency will cause errors
- Also makes it more difficult to keep your packages up to date automatically
- Finally, it's not good for asset bundling as it can't transpile or bundle code, so you only want to use it when directly importing 3rd party code
- **Basically importmaps are the easy, default solution to including packages; if you need something more complex go back to using webpack** 

### Odin Project - Ruby on Rails - Turbo Drive
- Turbo Drive handles page navigation, it allows you to update your page without a full reload
  - defines page navigation as a visit to a location (URL) with an action
  - There are 2 kinds of visits
    - Application visit - a visit with a Drive action of advance or replace (set with data: { turbo_action: "replace/advance" })
      - Begins when a user clicks a TD enabled link (TD is enabled by default)
      - TD receives the HTTP request and renders the HTML
      - If possible, will be rendered using cache of a previous visit to the same URL
      - The browser history is updated to reflect the navigation
        - if an advance action, a new entry is added to the history
        - if a replace action, the previous entry is replaced by the new location
    - Restoration visit - a visit with a Drive action of restore, handles navigation with forward/back buttons (do not manually set an action of restore, TD does this internally)
      - Tries to render a copy of the page from browser cache, if unavailable retrieves a fresh copy
      - Saves scroll position before navigating away, and will return to that position if you return to the page
  - You can set a link to something other than a GET request using data: { turbo_method: "type of request" }
  - can set "data: { turbo: "true/false" }" to enable/disable
    - if on a parent container, will set for all children
    - but can be overridden by attributes on those children
- Forms
  - Turbo receives all form submissions by default, and expects to receive at HTTP status 303 (redirect) in return
    - will also accept a 4xx code which indicates you made a mistake with your data, or a 5xx code which indicates an internal error
    - responds to anything else, including a 2xx 'ok' request, by staying on the same page
- Turbolinks was the predecessor of Turbo, didn't work with form submissions but also allowed you to refresh the page by changing the content between the body tags

- [Turboframes](https://turbo.hotwired.dev/handbook/introduction)
  - Allow you to structure a page as a series of lazy loaded sections which can be refreshed independently and don't affect each other
  - You wrap these sections inside a turbo-frame element
    - if you add a src attribute to this element, the element will have its loading deferred and be filled by content from the src
  - Turbostreams does the same thing but updates automatically in response to an external resource changing

- Preloading
  - TD can preload links into its cache with "data-turbo-preload"



## Sun 16th
### Odin Project - Ruby on Rails - Form Basics
- Rails server output will tell you what a form submitted to your application
- If you just create your own form it won't work, you need a form authenticity token to protect you from cross-site requests
  - can manually add it to a form with "input type="hidden" name="authenticity_token" value="<%= form_authenticity_token %>""
  - automatically created by Rails when you use form_with
- If you wanna pass values from the form to params nested in a hash, just make the name attribute for those for elements something like hash_name[value_name]
- Basic structure for creating a form with helpers is form_with wrapping a bunch of tag helpers
  - IDs of inputs will also be their names
  - All forms are submitted by turbo drive by default so the whole page doesn't have to reload, if you want to cancel that set data: {turbo: false} on the form_with element
- Creating with a model is almost the same, just use form_with model: @model_name and pass |form| to the block
  - fields are generated in the block with "form.text_field :field_name" for example
  - when created this way, the form will automatically know if you're submitting a new or previously saved object and send it to create or update as appropriate
  - errors are displayed in a created div with class "field_with_errors"
  - can manually display them like
  ```
  <% if @post.errors.any? %>
    <div id="error_explanation">
      <h2><%= pluralize(@post.errors.count, "error") %> prohibited this post from being saved:</h2>

      <ul>
      <% @post.errors.full_messages.each do |msg| %>
        <li><%= msg %></li>
      <% end %>
      </ul>
    </div>
  <% end %>
  ```
  - can make your form submit a PATCH or DELETE rather then GET or POST using method: "path/delete" in the form_with options
    - you can also make a button in your form that has a different method to the overall form method by attaching the 'formethod: :method' option
  - the "unprocessable entity" bit in the controller ensures your server returns a 400 error rather than 200, which would cause no response
  - Rails has helpers for generating select boxes and checkboxes from your collections
  - You can do some really [funky stuff](https://guides.rubyonrails.org/form_helpers.html#understanding-parameter-naming-conventions) with the params hash like nesting hashes in an array or allowing a user to insert multiple phone numbers in an array



## Mon 17th
### Odin Project - Ruby on Rails - Forms Project

#### What I did
- [x] Created the 're-former' app
- [x] Added MVC for User
- [x] Create a HTML form, without the Rails helpers
  - [x] pass values to params hash as a hash
  - [] build the #create controller method
    - [] filter with user_params private method (on #new)
- [] Change the form to use Rails form_tags (maybe save the old version somewhere for comparison)
- [] Create it one final time using form_with and the model
  - [] allow the form to also update users
  - [] show any errors at the top of your form



## Tues 18th
### Odin Project - Ruby on Rails - Forms Project

#### What I did
- [x] Create a HTML form, without the Rails helpers
  - [x] pass values to params hash as a hash
  - [x] build the #create controller method
    - [x] filter with user_params private method (on #new)
- [x] Change the form to use Rails form_tags (saved other versions in branches)
- [x] Create it one final time using form_with and the model
  - [x] allow the form to also update users
  - [x] show any errors at the top of your form


#### What I learned
- Form_with bound to a model is wayyyyy easier than the other ways of making a form


## Wed 19th
### Odin Project - Ruby on Rails - [Sessions, Cookies and Authentication](https://www.theodinproject.com/lessons/ruby-on-rails-sessions-cookies-and-authentication)
**Both sessions and cookies are treated like hashes, but they're not really hashes. Also size limited to 4kb (ideally you wanna make them much smaller than that tho ). if no expiry is specified, they expire when browser is closed**
- Sessions
  - **Store references to objects in sessions, not the object itself**
  - Sessions are similar to cookies, but a session is stored as a single tamper-proof hash rather than a separate cookie for each key/value
    - by default decrypts to JSON, but you can change this and also regenerate a new key 
  - works basically the same as a regular hash, but reset_session will... reset the session
  - sessions expire when the browser is closed by default, but you can set other expiry times
  - handled by a sessions controller
    - usually has new, create and destroy routes
    - credentials checked with an #authenticate
  - Storing actual data in cookies opens you up to a lot of problems, like:
    - cookie sniffing, where attackers can intercept cookies if not over HTTPS
    - replay attacks, where the same cookie is submitted over and over to infinitely increase a resource 
  - Alternative methods of storing sessions include in ActiveRecord, Redis or MemCache
    - you send only the sessionID to the cookie, all other session info lives in your table
      - you can change this by changing the gem used for session_store in config to :active_record_store and use of activerecord-session_store gem and creating a table with "rails g active_record:session_migration"
      - keep in a db if you want it to persist
        - but not cleaned up automatically, and might be privacy/legal concerns
      - keep in cache for speed and you don't mind sessions potentially expiring early so much
        - sessions will have to compete for space with normal cached data 
  - Sessions are lazy loaded, so you'll never need to disable them, just don't use them

- Cookies
  - Key/value pairs stored in the browser until a specified expiration date
  - Can be used for many things, but not for anything that needs to be secure or persist across browser sessions
  - Rails deals with cookies by giving you cookies hash, where each key/value pair is stored as a separate cookie in the browser
    - save with cookies[:key] = value
    - delete with cookies.delete(:key)
    - cookies are included in each request to your server, and can be accessed in controllers/views like a normal hash
    - expiration dates can be set like "cookies[:name] = { value: "cookies YUM", expires: Time.now + 3600}"
  - To stop people stealing your cookies, use HTTPS
    - config.force_ssl = true in config/environments/production.rb 

- Flashes
  - A flash persists only from one request to the next, like a session hash that self-destructs when opened
  - commonly used to send messages from the controller to the view so user can see success/failure messages for forms
  - remember Flash.now[] if you want to display the error on the current view

- Controller filters
  - Runs code (usually to check the action a user is trying to take is allowed) before a specified action (but goes at the top and is limited by options)
  - e.g. "before_action" will run a check before any of the controller code is called. All _action methods accept a block as well, not just another method to run
    - after_action runs after a successful action and will have access to the result
    - around_action runs the associated actions by yielding
  - can use only/accept [symbols for the actions you want it to check] to limit it to/exclude those actions from checking
  - make your filters private
  - they're inherited, so if you want a filter to apply to every action put it in application_controller.rb

- Authentication
  - Don't store passwords in plaintext lol
    - instead store as a 'password digest' and compare that to the password digest created when a user submits their password in a form
    - digests are one way encryption, ez to encrypt a string to digest form but difficult to decrypt a digest to a string
  - adding #has_secure_password to your User model will intercept password and password confirmation values without persisting them, then convert them to digests and compare with the database
  - to remember users between sessions (like the remember me check box) you add a col to your users table for an encrypted token representing the user, then drop the unencrypted token as a string into the user's browser as a cookie with cookies.permanent
    - best practice to reset the token on sign in if the user signs out
  - Commonly used helper methods are signing in a user, checking if they're signed in and comparing them to another user (e.g. if they look at a profile page should they be able to edit it or not)
- Generic overview for adding auth
  1. Add a column to your Users table to contain the user’s password_digest.
  2. When the user signs up, turn the password they submitted into digest form and then store THAT in the new database column by adding the has_secure_password method to your User model.
  3. Don’t forget any necessary validations for password and password confirmation length.
  4. Build a sessions controller (and corresponding routes) and use the #authenticate method to sign in the user when the user has submitted the proper credentials using the signin form.
  5. Allow the user to be remembered by creating a remember_token column in the Users table and saving that token as a permanent cookie in the user’s browser. Reset on each new signin.
  6. On each page load that requires authentication (and using a #before_action in the appropriate controller(s)), first check the user’s cookie remember_token against the database to see if he’s already signed in. If not, redirect to the signin page.
  7. Make helper methods as necessary to let you do things like easily determine if a user is signed in or compare another user to the currently signed in user.

- Devise
  - Gem that handles auth for you, almost always better than rolling your own auth as it handles a lot of edge cases you haven't thought of
  - Also ez integration with OAuth etc
  - Basically packages a bunch of sign-in/up forms and methods to help implement them
  - Made up of 10 modules, you can choose which to use
  - Will need to run a db:migrate after install to add the extra cols to your User table
  - Modules do things like allow you to require email confirmation, or make passwords recoverable


## Thurs 20th
### Odin Project - Ruby on Rails - [Members Only Project](https://www.theodinproject.com/lessons/ruby-on-rails-members-only)

#### What I did
- [x] Plan/create models for users and posts
- [x] Add and install Devise
- [x] Restrict access to Posts #new and #create to only logged in users
- [x] Set up the #new action
  - [x] set up a form to create new posts
  - [x] show current user's name on new post page
- [x] set up the #create action with auto-populated user id
- [] Display author name (in index view) only if user is signed in
- [] Styling
  - [] for the index, have a list of actions in a sidebar on the left
  - [] when you click on a post, the sidebar instead becomes populated with the index of posts and the clicked on post expands to fill the remaining space (show view)
  - [] make notices a green or red box that fades out over a period of time then becomes hidden (on a higher z-axis so it doesn't shift content)

#### What I learned
- You can't use validates_associated on anything that has a confirmation field, those aren't stored in the table so it'll say it's invalid despite being successfully saved
- Devise has some issues with Turbo, either generate the views and disable Turbo on all Devise forms or follow the instructions [here](https://gorails.com/episodes/devise-hotwire-turbo)
  - but you need to create the turbo_controller in the controllers folder, not just put it in the Devise config file. Otherwise you get a nameerror for ApplicationController
- Remember you can generate a controller, model and routes all at once with 'rails generate resource Name col:type col:type etc...'
- Probably best to generate model with Devise first, then add any extra fields you need to the migration file. Otherwise you end up with dup fields for email, pwd etc.
- You can auto-add current user's id by using "current_user.posts.new(post_params)", just like you would in rails console, in the #create action
- **Git 'bad object' errors can be caused by a 2 randomly being added to a file in git. If that occurs, renaming that file to remove the random 2 allows the error to be resolved**


## Fri 21st
### Odin Project - Ruby on Rails - Members Only Project

#### What I did
- [x] Display author name (in index view) only if user is signed in
- [] Styling
  - [x] figure out why it's printing a list of all the post objects in the index view
    - it was because I had an = on the tag for @posts.each, so it was displaying the return value
  - [x] style global layout
    - [x] header with site name centered
    - [x] drop shadow marking transition to body of the page
    - [x] style the sidebar
      - [x] for the index, have a list of actions like new post, sign in, sign up
      - [x] for the show view, instead becomes populated with the index of posts and the clicked on post fills the main tag
      - [x] fix the sign out button (delete method not being sent for some reason)
        - see "what I learned" section for solution
  - [] make notices a green or red box that fades out over a period of time then becomes hidden (on a higher z-axis so it doesn't shift content)
  - [] add details to make stuff pretty
    - [] gradient on the sidebar
    - [] revisit the sidebar expanding and hiding (maybe use :hover?)

#### What I learned
- Devise helpers like "user_signed_in?" can be used in your views as well, not just controllers
- If you wanna make an image a link in rails you can go "link_to image_tag(""), _path" inside the erb bit
- Devise and Rails have a problem where using the destroy session path sends a get method rather than a delete method
  - tried manually setting the method to delete on the link, that didn't work
  - found the solution [here](https://chimkan.com/rails-7-and-devise-issue-with-sign-out/), it's a turbo-related issue. Rather than just method: delete, you need to set "data: {turbo_method: :delete}"


## Sat 22nd
### Odin Project - Ruby on Rails - Members Only Project
- Project requirements are finished, so I'll just keep doing this from time to time as a break from reading

#### What I did
- [] Styling
  - [] make notices a green or red box that fades out over a period of time then becomes hidden (on a higher z-axis so it doesn't shift content)
  - [x] Index page
    - [x] scrollable, responsive grid of posts on index page
    - [x] figure out what to set list container height as to stop it clipping posts (see what I learned section)
  - [] Sidebar
    - [] gradient on the sidebar
    - [] make post list scrollable
    - [] revisit the sidebar expanding and hiding (maybe use :hover?)
  - [] Forms
    - [] center them
    - [] add some kind of styling to the input fields (:valid and :invalid)
    - [] figure out how to make all the tiny links below the form readable (or go into Devise and remove them since they're not needed)
  - [] Show view
    - [] style the article
    - [] add delete, edit buttons if current_user == post.user


#### What I learned
- Scroll needed to be set on the main element, not the list container
  - setting grid-auto-rows to 1fr fixed the differently sized boxes with only a little text


### Odin Project - Ruby on Rails - [Installing PostgreSQL](https://www.theodinproject.com/lessons/ruby-on-rails-installing-postgresql)
- Environments & Pipelines
  - 4 main environments are dev, test, staging and prod, grouped in the production pipeline
    - dev: safely make changes, usually on dev's local machine, without impacting users
    - test: uses different tools and settings (like increased logging) to identify bugs with automated testing
    - staging: mirrors prod but deployments are not public
    - prod: user-facing
- [Environment Variables](https://www.rubyguides.com/2019/01/ruby-environment-variables/)
  - key/value pairs
  - Environment variables aren't permanent, when you reboot your computer, or even when you close your terminal, changes to environment variables are lost
  - list all environment variables with env
    - access them within Ruby with ENV.[ "key" ]
    - or a list with ENV.keys
  - set a new ENV variable in cmd using "export API_KEY=1"
  - Only accessible in a given environment
  - Used so that when you push your code to Github etc. it doesn't have any sensitive info
  - Rails has a RAILS_ENV environment variable it looks for, and if not found it assumes it's in a dev environment
- PostgreSQL
  - check if active with "brew services info postgresql@14"
  - need to restart after updating with "brew services restart postgresql@14"
  - your role should be your username, and you need to create a db to match it
  - open the console?? with "psql postgres" (just psql once you set up your role)
    - quit with \q
  - ENV for password is DATABASE_PASSWORD
  - can make a new Rails app using pg with "rails new < app_name > --database=postgresql"
    - set it up by going to database.yml and adding the following code, then rails db:create
    ```
    default: &default
      adapter: postgresql
      encoding: unicode
      # For details on connection pooling, see Rails configuration guide
      # http://guides.rubyonrails.org/configuring.html#database-pooling
      pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
      +  username: <role_name> # role previously added
      +  password: <%= ENV['DATABASE_PASSWORD'] %> # variable previously added
    ```


## Sat 22nd
### Odin Project - Ruby on Rails - Members Only Project

#### What I did
- [] Styling
  - [] make notices a green or red box that fades out over a period of time then becomes hidden (on a higher z-axis so it doesn't shift content)
  - [] Sidebar
    - [] gradient on the sidebar
    - [] make post list scrollable
    - [] revisit the sidebar expanding and hiding (maybe use :hover?)
  - [] Forms
    - [] center them
    - [] add some kind of styling to the input fields (:valid and :invalid)
    - [] figure out how to make all the tiny links below the form readable (or go into Devise and remove them since they're not needed)
  - [] Show view
    - [] style the article
    - [] add delete, edit buttons if current_user == post.user


#### What I learned
- 


### Odin Project - Ruby on Rails - [Active Record Queries](https://www.theodinproject.com/lessons/ruby-on-rails-active-record-queries)
- 
