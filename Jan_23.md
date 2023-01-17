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
- [] Allow parents to add new/existing children on their profile

#### What I learned
- 