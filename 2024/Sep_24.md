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

### Jayson Stuff

- Add announcements
  - [] Add controllers/views
- [] Add organisation ID to kids
  - [] Add automatically when uploading from CSV
  - [] Use in policies
  - [] Make student ID unique within org, not school
  - [] Form and strong params too
  - [] And migrate the existing ones
  - [] Create default teacher and class when new schools create
  - [] Add uploaded students to their school's default class
  - [] In future will need a way for other orgs to bulk assign students to a class
- [] Add event lessons
  - [] They're gonna need an attached image to display
  - [] Use the cards for teacher lessons as a template, same basic layout too
  - Can probably be handled by same controller?
  - [] Style to match Alex's mockup
- [] Provide a summary of kid's test results per test
  - For curriculum team/admins to look at
  - like the input view but minimal
  - maybe sorted by the level they moved to and just showing name/prev level/score
- [] Add reviews to lessons
  - [] Need stars and text
  - [] Text pops up after star rating given
  - [] on the teacher_lesson modal
  - [] Button on the lesson page to mark all reviews acted on, they won't count to the current score
    - Maybe show the score for active reviews and all? And have an index with all of them

### General

- [] Need a separate boolean column for whether the kid has a food allergy
  - Talk to leroy about it
  - Set by a radio button
  - Parents get a splash on their page & kid's page telling them to update, redirected if they try to register
  - [] After Summer School, change it so allergy kids can't see the option for lunch
  - [] When merging children the food allergy or not needs to be copied
  - [] When finding by SSID, make them select food allergy or not in addition to first seasonal or not
- [] Look into setting up emails for our new domains

### Expo prep

- Add an API on the LMS to receive form submissions & email Nakagawa san
  - [] Allow it to receive requests without auth/CORS issues

### Leaving prep

- [] Give event site a 'toggle first seasonal' button
  - Gets the name of the latest seasonal with `#seasonal?`, then a list of their ids
  - Get all the children who attended
  - If they're marked first seasonal toggle it to false
  - [] Add to the wiki under 'creating events' cos it needs to be done before each seasonal
- Get Jayson credentials
  - [] AWS
  - [] New company docker
  - [] Company github
  - [] Company cloudflare
- [] Style the photo service button on footer once designed by Alex
  - [] Will need to change the child switcher links to point at new invoice path

### LMS

- Styling
  - Splash pages
    - [] Splash
    - [] Login
  - [] Tests
- [] Add a UI for viewing/rolling back to previous versions of students
  - [] Remove limit on versions of students stored
- [] Delete the 'LessonUses' controller and move it to CourseLessons#index, since that's what it really is
  - [] See if there's anything stopping me just using a CourseLesson form, rather than `fields_for` in a form
  - [] Add the date fields and CourseLesson update/create actions to enable adding lessons to courses easily
- [] When updating upload progress, decrement failures if sum of all > total

### Event Site

- [] Need to add event summary stats to the charts
  - Like the table Admins get at the top when they log in
- Extract PDF generation into a concern
  - [] Generate it in a SQ job when the invoice is modified
    - [] Though this might cause issues with ordering, so will need a new queue to ensure pdf jobs performed first
    - [] And make it available to download from the invoice partial
  - [] Refactor to use the cost info object returned by Invoice#calc_cost

#### Future Plans

