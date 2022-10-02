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
        - #all on the db returns all records in the db as an ActiveRecord::Relation object, which is basically a super array

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


#### What I learned







### Odin Project - Ruby Foundations
- When making a move
    - 

- When checking for checkmate
    - 