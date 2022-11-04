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
