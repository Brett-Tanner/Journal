# August 2023

## August 3rd

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Chores

  - [x] Add Ojima's special day
  - [x] Add Oi and Kitashinagawa's special days
  - [] Add Shin-kawasaki's special day

- Features

  - [x] Give SMs a printable list of kids who need a hat (based on the hat adjustment, not received hat which is something different)
  - [] Finish off the event creation features so someone other than me can actually do it
    - [x] Add "Edit Event" button to event partial for admins
    - [] Event step
      - [x] Fix the infinite loop my old method of adding images was causing
      - [x] Gracefully handle redirects when the event can't be saved
      - [x] Allow event option creation in the event creation form (step 1)
      - [] pre-select the existing image in the form
      - [] Extend the 'all' option on event creation to allow specific schools to be selected
    - [] Time Slot step
      - [x] Automatically create default options (per morning/afternoon/category) when a time slot is created
      - [x] Automatically create afternoon slots for morning slots
        - Unless the morning slot is a special day
        - Can't create afternoon for special days here as there's no way to link them to a morning slot without an id yet
      - [x] Split slot creation as part of event creations into a separate view and redirect there from the controller if there's an event param
      - [] Allow slots to be edited individually from the index
        - [x] Add fields for the afternoon slot to the slot_fields partial (when rendered here)
        - [] Allow adding an afternoon slot manually if editing a special day
        - [] Allow custom options to be added/edited
        - [] Allow updating time slots with the same name for all events with the same name
      - [] pre-select the existing image in the form
    - [] Add a way of uploading images to the S3 bucket from the site
      - [] Upload to a specific folder based on purpose of image
      - [] Make sure large files work, they didn't the first time
    - [] Remove ability to destroy events from frontend when I'm done testing (no route for it)
    - [] Add a test event with the new flow (on dev env) and go through the whole app to see what needs changing to support having multiple events
      - Probably need some dummy registrations too
  - Stats page
    - [] Add school-specific pages for each of the existing stats
  - [] Figure out what needs to change to stop persisting a blank invoice when there are no unconfirmed invoices available for a child and someone looks at their registration page
  - [] Remove all references to the email template column, then remove the column
    - [] Split the User#show pages out into different pages for different roles
  - [] Have a way to stop sending emails when the event stops
  - [] Look into using our SES account/domain for the school emails to escape their 5000 email limit

## August 8th

### Odin Project - [Budgeting Site](https://github.com/Brett-Tanner/budgeting-site)

- [x] Plan out the basic features
  - On arrival loads your budget for that month from local storage, or prompts you to create/import one if you don't have one
  - Budgets should have your salary for that month and your saving goal
  - Parent object for everything is a user, user can have many budgets (monthly) and budgets have many expenses
  - Also allow for extra income from various things, but probably less prominent in UI cos it's less likely
  - Expenses/budget should have categories like food, transport, bills
  - Should be able to add expenses quickly from the main page
    - Either as a custom expense through a form
    - Or as a saved frequent expense by just clicking it/selecting from a dropdown
  - Display a (reverse) progress bar at the top of the home page showing how close you are to spending too much
  - Projected yearly savings/expenses etc. based on existing data
  - List of expenses for a given week or day
  - Export to JSON/CSV button
  - Use chart.js for
    - a pie chart of your expenses by category over the month
    - bar chart of your expenses by day/week
      - filterable by category?
- [x] Create base factory functions for users, budgets, frequent expenses and expenses

## August 9th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Chores

  - [x] Add Shin-kawasaki's special day
    - [x] exclude it from the different prices for Minami-machida/futatamagawa's summer festival
  - [x] Make requested changes to Oi and Kitashinagawa's
    - [x] Add the options they want (lunch on AM/PM and 2 period extension)
    - [x] Change all the hardcoded exceptions to use the new names
    - [x] Rename them
    - [x] Add the new photos
  - [x] Show minami-machida/futatamatagawa's (18, 21) summer festival day in the daily attendance (it's missing now)
  - [x] Add Rinkai's triple day
    - [x] Middle activity as an option
  - [x] Monzen
    - [x] The new days are alongside PM activities, but tag them morning cos it's easier
    - [x] Close afternoon slots for the existing activities, and move the kids registered for them to the new activity on that day
  - [x] Add special days for Ikegami, Magome, Nagahara, Todoroki & Toyocho
    - [x] Actually create all those on live
  - [x] Add the TY coupon and update translation on button
    - [x] Get leroy the list of people eligible for the coupon

## August 10th-14th

Obon Holiday in Hokkaido!

## August 15th

### Odin Project - [ToDo List](https://github.com/Brett-Tanner/odin-todo)

