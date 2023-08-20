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
  - [] And the logic to display it if it exists
- [] Make submit button a shared component which takes innerText and a callback as arguments
- [] Add a way to delete projects (probably from their own screen)
- [] LocalStorage
  - [] Save & load projects
  - [] Save & load todos

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Features

  - Stats page
    - [] Option charts
      - [] Count total registrations for options grouped by name
      - [] Separate the arrival and departure options into pie charts showing which are most popular
      - [] Separate graphs for daily updates by staff and customers
        - Count versions where item_type == invoice and event == update
        - Possibly subtract the create events for that day? Might stop inflation from both usually happening together
        - Might also lead to negative numbers though
    - [] Add school-specific pages for each of the existing stats
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
    - [] Add a way of uploading images to the S3 bucket from the site
      - [] Upload to a specific folder based on purpose of image
      - [] Make sure large files work, they didn't the first time
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
      - [] Add JS validation as well
    - [] Come up with a better logging system than just dumping them unsorted to S3 (apparently sending them to STDOUT sends them to Cloudwatch?)

### Work Project - Setsumeikai

- Rails DB setup
  - Each school gets a setsumeikai event (add a setsumeikai category to that enumerable)
    - The actual setsumeikai is a time slot on that event, SMs can create and edit those time slots for their schools
  - I add area and nearby train stations to the school table so we can sort by those
  - New table for something like 'leads' which will be where we store the info customers submit when requesting a setsumeikai
- Will need SM interfaces for
  - List of leads (per setsumeikai and overall)
  - Calendar view where they can see their setsumeikais
- Customer interface needs
  - School selection
    - with filter by area/station/name etc
  - Then date selection with the calendar
  - Then the form
  - Then a confirmation which shows the details they entered
- Calendar using [this](https://www.ruby-toolbox.com/projects/simple_calendar)

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