- [] Add a table showing a summary of inquiries per month and type, as well as total per month [like this](https://docs.google.com/spreadsheets/d/1fcCN4togDFfhgDeuver5Ts-Javrq_s-RI0b_qRcJc3k/edit#gid=1456240236)
- [] Allow for varying price list courses by automatically determining max/intervals in invoice calc
- [] Overwrite the sign in path properly as well
  - Can use `stored__location_for` to redirect to originally requested page
- [] Uncomment `config.force_ssl` in production, we're already redirecting to HTTPS and the other stuff is good
- [] Investigate what happens if you upload a new asset with the same key as an existing one
- [] When importing the historical setsu/inquiries, try insert/upsert_all with record_timestamps: false to set our own created at
- [] In August 2022, RDS certificate [expires](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/UsingWithRDS.SSL-certificate-rotation.html#UsingWithRDS.SSL-certificate-rotation-updating). Will need to rotate to avoid connectivity issues.
- [] Add button to generate photo service armband PDF for parties
  - Printable template with kids' names and a color which shows their photo status

##### ActiveRecord

- Look into [delegated types](https://api.rubyonrails.org/classes/ActiveRecord/DelegatedType.html)
  - [] especially for splitting the mess of user logic into more manageable chunks
- Maybe use [#store](https://api.rubyonrails.org/classes/ActiveRecord/Store.html) on models with JSON, seems to give a nicer API
  - [] price lists
  - [] surveys
  - [] maybe email preferences
- Can use has_one on a has_many to single out a specific important record
  - [] Next event
  - [] Active invoice
- You can define methods on associations either by nesting them within a block for that association or defining a class method on the model like `self.my_method`
  - Lets me pass parameters to an operation on an association
  - But I think this is basically just scopes no?
  - Apparently can define a scope on children like `scope :event_invoices, ->(name) { where(event_name: name) }`
- More specific to what I've needed before, you can pass params to scopes by just putting brackets with the params after the '->'
  - Can also put these in modules for re-use, could be handy for stuff like dates that are on everything
  - [] Definitely useful somewhere in the Charts/Stats section of the site
- validates_acceptance_of creates a virtual attribute which must be true for the record to be saved
  - [] add to User for backend validation of privacy policy
- You can chain a list of validations on a single column, like `validates presence: true, uniqueness: true ... etc.`
- Use SQL strings, or maybe the active_record_import gem to update children

##### Optimisation

- [] Nest the confirm_invoice view inside the new route so it's confirm_new_invoice_path

```
resources :invoices do
  new do
    post :confirm
  end
end
```

- [] Similarly, I could do school filtering by nesting those resources inside the school resource.
- [] Use #fetch and #dig in the controller rather than conditionals about the existence of a param, since they can have a default value if not found
- See if the occasional memory problems are actually something more like [this](https://www.engineyard.com/blog/thats-not-a-memory-leak-its-bloat/)
  - [] Also maybe Rack::Bug, or a newer version of something similar since it was last updated in 2015
- [] use read/write_attribute or bracket notation in my custom getters/setters
  - Not sure what I'm using now, but probably not those
- [] Use AWS Cloudfront to serve images?
  - [Useful article](https://headey.net/rails-assets-active-storage-and-a-cloudfront-cdn)
- [] Can probably speed up queries for ChartController with pluck
- [] If indexing FK columns which can be null, exclude null from the index

##### Views

- [] Check for missing translations with `i18n-tasks`
- [] Use @layer to section off old BS styles so I can switch to tailwind
  - But both tailwind and BS using !important liberally might make that problematic
- [] Use `current_page` helpers in partials to conditionally render stuff like diff school selection on event partial
- [] Only needs locale param in `number_to_currency` calls, rest are bloat
- [] number_to_phone_number exists
- [] there's also a number_to_percentage helper, but may be more verbose than what I'm doing now
- [] If you wanna show fallback content (like on the invoice index) use `render 'partial' || 'fallback text/content'`
- Extract form error messages into a shared partial
  - This exists now as 'shared/\_form_errors'
  - [] But don't think I made sure it was used everywhere
- [] Use time_tag helper when outputting date or time, generates a `time` element which apparently is a thing
- [] Use number_to_human_size when I add the blob index etc.

### SS Replacement

- We need an electronic version of the new student application form
  - Maybe prefill behind a PIN
  - Could use the PIN field on event site users for that
  - Have an open, blank one anyone can use
  - Multi-stage? With stage by stage validations
- New customer form
  - Add a `MultiInput` for select/radio
    - [] Still some issues with deserializing the custom type
    - [] Add the partial to display it on the submission form
    - [] Add the partial to display the responses on the Submission show page
    - [] Extract the reusable/shared code from Single/MultiInput
  - [] Will need to process the field `name` to ensure downcased and underscored
  - [] Create a test form template that matches the new child registration one
    - [] Seed it
  - [] Create basic models for the courses etc., just so I can run the calculation
  - [] Create a model for Contracts
    - [] If Submission#template_id is 1 or some other dumb condition like that;
      - Give a button to create a contract from it
      - which calculates & stores the adjusted contract from the submission
    - [] Calculates the fees based on form selections
      - [] For courses, first month is least of unit price \* selected days remaining or the regular monthly cost
      - [] Needs to add a bunch of other costs, like snack, textbook
      - [] SMs should be able to manually adjust calculated values
        - But only per item, not the total
    - [] Needs to be printable as a PDF for signing, or some way to electronically sign
