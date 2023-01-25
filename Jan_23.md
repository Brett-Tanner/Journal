# December 2022
## Jan 3rd

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)
#### What I did
- [] Tested registration associations
    - [x] To events
    - [x] To children
    - [] To time slots


## Jan 4th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)
#### What I did
- [x] Tested registration associations
    - [x] To time slots
    - [x] To everything else
- [x] Completely reworked the Area/School/Manager relationships to be has_many :through
    - [x] Tested Area
    - [x] Tested School
    - [x] Tested User
    - [x] Tested everything else

#### What I learned
- Has_one/belongs_to were going to cause problems down the line one way or another, whether it was the original inability the change managers or a future need to have multiple managers/managers to have multiple schools/areas
    - Moved to has_many :through instead to avoid these issues and create more room for added features


## Jan 5th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)
#### What I did
- [x] Edited migrations to simplify all the changes I had to make last night
- [x] Updated seeds.rb for all the new models I've added so far
- [x] Test management model
- [x] Add Option model
    - [x] Test its associations through registrations
- [x] Create SlotOptions model
    - [x] Test its associations
    - [x] Delete it and realise you need a one slot to many options relationship instead
- [] Test all option relationships with the new associations
    - [x] Associations from Option
    - [x] Associations with TimeSlot
    - [] Associations with Registration
    - [] Associations with Event
    - [] Associations with School
    - [] Associations with Child
    - [] Associations with Area

#### What I learned
- Rubocop doesn't like HABTM, so I guess I use :through for everything cos I must kill all the errors
- I think I can use the scope on registrations to get registered options for anything, but I'll have to check
    - If not, I'll need to set up associations for :registered_options and :available_options
    - Yeah we're going for an additional has_many :through model
    - Nope, needed less complexity, not more
- To be able tor register for options and show users what options they've chosen for a given time slot each option must be linked to a single time slot, not a collection of them


## Jan 6th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)
#### What I did
- [x] Test all option relationships with the new associations
    - [x] Associations with Registration
    - [x] Associations with Event
    - [x] Associations with School
    - [x] Associations with Child
    - [x] Associations with Area

#### What I learned
- Joins are very useful and I should really consider using them more in scopes/generally


## Jan 7th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)
#### What I did
- [x] Let children be created without parents so we can actually migrate data from the SS
- [] Figure out any extra fields I need from my call with Leroy/the resources he sent
- [] Add said fields
    - [x] Test new fields for Child
    - [] Test new scopes for Child
    - [x] Test new fields for Parent
    - [x] Update seed for both of them
- [] Add the backup models for User/Child
- [] Add Day and the through table RegularDay for children
- [] Add Adjustments for Registrations
- [] Create the User#show page
    - [] For customer
    - [] For SM
    - [] For AM
    - [] For Admin

#### What I learned
- First and family names need separate fields for clarity


## Jan 8th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)
#### What I did
- [x] Figure out any extra fields I need from my call with Leroy/the resources he sent
- [x] Add said fields
    - [x] Test new scopes for Child
    - [x] Test new fields for Event
    - [x] Test new fields for User    
    - [x] Test new fields for TimeSlot    
    - [x] Update seed for Child, TimeSlot & Event
- [] Add the backup models for User/Child
- [] Add Day and the through table RegularDay for children
- [] Add Adjustments for Registrations
- [] Create the User#show page
    - [] For customer
    - [] For SM
    - [] For AM
    - [] For Admin

#### What I learned
- We have coupons, which will need a variety of extra info probably
    - e.g. adjustments will need to know what coupon was used for them if any
    - Coupons will need to know if they can be combined, and a specific target if they have one


## Jan 10th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)
#### What I did
- [x] Add PaperTrail for User/Child, test its functionality
- [x] Add RegularSchedule for Child
- [x] Remove username from User as it's not necessary anymore
- [x] Add booleans to registrations to say if they've been confirmed (which means the confirmation email has been sent) and paid. Also add billing date.
- [x] Add Adjustment for Registration
- [x] Add numericality validations to all the stuff that should already have them
- [] Add Coupon
- [] Update seeds.rb with today's changes
- [] Create the User#show page
    - [] For customer
    - [] For SM
    - [] For AM
    - [] For Admin

