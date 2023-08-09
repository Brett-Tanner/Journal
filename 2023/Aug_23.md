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

### Odin Project - [Budgeting Site](https://github.com/Brett-Tanner/budgeting-site)

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Chores

  - [] Add Shin-kawasaki's special day

- Features

  - [] Finish off the event creation features so someone other than me can actually do it
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
  - Stats page
    - [] Add school-specific pages for each of the existing stats
  - [] Figure out what needs to change to stop persisting a blank invoice when there are no unconfirmed invoices available for a child and someone looks at their registration page
  - [] Remove all references to the email template column, then remove the column
    - [] Split the User#show pages out into different pages for different roles
  - [] Have a way to stop sending emails when the event stops
  - [] Look into using our SES account/domain for the school emails to escape their 5000 email limit

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
