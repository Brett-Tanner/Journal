# February 2023
## Feb 1st

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)
#### What I did
- [x] Demo stuff
    - [x] Add images to the time slots
        - [x] Left align options
    - [x] Style the result box when finding a child by SSID and bday
        - [x] Only show the kid's name and SSID here to reduce potential fears of info being exposed
        - [x] Move add child functionality into the add children box on User#show, change edit button back to just edit but keep ability to add child
    - [x] Add error display to all forms
    - [x] Kids should be more distinct
    - [x] For slots, AM and PM need to be linked
    - [x] Sign up form
        - [x] No english name
        - [x] Separate out address
    - [x] Photo service is an option for the whole event, probably need to make options polymorphic
    - [x] Make arrival/departure time options mutually exclusive (select boxes?)
        - They currently have no way of being deleted, but we'll ignore that for now

- [] Change all date fields to be YY/MM/DD (maybe will be done automatically by I18n??)
    - [] Allergies need to be two columns, boolean for has one or not and info about the allergy
- [] Event_children/time_slot_children rework
    - [] Don't need not attending list
    - [] Should just be info, click on child name to change stuff
    - [] Add a cost placeholder (maybe just num of slots * 8000 for now)
        - [] Button to cost breakdown which pops up an overlay
    - [] Regular days, photo status, allergy or not (if allergy, click on it for more info)
    - [] On event_children, each slot needs to show if they're attending, their arrival/departure times and what meals they're having
    - [] For time slot children, should just look exactly like the printable one

- [] Make flash notices pretty
    - [] Make them little notification bubbles floating above the nav bar
    - [] Fade/slide them in from left, fade/slide out to top
- [] Add notifications
- [] Add a way of calculating the cost for an event, probably requires implementing a Course model

- Bugfixes/Requested Features
    - [] 



## Feb 2nd

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)
#### What I did
- [x] Demo stuff
    - [x] Write an example systems test for the sign up page

- [] Change all date fields to be YY/MM/DD (maybe will be done automatically by I18n??)
    - [] Allergies need to be two columns, boolean for has one or not and info about the allergy
- [] Event_children/time_slot_children rework
    - [] Don't need not attending list
    - [] Should just be info, click on child name to change stuff
    - [] Add a cost placeholder (maybe just num of slots * 8000 for now)
        - [] Button to cost breakdown which pops up an overlay
    - [] Regular days, photo status, allergy or not (if allergy, click on it for more info)
    - [] On event_children, each slot needs to show if they're attending, their arrival/departure times and what meals they're having
    - [] For time slot children, should just look exactly like the printable one

- [] Make allergy or not a boolean, then have allergy details as a separate column
- [] Make flash notices pretty
    - [] Make them little notification bubbles floating above the nav bar
    - [] Fade/slide them in from left, fade/slide out to top
- [] Add notifications
- [] Add a way of calculating the cost for an event, probably requires implementing a Course model
- [] Set up notifications


## Feb 3rd

DEMO DAY!


#### What I learned
- I don't need to change the date format in the forms, user's browser does that for them


## Feb 5th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)
#### What I did
- [x] Setup main laptop so I can do work project on it
- [x] Setup ActiveStorage

- [] Change all date fields to be YY/MM/DD (maybe will be done automatically by I18n??)
    - [] Allergies need to be two columns, boolean for has one or not and info about the allergy
- [] Event_children/time_slot_children rework
    - [] Don't need not attending list
    - [] Should just be info, click on child name to change stuff
    - [] Add a cost placeholder (maybe just num of slots * 8000 for now)
        - [] Button to cost breakdown which pops up an overlay
    - [] Regular days, photo status, allergy or not (if allergy, click on it for more info)
    - [] On event_children, each slot needs to show if they're attending, their arrival/departure times and what meals they're having
    - [] For time slot children, should just look exactly like the printable one

- [] Make allergy or not a boolean, then have allergy details as a separate column
- [] Make flash notices pretty
    - [] Make them little notification bubbles floating above the nav bar
    - [] Fade/slide them in from left, fade/slide out to top
- [] Add notifications
- [] Add a way of calculating the cost for an event, probably requires implementing a Course model
- [] Set up notifications\



## Feb 6th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)
#### What I did

- [x] Make allergy or not a boolean, then have allergy details as a separate column
- [x] Remove costs from time slots
- [x] Clean up tests after the move to options being polymorphic

- [] Cost rework
    - [] Add ability to select time slots from list and have them appear at the bottom of the event page
    - [] Add a way of calculating the total cost for an event, probably requires implementing a Course model and some JS

- [] Event_children/time_slot_children rework
    - [] Don't need not attending list
    - [] Should just be info, click on child name to change stuff
    - [] Add a cost placeholder (maybe just num of slots * 8000 for now)
        - [] Button to cost breakdown which pops up an overlay
    - [] Regular days, photo status, allergy or not (if allergy, click on it for more info)
    - [] On event_children, each slot needs to show if they're attending, their arrival/departure times and what meals they're having
    - [] For time slot children, should just look exactly like the printable one

- [] Implement notifications

- Bugfixes/Requested Features
    - [x] Correctly order Event#index



## Feb 7th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)
#### What I did

- [] Email confirmation as well as password
- [] Send a confirmation email when people sign up
- [] Implement forgot password process

- [] Event_children/time_slot_children rework
    - [] Should just be info, click on child name to change stuff
    - [] Add a cost placeholder (maybe just num of slots * 8000 for now)
        - [] Button to cost breakdown which pops up an overlay
    - [] Regular days, photo status, allergy or not (if allergy, click on it for more info)
    - [] On event_children, each slot needs to show if they're attending, their arrival/departure times and what meals they're having
    - [] For time slot children, should just look exactly like the printable one

- [] Cost rework
    - [x] Scaffold what the new version will look like
        - [x] Create a link between AM and PM slots of the same day (foreign key)
    - [] Add ability to select time slots from list and have them appear at the bottom of the event page
    - [] Add a way of calculating the total cost for an event, probably requires implementing a Course model and some JS
        - Have the total cost saved in a model that belongs to both an event and a parent
        - Update it whenever you do a big submit/change anything else that would effect it
            - For the live total, just calculate with JS?

- [] Implement notifications

- Bugfixes/Requested Features
    - [] 



## Feb 8th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)
#### What I did

- [] Email confirmation as well as password
- [] Send a confirmation email when people sign up
- [] Implement forgot password process

- [] Event_children/time_slot_children rework
    - [] Should just be info, click on child name to change stuff
    - [] Add a cost placeholder (maybe just num of slots * 8000 for now)
        - [] Button to cost breakdown which pops up an overlay
    - [] Regular days, photo status, allergy or not (if allergy, click on it for more info)
    - [] On event_children, each slot needs to show if they're attending, their arrival/departure times and what meals they're having
    - [] For time slot children, should just look exactly like the printable one

- [] Cost rework
    - [] Add ability to select time slots from list and have them appear at the bottom of the event page
    - [] Add a way of calculating the total cost for an event, probably requires implementing a Course model and some JS
        - Have the total cost saved in a model that belongs to both an event and a parent
        - Update it whenever you do a big submit/change anything else that would effect it
            - For the live total, just calculate with JS?

- [] Implement notifications

- Bugfixes/Requested Features
    - [] 


#### What I learned
- 