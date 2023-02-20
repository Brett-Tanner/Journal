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

- [] Add Invoices
    - [x] Belongs to an Event and User
    - [x] Has many registrations, invoice has the billing date/added to SS/paid that registrations previously had
        - [x] So add an invoice FK to registrations
    - [] Add the courses to Events as JSON
        - [] Calculate invoice cost by using the event's course JSON for the Child's category with the number of linked registrations, than adding the cost of the registered options
    - [] Need to be able to merge invoices by moving registrations from one to another

- [] Event_children/time_slot_children rework
    - [x] Scaffold info/cost, click on child name to change stuff
    - [x] On event_children, each slot needs to show if they're attending, their arrival/departure times and what meals they're having
    - [x] Include regular days, photo status, allergy or not
    - [] For time slot children, should just look exactly like the printable one

- [] Event booking rework
    - [] Add ability to select time slots from list and have them appear at the bottom of the event page
    - [] When you register for those time slots, it adds the registration to the invoice form in the bar at the bottom
        - Submitting the invoice form creates all the associated registrations along with the invoice
        - Will need some way to check for duplicate registrations, probably unable to do it on frontend and a backend check
    - [] Have running total for the invoice calculated in real time by JS (validated by the DB calculation when submitted)

- [] Implement notifications
    - [] Need a link, message, read/unread boolean
    - [] Not live, can be displayed when page is refreshed
    - [] Automatically created on certain actions
        - 


## Feb 9th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)
#### What I did

- [] Email confirmation as well as password
- [] Send a confirmation email when people sign up
- [] Implement forgot password process

- [] Add Invoices
    - [x] Write tests for the basic Invoice model
    - [x] Add the courses to Events as JSON
        - [x] Price list model with courses as a JSON hash, category as enumerable (member/non-member), name
        - [x] Foreign key for member/non-member price lists on event
        - [x] Test basic model functionality
    - [] Calculate invoice cost using PriceList, number of registrations, option costs and any adjustments
    - [] Need to be able to merge invoices by moving registrations from one to another

- [] Event_children/time_slot_children rework
    - [] For time slot children, should just look exactly like the printable one

- [] Event booking rework
    - [] Add ability to select time slots from list and have them appear at the bottom of the event page
    - [] When you register for those time slots, it adds the registration to the invoice form in the bar at the bottom
        - Submitting the invoice form creates all the associated registrations along with the invoice
        - Will need some way to check for duplicate registrations, probably unable to do it on frontend and a backend check
    - [] Have running total for the invoice calculated in real time by JS (validated by the DB calculation when submitted)

- [] Implement notifications
    - [] Need a link, message, read/unread boolean
    - [] Not live, can be displayed when page is refreshed
    - [] Automatically created on certain actions
        - 

- Bugfixes/Requested Features
    - [] Autofill address from post code
        - [] Move postcode to the left, so it's at the start of address fields


## Feb 10th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

Got nothing of substance done, time wasted by dumb setsumeikai prep then cleaning


## Feb 11th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)
#### What I did

- [] Add Invoices
    - [] Calculate invoice cost using PriceList, number of registrations, option costs and any adjustments
        - [x] Test for just registrations
        - [] Test with options and adjustments
    - [] Update the cost breakdown when new total cost is calculated
    - [] Need to be able to merge invoices by moving registrations from one to another

- [] Event_children/time_slot_children rework
    - [] For time slot children, should just look exactly like the printable one

- [] Event booking rework
    - [] Add ability to select time slots from list and have them appear at the bottom of the event page
        - Probably do this by rendering them then toggling their display status with JS?
        - When they go to the event page it loads their current invoice if not paid, new one if not paid
    - [] When you register for those time slots, it adds the registration to the invoice form in the bar at the bottom
        - Submitting the invoice form creates all the associated registrations along with the invoice
        - Will need some way to check for duplicate registrations, probably unable to do it on frontend and a backend check
    - [] Have running total for the invoice calculated in real time by JS (validated by the DB calculation when submitted)

- [] Implement notifications
    - [] Need a link, message, read/unread boolean
    - [] Not live, can be displayed when page is refreshed
    - [] Automatically created on certain actions
        - 