- Create factories for
  - [x] ToDos with
    - title
    - description
    - due date
    - priority
    - notes (like comments)
    - checklist (interactive)
  - [x] Projects which group ToDos, default project called "Misc"
  - [x] Checklists
    - Completed boolean
    - Step description
- UI
  - [x] Homepage has
    - [x] all todos (sorted by due date)
    - [x] list of projects
    - [x] ability to add a todo
    - [x] ability to add a project
  - [] Project pages showing all todos for a project
    - Activated by clicking on the project from the sidebar nav
    - Replaces the content of the main, renders using the todo list of the project and listTodos from todoComponents
  - Individual todos have
    - [x] Their title and due date, as well as the description by default
    - [x] Different colors for different priorities
    - [x] Edit, delete, view notes, view checklist and view description buttons
- Functionality
  - [] Can click a button to add new todos
  - [] And to add new projects
- [] Build out the localStorage capability

## August 16th

### Odin Project - [ToDo List](https://github.com/Brett-Tanner/odin-todo)

- UI
  - Shared components for
    - [x] Modal
    - [x] Form
      - [] Project Fields
      - [] Todo Fields

## August 17th

### Odin Project - [ToDo List](https://github.com/Brett-Tanner/odin-todo)

- UI
  - Shared components for
    - [x] Form
      - [x] Project Fields
      - [] Todo Fields
  - [] Project pages showing all todos for a project
    - Activated by clicking on the project from the sidebar nav
    - Replaces the content of the main, renders using the todo list of the project and listTodos from todoComponents
- Functionality
  - [] Can click a button to add new todos
  - [x] And to add new projects
- [] Build out the localStorage capability

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Chores

  - [x] Fix Rinakai's afternoon price
    - [x] Fix a pricing bug when both AM and PM are registered for Rinakai's triple day
    - [x] Allow the pizza party to be selected independently of AM or PM
  - [x] Add new activities
    - [x] Yako
    - [x] Shinjo
    - [x] Shin-Urayasu
    - [x] Kamata
    - [x] Minami Gyotoku
      - [x] Add a plusone category to options
      - [x] Modify views to show plusone options with radio buttons on the registration page
  - [] Update the attendance sheet views
    - [] to show the morning and afternoons of the new special days separately
    - [] gyotoku's plus one options should only show the registered one
    - [] Summer monster shows as the afternoon slot for the main special day on Rinkai's main sheet??

- Features

  - Stats page
    - [x] Add coupon tracker graph
      - [x] And one showing revenue for Leroy's
        - Internal cost is 3000, external is 5000
        - Per school graph of the revenue from that coupon
      - [x] Also total revenue from coupons
    - [x] Split activity popularity into 2 graphs, one for new activities and one for original
    - [] Add school-specific pages for each of the existing stats

## August 18th

### Odin Project - [ToDo List](https://github.com/Brett-Tanner/odin-todo)

- UI
  - Components for
    - [x] Project Form
    - [x] Todo Form
  - [] Project pages showing all todos for a project
    - Activated by clicking on the project from the sidebar nav
    - Replaces the content of the main, renders using the todo list of the project and listTodos from todoComponents
- Functionality
  - [x] Can click a button to add new todos
  - [x] And to add new projects
- [] Build out the localStorage capability

## August 19th

### Odin Project - [ToDo List](https://github.com/Brett-Tanner/odin-todo)

- [x] Project name links lead to their todo list when clicked
- [x] Add button to go back to home/all todos
- ToDo card buttons
  - [x] Description
  - [x] Notes
  - [x] Checklist
  - [x] Edit
  - [x] Delete
    - [x] pass a reference to the project it belongs to at creation so you can actually delete
- [x] Fix layout on mobile
- [] Add notes form
- [] Add checklist form
- [] Add a way to delete projects (probably from their own screen)
- [] LocalStorage
  - [] Save & load projects
  - [] Save & load todos

## August 20th

### Odin Project - [ToDo List](https://github.com/Brett-Tanner/odin-todo)

- [x] Add notes form
- [x] Add checklist form
  - [] And the logic to display it if it exists
- [] Make submit button a shared component which takes innerText and a callback as arguments
- [] Add a way to delete projects (probably from their own screen)
- [] LocalStorage
  - [] Save & load projects
  - [] Save & load todos

## August 21st

### Odin Project - [ToDo List](https://github.com/Brett-Tanner/odin-todo)

- [x] Add checklist form
  - [x] And the logic to display it if it exists
- [x] Add a way to delete projects (probably from their own screen)

## August 22nd

### Odin Project - [ToDo List](https://github.com/Brett-Tanner/odin-todo)

- [x] LocalStorage
  - [x] Save projects automatically when
  - [x] Load projects (if they exist) on page load
