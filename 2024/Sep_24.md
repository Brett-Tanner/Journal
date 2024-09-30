# September 2024

## September 2nd

- [x] Add `#party?` to Event, so I can change the current check later without needing to find/replace
  - [x] Change all occurrences of checking for the early bird discount

### Leaving prep

- [x] Hide images uploaded after n months from select box
  - [x] Add tests for BlogGroupable
  - [x] Refactor the BlogGroupable concern for readability
- Registration Page
  - [x] Refactor the view to HAML

## September 3rd

- [x] Check out Kindy Special Lessons appearing on the wrong row of the calendar
  - Seems to be caused bt having multiple Special Lessons on the same day
  - Was actually because I was missing a specified row for kindy Special Lessons

### Leaving prep

- Registration Page
  - Extract various components into partials, move existing ones to invoices folder
    - [x] Header
    - [x] Event Options
    - [x] More Info
    - [x] Parent Messages
    - [x] Price Footer
  - [x] Make a 'modal confirm' partial and use it when responding to reworked view
    - To avoid breaking existing functionality
  - [x] Replace BS modals with real dialogs, so sick of messing around with their attributes
    - [x] Copy & modify the dialog controller from LMS so I can actually open it when clicked
    - [x] Fix modal exceeding screen width on mobile
  - [x] Fix price bar running around the screen

## September 4th

- [x] Styling discussion with Alex

### Leaving prep

- Registration Page
  - [x] Copy missing translations that affect the events/show page
  - [?] Simplify the ids for turbo frames? Shouldn't need the child ID
    - Same for the list of registrations
    - Works fine on new version but not current one, so leave it for later
  - [x] Change the BS accordion stuff to just be details elements
  - Deal with the mess of an 'add slot' partial
    - Convert to HAML
      - [x] Separate out morning and afternoon
      - [x] Morning part
      - [x] Afternoon part
  - Identify & fix in-view DB access
    - [x] Price Footer

### LMS

- [x] Identify and fix cause of category resources repeating for teachers

## September 5th

- [x] Change all the afternoons marked outdoor to seasonal

### Leaving prep

- Registration Page
  - Identify & fix in-view DB access
    - [x] Afternoon Reg Card
    - [x] Event Cost
    - [x] Realise the registered slots where being fetched in the view without `includes`, leading to N+1 queries
  - Refactor the controller to be less of a mess/remove filtering from view
    - [x] Extract NewInvoiceable concern to encapsulate data fetching for the new action
    - Eliminate unnecessary instance variables, and add new ones if needed
      - [x] Choose between @member and @non_member prices in controller & assign to @price_list
      - [x] Add a 'for_registration_page' scope to TimeSlot to DRY the includes etc for that
    - [x] Create 'new-' prefixed controllers and use them in new views
      - [x] Then roll them back, better to have test first. Also should start by completely reworking it, not altering first

### LMS

- [x] Put the general category materials behind a feature flag for the expo & hide for both showcase orgs in:
  - [x] Teacher lessons
  - [x] Teacher resources
- [x] Hide empty lesson types on calendar
- Add translations
  - [x] Nav
    - [x] Fix upload selector styling with JA text
  - [x] Teacher homepage
  - [x] Teacher lesson index
  - [x] Extract level translations to a levels top level file
  - [x] Teacher lesson show
    - [x] Add subtype translations to lesson files
  - [x] Notifications

## September 6th

- [x] Let staff make registrations for kids at online school events
- [x] Make the JS sort controller able to sort multiple tables on one page
  - Right now it always sorts the first one

### Leaving prep

- Registration Page
  - [x] Clean up confirm action logic
    - [x] Lead to me completely removing the ignore_slots/opts args from calc_cost & doing it automatically in model
  - [x] Write a JS enabled system spec to check it all works
    - [x] And once for the new version, hopefully few changes
  - [x] Copy the missing translations
  - Simplify JS
    - [x] Ensure there are commas in the JS costs and initial cost
    - [x] Use the fact there's only one price list instance variable now
      - [x] Don't need member anymore
    - [x] Rename `others_cost` to `siblings_event_cost`
    - [x] Alter the JS to preserve commas in the calculated total price
  - [x] Refactor radio partial to Haml
    - [x] Combine the conditional branches, setting the different values at the start of the partial
    - [x] Move all the time option logic into a time option partial
  - Check TimeSlot, Option, Event & Invoice models for methods that should be helpers
    - [x] TimeSlot
    - [x] Setsumeikai

## September 9th

- [x] Fix incorrect name_date arg erroring attendance sheets for activities
- [x] Chase down error when editing some student's party bookings
  - Was day helper not existing, needed `en_day`
  - [x] Add `#has?` to regular schedule as replacement
  - [x] And tests for `#has?`
- [x] Fix the lesson topic being parsed incorrectly on the form
  - [x] Add tests

### Leaving prep

- Activity attendance list
  - Haml refactor
    - [x] Base partial
    - [x] Row partial

## September 10th

- [x] Decide on a resignation date - October 15th
- [x] Delete parent account
- [x] Investigate the kid with the missing booking
  - When he was merged with his SS version the summer bookings merged into his unconfirmed spring booking
  - [x] Verify it was just the 3 summer bookings on his spring invoice, then delete those and make a new summer booking with them on it