- Bugfixes/Requested Features
    - [] Autofill address from post code
        - [] Move postcode to the left, so it's at the start of address fields
    - [] Email confirmation as well as password
    - [] Send a confirmation email when people sign up
    - [] Implement forgot password process



## Feb 12th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)
#### What I did

- [] Add Invoices
    - [] Calculate invoice cost using PriceList, number of registrations, option costs and any adjustments
        - [x] Test with options 
        - [] Change adjustments to be on invoices and test including them in calculations
    - [] Update the cost breakdown when new total cost is calculated
    - [] Need to be able to merge invoices by moving registrations from one to another


#### What I learned
- Since we're using a separate account for the app to the main site, the main site account will need to add us to the Route 53 records like [this](https://medium.com/shelf-io-engineering/aws-route53-how-to-share-subdomains-with-multiple-aws-accounts-ad002c77be76)


## Feb 14th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### Time spend
- At work
    - 12-13
    - 14-14:25
    - 19:30-20:00
- At home
    - 24:00-1:15


#### What I did

- [] Add Invoices
    - [x] Calculate invoice cost using PriceList, number of registrations, option costs and any adjustments
        - [x] Change adjustments to be on invoices and test including them in calculations
        - [x] Figure out how coupons should relate to invoices/adjustments and test that
    - [x] Update the cost breakdown when new total cost is calculated
    - [] Need to be able to merge invoices by moving registrations from one to another

- [] Event_children/time_slot_children rework
    - [] For time slot children, should just look exactly like the printable one

- [] Event booking rework
    - [] Add ability to select time slots from list and have them appear at the bottom of the event page
        - Probably do this by rendering them then toggling their display status with JS?
        - When they go to the event page it loads their current invoice if not paid, new one if not paid
    - [] When you register for those time slots, it adds the registration to the invoice form in the bar at the bottom
        - Submitting the invoice form creates all the associated registrations along with the invoice
        - Will need some way to check for duplicate registrations, probably unable to do it on frontend and a backend check
    - [] Have running total for the invoice calculated in real time by JS (validated by the DB calculation when submitted)

- [] Implement notifications
    - [] Need a link, message, read/unread boolean
    - [] Not live, can be displayed when page is refreshed
    - [] Automatically created on certain actions
        - 

- Bugfixes/Requested Features
    - [] Autofill address from post code
        - [] Move postcode to the left, so it's at the start of address fields
    - [] Email confirmation as well as password
    - [] Send a confirmation email when people sign up
    - [] Implement forgot password process



## Feb 15th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- [] Add Invoices
    - [] Cost break down needs list of courses and all options in one place
    - [] Kindy spot use has a different price if full day
        - Only relevant if full day registrations are more than the nearest full course
        - Leroy's function needs full days and the number of regs covered by the course
        - Overall flow of calculation:
            - 
    - [] Tidy the whole thing up and split it into separate methods for each section
    - [] Need to be able to merge invoices by moving registrations from one to another
    - [] Need a request change button on the old, paid invoices

- [] Event_children/time_slot_children rework
    - [] For time slot children, should just look exactly like the printable one

- [] Event booking rework
    - [x] Scaffold the new layout
    - [] When you register for time slots, it adds the registration to the invoice form in the bar at the bottom
        - [] If already registered on current invoice, slots should be outlined green and in a different section
    - [] Use current invoice if it exists/is not closed, otherwise use a new invoice
        - [] Grey out slots if registered for in previous invoice
        - [] Put a link to that invoice on greyed out slots (separate for each child)
    - [] Have running total for the invoice calculated in real time by JS (validated by the DB calculation when submitted)

- [] Implement notifications
    - [] Need a link, message, read/unread boolean
    - [] Not live, can be displayed when page is refreshed
    - [] Automatically created on certain actions
        - 

- Bugfixes/Requested Features
    - [] Autofill address from post code
        - [] Move postcode to the left, so it's at the start of address fields
    - [] Email confirmation as well as password
    - [] Send a confirmation email when people sign up
    - [] Implement forgot password process


#### What I learned
- When eager loading images from ActiveStorage, you can use #with_attached_#{name of association}