#### What I learned
- If you wanna access a value on an associated model for validations, you can create a private method that returns that value
    - Cleaner way is to create some kind of validator class with the method comparing the two model values and include that, but a lot of effort for one validation


## Jan 11th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)
#### What I did
- [x] Add Coupon
- [x] Update seeds.rb with recent changes
    - PaperTrail doesn't need to be seeded
    - Regular Schedule
    - Adjustments
    - Coupons
- [x] Implement User filtering for the relevant parts of User#index
- [x] Figure out how to get the redirect to error pages working
- [] Create the User#show page

#### What I learned
- Use #create! for the seeds file or a lot of stuff fails silently
    - Also a lot of stuff was failing silently lol
- Just generate a controller if you need to direct to pages, it's a lot easier

- AR query optimisation
    - The optimisation I'm looking for to avoid making a million AR queries is #includes(:association), which loads the associated records together with the parents
    - Also use #select and #pluck to only get the fields you need
    - Use #size rather than #count to avoid querying the db again when you've already loaded the relation you wanna count


## Jan 12th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)
#### What I did
- [x] Set home page to User#show
- [x] Allow users/children controllers to accept nested attributes for children/registrations respectively
- [x] Create the User#show page
    - [x] Upcoming events (at the user's school, plus any their kid is attending at other schools)
    - [x] Registered time slots and their options
    - [x] Managed schools/areas if manager
- [x] Modify the sign up form so it's actually possible to sign up

#### What I learned
- AR query optimisation is hard and changes whenever the stuff you need to display does. I'm leaving that for after the prototype gets demoed


## Jan 13th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)
#### What I did
- [x] Create Event#show
    - [x] Add options to the TimeSlot partial
    - [x] Update the methods on Event to provide the children I actually need to find
    - [] Start thinking with turboframes
- [] Create Child partial
- [] Create Child#index
- [] Create Child#show
- [] Allow parents to add new/existing children on their profile

- [] Create the different versions of views for staff
    - Generally more optimised for long lists of kids/events etc., like a table or spreadsheet
    - Plus able to edit all the extra fields
- [] Make the 'children registered' counter on the event partial a link to the list of registered children
    - As Child#index but the event_id is passed as a param

#### What I learned
- Maybe have each slot/option registration "form" inside a turboframe so you're not jumping back to the top of the page when you hit it
    - Need to find out if turboframes render the frame corresponding to the controller the link goes to or where the controller redirects to after the action
    - Currently the links are going to Registration#create and #destroy respectively, so should I put the frames in them or can I have them redirect to a different partial with the frame in it?
        - Don't really want the frames to be on the full pages for those as staff need them, though could always make them hidden with CSS I guess??
        - Yes, it looks for the turbo_frame in the place the controller redirects it to
        - Having some issues with querySelector though? The frame appears after registering but isn't filled with any content
- Did not tick a lot of boxes today but I did a lot of thinking about how to set stuff up


## Jan 15th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)
#### What I did
- [x] Create Event#show
    - [x] Start thinking with turboframes
    - [x] Add all the necessary info to the registration partial
    - [] Adjust Event#show and User#show to accomodate these new fields (more of a spreadsheet layout but small)
        - [] Also add stuff like previous events, recent registrations etc.
    - [] Limit the number of records displayed on User/Event#show and add buttons to the full list (#index) for User/Event
- [] Allow parents to add new/existing children on their profile

- [] Create the different versions of views for staff
    - Generally more optimised for long lists of kids/events etc., like a table or spreadsheet
    - Plus able to edit all the extra fields
- [] Make the 'children registered' counter on the event partial a link to the list of registered children
    - As Child#index but the event_id is passed as a param



## Jan 16th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)
#### What I did
- [x] Create Event#show
    - [x] Adjust Event#show and User#show to accommodate these new fields (more of a spreadsheet layout but small)
        - [x] Adjust events/time slots to actually show what people might want to see
        - [x] Also add turboframes to _option so it updates in place
        - [x] Add labels for registrations in the time slots
        - [] Fix adjusted cost being the value for cost as per message I sent
    - [x] Add buttons to the full list (#index) of attending students for _event/_time_slot
    - [] Separate _registration into _registration and _unregistered
- [] Allow parents to add new/existing children on their profile

#### What I learned
- The turbo frame goes **inside** the conditional, or you spawn two with identical ids and weird stuff happens
- When passing variables to a rendered partial sometimes you need to use a locals hash, sometimes just an implied hash???
    - Maybe locals in controller and implied in the views?


## Jan 17th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)
#### What I did
- [x] Create Event#show
    - [x] Adjust Event#show and User#show to accommodate these new fields (more of a spreadsheet layout but small)
        - [x] Fix adjusted cost being the value for cost as per message I sent
    - [x] Separate _registration into _registration and _unregistered
    - [x] Clean up styling for registrations and add those see all buttons I keep forgetting
- [x] Add a title to Registrations#index
- [x] Get flash messages and the attending count updating with turboframes as well
- [] Allow parents to add new/existing children on their profile

#### What I learned
- I shouldn't hate on JS quite so much, especially with access to Stimulus. Both CSS and JS have things they're good at


## Jan 18th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)
#### What I did
- [x] Clean up Registration Controller using turbostream templates
- [] Allow parents/staff to add new/existing children on the parent's profile
    - [] Also let staff remove the children
- [] Allow staff to create new events
- [] Make flash notices pretty
    - [] Make them little notification bubbles floating above the nav bar
    - [] Fade/slide them in from left, fade/slide out to top

- Bugfixes/Requested Features
    - [x] User#index limited to 12 users
    - [x] Admin can delete self even though only one exists
    - [x] Stop customers escaping
    - [x] Scaffold School#index
    - [x] Scaffold Child#index
    - [x] Scaffold School#index

#### What I learned
- Turbo stream templates let you update all/some of the turboframes on a page as necessary
    - Just respond_to turbo_stream in the controller, and have an action.turbo_stream.erb file in your views with the stuff you wanna update
- Unless you're submitting a form, you'll need to specify format: :turbo_stream on the link to handle it as a turbo stream rather than html


## Jan 19th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)
#### What I did
- [] Allow parents/staff to add new/existing children on the parent's profile
    - [x] Figure out why the hell it's downloading the response rather than rendering it in the frames
    - [] Also let staff remove the children so they can be added to the correct parent
- [] Allow staff to create new events
- [] Make flash notices pretty
    - [] Make them little notification bubbles floating above the nav bar
    - [] Fade/slide them in from left, fade/slide out to top

- Bugfixes/Requested Features
    - []

#### What I learned
- Now that I moved the parent destroying children from dependent into a before_destroy, I can remove children from a parent using parent.children.delete(child)
    - And then add them to the correct parent
- Got nothing done during work cos of a long meeting with Leroy and dumb setsumeikai stuff
    - From the meeting, to prep for the demo I need to:
        - Fix the add kid form -__-
        - Change the registration index to show the order the kids registered in (just each with index and print the index), kid's name and the time slots they're attending (options below?? maybe a really minified timeslot partial somehow?)
        - Update my seeds file to manually set values that actually make sense
- It's best to use forms for submissions to register/add stuff, because a: that's how I know to do it and b: they use POST automatically adn c: easier to submit the params
    - I think the problem causing the random download was that my original request was a GET? So it thought I wanted a full page in return and downloaded that??? Will remain one of life's mysteries but it's fixed



## Jan 20th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)
#### What I did
- [x] Allow parents/staff to add new/existing children on the parent's profile
    - [x] Update the relevant bits of the page with the new child
- [x] Also let admins remove the children so they can be added to the correct parent

- [] Demo stuff
    - [x] Update seeds to stuff that actually makes sense rather than random values
    - [] Event registration index
        - [x] First 3 columns are an index and their two names
        - [] Remaining columns are all the time slots for that event, plus an indication of whether they're coming in the morning or afternoon
    - [] Decide what pages we're gonna show and make sure they look clean
        - [] User#show should list all the time slots, either vertically or horizontally scrolling



## Jan 23rd

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)
#### What I did
- [] Demo stuff
    - [x] Update seeds to stuff that actually makes sense rather than random values
    - [x] Event registration index
        - [x] Remaining columns are all the time slots for that event, plus an indication of whether they're coming in the morning or afternoon
        - [x] Split kids on event index into attending/not attending
        - [x] Currently need to refresh to move kids from/to attending/possible. Fix this with frames
    - [x] Decide what pages we're gonna show and make sure they look clean
        - [x] User#show should list 5 time slots, horizontally scrolling
        - [x] Event#show should list all the event's time slots, also horizontally scrolling
    - [] Focus on optimizing the pages we're gonna show, event children index is especially slow cos of partials rather than AR queries

- [] Allow staff to create new events
- [] Make flash notices pretty
    - [] Make them little notification bubbles floating above the nav bar
    - [] Fade/slide them in from left, fade/slide out to top

- Bugfixes/Requested Features
    - [x] Some buttons aren't updating when clicked on Event children index
    - [x] Can register multiple times if button not updated
    - [x] Need to update the PM option button too when a slot registration is deleted

#### What I learned
- Lots of initial reading on optimisation, combining queries as expected but also caching could be a really big help
    - [Lots of good resources here](https://blog.appsignal.com/2020/01/22/rails-is-fast-optimize-your-view-performance.html)
    - [Rails has built in caching](https://guides.rubyonrails.org/caching_with_rails.html) and there are also other options
    - [Kaminari](https://github.com/kaminari/kaminari) looks like a good option for pagination



## Jan 24th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)
#### What I did
- [] Demo stuff
    - [x] Style login and sign up pages
        - [x] Plus add some color to the whole app
        - [x] And do a styling pass on the pages linked to in the nav bar
    - [] Add the edit/user add child form cos they might want to see that rather than just claiming a kid
    - [] Add Child#timeslot_index
    - [] Focus on optimizing the pages we're gonna show, event children index is especially slow cos of partials rather than AR queries

- [] Allow staff to create new events
- [] Make flash notices pretty
    - [] Make them little notification bubbles floating above the nav bar
    - [] Fade/slide them in from left, fade/slide out to top

- Bugfixes/Requested Features
    - [x] Labels in _registration partial did not have unique ids
    - [x] _child needs to include hat and allergies

#### What I learned
- You can style alternating rows in a table using :nth-child and odd/even


## Jan 25th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)
#### What I did
- [] Demo stuff
    - [x] Add the edit/user add child form cos they might want to see that rather than just claiming a kid
        - [x] Style it for the partial/in place editing
        - [x] Update the user index to match other indexes, with edit links
    - [] Add Child#timeslot_index
        - [] Needs to show options
        - [] Arrival time
        - [] Maybe group by kindy/elementary?
    - [] Focus on optimizing the pages we're gonna show, event children index is especially slow cos of partials rather than AR queries

- [] Allow staff to create new events
- [] Make flash notices pretty
    - [] Make them little notification bubbles floating above the nav bar
    - [] Fade/slide them in from left, fade/slide out to top
- [] Add notifications
- [] Add a way of calculating the cost for an event, probably requires implementing a Course model

- Bugfixes/Requested Features
    - [x] Create Event list for staff
    - [x] Stop customers editing registration after payment
    - [x] Allow users to be edited on their profile 


#### What I learned
- 



## Jan 26th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)
#### What I did
- [] Demo stuff
    - [] Add Child#timeslot_index
        - [] Needs to show options
        - [] Arrival time
        - [] Maybe group by kindy/elementary?
    - [] Focus on optimizing the pages we're gonna show, event children index is especially slow cos of partials rather than AR queries

- [] Allow staff to create new events
- [] Make flash notices pretty
    - [] Make them little notification bubbles floating above the nav bar
    - [] Fade/slide them in from left, fade/slide out to top
- [] Add notifications
- [] Add a way of calculating the cost for an event, probably requires implementing a Course model

- Bugfixes/Requested Features
    - [] 


#### What I learned
- 