- [x] Check confirm emails have correct text with fake kid
  - Definitely sending the correct email
  - Unless it's an SM confirming it, which sends the modified email as well
  - [x] Fix & add a test
- [x] Add new Halloween exclusive banner
- [x] Get Leroy a list of stuff I manage

### Leaving prep

- [x] Add a away for admins to delete users (if they don't have kids)
- [x] Add CSV export for versions
  - [x] Another button for just the last month

## September 11th

### Leaving prep

- [x] Look into adding photo service button to floating price bar
  - [x] Get a draft going on the Invoice#new page
  - Need the visuals reworked though
- [x] Fix duplicate departure options
  - Was cos I overwrote `Option#departure?` to include both types
- [x] Test adding a new school
  - [x] Add the ability to delete schools so I can remove it after
  - [x] Add notes about array inputs being comma separated, if they still are
  - [x] Write docs for it
- [x] Default setsu calendar to adding unknown schools to the end

## September 12th

- [x] Ignore my beautiful summary page to redirect to the ugly complete page on the main site when setsu inquiry made
- [x] Add some text to the event site confirmation emails

### Expo prep

- Add an API on the LMS to receive form submissions & email Nakagawa san
  - [x] Add the controller & non-DB model
  - [x] Create the mailer
    - [x] Create a job to send the mail
- [x] Also need to set up an inquiries@vision-up.biz email address, which forwards to Nakagawa san
- [x] Add age ranges to level cards for teacher page k3-6, ele6-12
- [x] Make sure the cards don't fill the whole screen when there're less than 4
- [x] Check how Luis keeps getting the fun colorscheme on org 3
- [x] make monthly materials default to current week, not blank
- [x] Add priority label to support requests form
- [x] Also send emails when a support request is made

### Leaving prep

- [x] Add SchoolsController#index to allow reordering school display order on one page
  - [x] Add `position` col to schools
  - [x] Use the position attr in the setsu calendar to sort
  - [x] Figure out the way to deploy with minimal disruption
- [x] Add ability to delete areas
  - [x] Change policy to allow admins to delete areas
  - [x] Refactor area related views to Haml

## September 13th

### Expo prep

- [x] Add a polyfill for Popover

### Leaving prep

- [x] Add ability for admins to create admin accounts to LMS
  - [x] And to edit themselves
  - [x] And destroy themselves
  - [x] Update the policy & specs
- Figure out how to get the splash/login working with just an image/picture tag rather than bg-image
  - [x] Refactor the templates to use `picture` rather than `background-image` CSS property
  - [x] Allow uploading splash images from frontend
  - [x] Haml refactor for upload page
  - [x] Set the splash image in controller from latest uploaded splash
    - [x] Add to BlobGroupable & rename to BlobFindable
- Move stuff I've been hosting to company accounts
  - [x] Cloudflare wiki
  - [x] LMS & event site Dockerhub
    - [x] And change the targets in code
- [x] Fix vision-up.app emails going to spam
  - Was missing an MX record for SES in Cloudflare

### LMS

- Add translations
  - [x] Support Requests
  - [x] Students
  - [x] Tests
  - [x] Lesson Calendar

## September 17th

### Leaving prep

- [x] Planning what to do with Jayson

### LMS

- Styling
  - Test results
    - [x] Header
    - [x] Body
  - Students
    - [x] Search form

## September 18th

### Leaving prep

- Training Jayson
  - [x] Overview/walkthrough of LMS
  - [x] Discussion on importing lessons from CSV, likely to not be needed at least in current form
  - [x] Prep/instructions for adding announcements
- [x] Make copy of journal so Leroy can show people the task list

### LMS

- Styling
  - Students
    - [x] Count summary
    - [x] Student profile
    - [x] Update test summary contents

## September 25th

- [x] Merge Mike's vision-up promo site code back to main
  - [x] Resolve conflicts
  - [x] Run a linter on it
  - [x] Add a file as an example of how to build the form

### Jayson Stuff

- Add announcements
  - [x] Wrote system spec
  - [x] Created model, migration & factory
  - [x] Wrote policy & policy spec
- [x] Set Jayson up to pull from KUJP-Code repo

## September 27th

- [x] Summer photo kids, kanji kana eng school membership and SSID
- [x] Various minor fixes
- [x] Exempt inquiry controller CSRF, other issues we can find in log
  - May need to whitelist mike.vision-up.biz and non subdomain version

### Jayson Stuff

- Add announcements
  - [x] Create new/edit/form partial
  - [x] Fill out controller
  - [x] Add index
  - [x] Add shared partial to display them
  - [x] Add update & delete actions

## September 30th

- Translations
  - [x] Calendar lesson types/heading
  - [x] Classes
  - [x] Tests
- [x] Style login page
  - [x] Add splash image
- [x] Style splash page

### Jayson Stuff

- Bumping versions/code scanning
  - [x] Brakeman run, dynamic render path
  - Dependabot
    - [x] Materials webrick & puma
    - [x] Materials solidqueue
- [x] Overview of event site
