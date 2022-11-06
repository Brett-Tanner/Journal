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
- 