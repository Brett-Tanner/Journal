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
  - if you use ':references' when generating, the new model will belong to the model prior
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
- [] Plan out the micro-reddit models


#### What I learned









### Odin Project - Ruby Foundations
- When making a move
    - 

- When checking for checkmate
    - 