## Feb 16th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- [] Add Invoices
    - [x] Cost break down needs list of courses and all options in one place
    - [x] Kindy spot use has a different price if full day
        - Only relevant if no courses used
    - [x] Compartmentalize Invoice#calc_cost
        - Stuff to calculate:
            - Course cost
                - If children are both members/not, calculate all slot registrations together
                - If different, calculate separately then add together
                - Total cost/number in child summary and in overall summary put the courses used/cost for each
                    - If kindy and full days are more than half the total of courses selected, they need to pay 184 yen extra per full day 
            - Option cost
                - Sum up all the options for each child
                    - Event options go in child summary, slot options go under their slot
                    - They also go in the overall summary
            - Adjustments
                - Apply non-member repeater discount if eligible
                - Apply hat fee if child needs hat
                - Apply any other manual adjustments
                - Discount by 184yen if dumb cost is not 0 and the special day is a full day
                - List them all in the overall summary
    - [] Need to be able to merge invoices by moving registrations from one to another
    - [] Need a request change button on the old, paid invoices

- [] Event_children/time_slot_children rework
    - [] For time slot children, should just look exactly like the printable one

- [] Event booking rework
    - [] When you register for time slots, it adds the registration to the invoice form in the bar at the bottom
        - [] If already registered on current invoice, slots should be outlined green and in a different section
    - [] Use current invoice if it exists/is not closed, otherwise use a new invoice
        - [] Grey out slots if registered for in previous invoice
        - [] Put a link to that invoice on greyed out slots (separate for each child)
    - [] Have running total for the invoice calculated in real time by JS (validated by the DB calculation when submitted)

- [] Implement notifications
    - [] Need a link, message, read/unread boolean
    - [] Not live, can be displayed when page is refreshed
    - [] Automatically created on certain actions
        - 

- Bugfixes/Requested Features
    - [] Autofill address from post code
        - [] Move postcode to the left, so it's at the start of address fields
    - [] Email confirmation as well as password
    - [] Send a confirmation email when people sign up
    - [] Implement forgot password process


#### What I learned
- Apparently you can pass count an arbitrary block specifying a condition to count by, despite there not being anything about that in the rails docs
    - Oh it's just the Array#count
    - fuck me that's annoying, wish they'd come up with different names for stuff like select/count but can definitely see why they didn't


## Feb 17th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- Bugfixes/Requested Features
    - [] Autofill address from post code
        - [] Move postcode to the left, so it's at the start of address fields
    - [x] Email confirmation as well as password
    - [x] Send a confirmation email when people sign up
    - [x] Lock access after 10 failed login attempts


## Feb 18th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- [] Implement notifications
    - [x] Create with message, read/unread boolean, link
        - Belongs to a User
        - Not live, can be displayed when page is refreshed
    - [] Test basic functionality
    - [] Automatically created on certain actions
        - 



## Feb 20th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- [] Event booking rework
    - [x] Add the relevant event price list/s to the page

- [x] Implement notifications
    - [x] Test basic functionality
    - [] Automatically created on certain actions
        - 


## Feb 21st

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- [] Add Invoices
    - [] Need to be able to merge invoices by moving registrations from one to another
    - [] Need a request change button on the old, paid invoices

- [] Event_children/time_slot_children rework
    - [] For time slot children, should just look exactly like the printable one

- [] Event booking rework
    - [x] Add the relevant event price list/s to the page
    - [] When you register for time slots, it adds the registration to the invoice form in the bar at the bottom
        - [] If already registered on current invoice, slots should be outlined green and in a different section
    - [] Use current invoice if it exists/is not closed, otherwise use a new invoice
        - [] Grey out slots if registered for in previous invoice
        - [] Put a link to that invoice on greyed out slots (separate for each child)
    - [] Have running total for the invoice calculated in real time by JS (validated by the DB calculation when submitted)

- [x] Implement notifications
    - [x] Test basic functionality
    - [] Automatically created on certain actions
        - 

- Bugfixes/Requested Features
    - [] Autofill address from post code
        - [] Move postcode to the left, so it's at the start of address fields

#### What I learned
- 