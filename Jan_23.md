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
    - [x] Associations with Registration
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