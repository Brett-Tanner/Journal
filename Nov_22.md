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
- 
