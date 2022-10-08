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
- [] Style the other pages to match
- [] Figure out why the comment count text is so annoying to make scale with its image

#### What I learned
- 















### Odin Project - Ruby Foundations
- When making a move
    - 

- When checking for checkmate
    - 