- [x] Finish!

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Chores

  - [x] Check the attendance sheets for all the new activities for any issues caused by all the complications
    - [x] Rinkai's middle event wasn't using the name of the actual event because I hardcoded it as 中延長 in the past
    - [x] Extension option was still taking up space on the sheet when it didn't exist because it was hardcoded to be there
    - [x] The event id for 大井's aqua park trip was 16 rather than 22 for some reason????? Was only stopping it from showing up in the daily attendance list, no other problems
      - [x] Same for 北品川
    - [x] 南行徳 parent days had the plusone options pushing everything else completely off the screen, condensing them all into one column too way too long
  - [x] Info for friday presentation
    - [x] Why the plugin option didn't work
    - [x] Time estimate for developing our own reservation solution
    - [x] And for getting the site ready for next event
    - [x] Put the time estimates in a sheet, not a doc

- Features

  - [x] Make sure coupons are preserved when invoices are merged (they were not)
  - Stats page
    - [x] Option charts
      - [x] Count total registrations for options grouped by name
      - [x] Revenue by options grouped by name
      - [x] Separate the arrival and departure options into pie charts showing which are most popular
    - [x] Daily Registration chart? Should get around the created_at issue for invoices
      - Can't get revenue from it though
      - But even after the blank invoice issue is resolved, will retain an accurate picture of registrations per day after invoices are merged
    - [x] Separate graphs for daily updates by staff and customers
      - Count versions where item_type == invoice and event == update
      - Possibly subtract the create events for that day? Might stop inflation from both usually happening together
      - Might also lead to negative numbers though
    - [] Add tabs/pages for the type of stat
    - [] Add school-specific pages for each of the existing stats

## August 23rd

### Odin Project - [JS Components](https://github.com/Brett-Tanner/js-components)

- [x] Figure out the TS/tailwind config for this project
  - Remember the preview server only gets the correct paths when run from the individual component's folder
  - tailwind cli is `npx tailwindcss -i ./main.css -o ./dist/output.css --watch`
  - `tsc -w` does the job for typescript
- [] Dropdown
  - [x] Scaffold layout
    - Dropdown container should be a ul with position relative
    - Heading is a li in that ul
    - Dropdown itself is a nested ul within the container, position absolute and w-full
- [] Offcanvas
- [] Carousel

## August 24th

### Odin Project - [JS Components](https://github.com/Brett-Tanner/js-components)

