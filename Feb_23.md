# February 2023
## Feb 1st

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)
#### What I did
- [] Demo stuff
    - [] Add images to the time slots
        - [] Left align options
    - [] Style the result box when finding a child by SSID and bday
        - [] Move add child functionality into the add children box on User#show, change edit button back to just edit but keep ability to add child
        - [] Only show the kid's name and SSID here to reduce potential fears of info being exposed
    - [] Photo service is an option for the whole event, probably need to make options polymorphic

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



#### What I learned
- 