- [] Dropdown
  - [x] Make heading links clickable if hoverable, and preventDefault if not hoverable
  - [x] Close non-hoverable dropdowns when you click elsewhere on the page (if target isn't the container or children)
  - [x] Close all other dropdowns when a new one is opened
  - [x] Create some animations to show off
    - [x] And a way to reverse them
  - [x] Add the animation API and the stuff I learned about it to my wiki
  - [x] Add animation duration to the animation info passed
  - [x] Probably add an array of default hidden classes, there are too many of them copied all over
  - [x] Implement some basic logic for applying individual, offset animations to each dropdown item
  - [x] Extract logic for adding the offset into its own function in the animations module
  - [] Refine offset logic to get rid of some of the weird glitchiness
    - The li are offset, but there's some weird flickering going on
    - Offset values are probably weird in some way
    - [This](https://css-tricks.com/repeatable-staggered-animation-three-ways-sass-gsap-web-animations-api/) got me on the right track, further inspection might help
  - [] Add the widgets and their animations
  - [] Some glitchiness while mousing over the hover animation as it fades in, try resolving that
    - Probably with a setTimeout on the listener which starts the removal
- [] Offcanvas
- [] Carousel

## August 25th

### Odin Project - [JS Components](https://github.com/Brett-Tanner/js-components)

- [] Dropdown

  - [x] Refine offset logic to get rid of some of the weird glitchiness
    - The li are offset, but there's some weird flickering going on
    - Offset values are probably weird in some way
    - [This](https://css-tricks.com/repeatable-staggered-animation-three-ways-sass-gsap-web-animations-api/) got me on the right track, further inspection might help
      - Yeah, the initial state of the element has no transforms, and I didn't specify a plain beginning state with no offset
      - So they were starting with no transform, animating to what should be the starting transform, then animating to the final state
      - Probably too much movement in opposing directions for 300ms, which is why it looked glitchy
  - [x] Decide the widget can/should just be handled with a ::before/after pseudoelement, styled through the passed headingClasses
    - [x] Create some examples of doing that

## August 26th

### Odin Project - [JS Components](https://github.com/Brett-Tanner/js-components)

- Menus
  - [] Bubble
    - [x] Hamburger button to toggle
- [] Carousel

## August 27th

### Odin Project - [JS Components](https://github.com/Brett-Tanner/js-components)

- Dropdowns
  - [x] The autoclose on clicks outside broke, I fixed/refactored it
  - [z] Modularize/document code
    - [x] addHoverListeners
    - [x] addClickListeners
      - [x] and hideOtherDropdowns to use ariaExpanded
- Menus
  - [x] Bubble
    - [x] Menu items fade in/out when toggled
    - [x] Backdrop slides to cover the whole screen when toggled
    - [x] Run the passed function on click
    - [x] Fix the X animation, the smaller the screen gets (or more toward certain aspect rations) the more off-center it gets.
      - Maybe switch to using absolute units?
      - Nah, made them all relative instead
    - [x] Add the logic for putting images in the buttons
  - [] Drawer
  - [] Offcanvas
  - [] Rudder
- Carousel

## August 29th

### Odin Project - [JS Components](https://github.com/Brett-Tanner/js-components)

- Carousel
  - [x] In index.ts, programmatically generate an array of path strings to pass to the carousel function
    - Nah, just use `ls` and copy it haha
  - [x] In the carousel function, automatically generate the thumbnail paths by adding `/thumbails/` ahead of the file name
  - [x] One image in the middle

## August 30th

### Odin Project - [JS Components](https://github.com/Brett-Tanner/js-components)

- Carousel
  - [] Arrows to click which move it in that direction
    - [] Create the arrows
    - [] Add the logic for moving images
    - [] Also keyboard navigation
  - [] Add nav dots allowing skipping to any image
- [] Offset and skew the previous/next images, maybe fade a bit as well? Or a shadow
- Menus
  - [] Rudder
  - [] Drawer
  - [] Offcanvas

### Work Project - [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Features

  - Stats page
    - Adjustments
      - [] Number of each adjustment applied
      - [] Total effect on revenue from each (some will be negative)
        - [] Group any with a magnitude less than a certain amount into a misc data point
    - Edits
      - [] Total edits by staff/customers (subtract the total number of creates from updates)
    - Revenue
      - [] Pie chart of revenue by student category
      - [] Pie chart of revenue by time slot/option/adjustment
    - [] Add tabs/pages for the type of stat
    - [] Add school-specific pages for each of the existing stats
  - [] Add a way of uploading images to the S3 bucket from the site
    - [] Upload to a specific folder based on purpose of image
    - [] Make sure large files work, they didn't the first time
  - [] Event creation
    - [] Event step
      - [] pre-select the existing image in the form
      - [] Extend the 'all' option on event creation to allow specific schools to be selected
    - [] Time Slot step
      - [] Allow slots to be edited individually from the index
        - [] Allow adding an afternoon slot manually if editing a special day
        - [] Allow custom options to be added/edited
        - [] Allow updating time slots with the same name for all events with the same name
      - [] pre-select the existing image in the form
    - [] Remove ability to destroy events from frontend when I'm done testing (no route for it)
    - [] Add a test event with the new flow (on dev env) and go through the whole app to see what needs changing to support having multiple events
      - Probably need some dummy registrations too
  - [] Per-activity costs
    - [] Add internal/external modifier cols to Time Slot
    - [] Add a snack boolean col to Time Slot
    - [] Add code to use them in Invoice#calc_cost
  - [] Figure out what needs to change to stop persisting a blank invoice when there are no unconfirmed invoices available for a child and someone looks at their registration page
  - [] Remove all references to the email template column, then remove the column
    - [] Split the User#show pages out into different pages for different roles
  - [] Have a way to stop sending emails when the event stops
  - [] Look into using our SES account/domain for the school emails to escape their 5000 email limit

- Future Plans

  - [] See if the occasional memory problems are actually something more like [this](https://www.engineyard.com/blog/thats-not-a-memory-leak-its-bloat/)
    - [] Setting up counter_cache for some stuff like registrations on TimeSlots might help with the memory usage
    - [] Also loading all the TimeSlots and Options from the start when calculating Invoice costs
    - [] Install and use Bullet gem
    - [] Also maybe Rack::Bug, or a newer version of something similar since it was last updated in 2015
    - [] Turnout gem to put it in maintenance mode?
    - [] Look at moving to view components rather than partials for (apparently) better performance and easier testing
    - [] Bump Ruby version and others as far as possible
    - [] Forms
      - [] Add useful error messages to all forms
      - [] Add JS validation as well (constraint validation API, see the [Odin Project Lesson](https://www.theodinproject.com/lessons/javascript-form-validation-with-javascript))
    - [] Come up with a better logging system than just dumping them unsorted to S3 (apparently sending them to STDOUT sends them to Cloudwatch?)

### Work Project - [Seasonal Wiki](https://github.com/Brett-Tanner/KU-wiki)

- [] Add 'How to contribute'
  - [] Adding a page
  - [] Adding a section
- [] AWS section
  - [] Pushing a new version
  - [] Services we use and overview of what for
- [] Rails section
  - [] Overview
  - [] Useful Commands
