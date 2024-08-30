# August 2024

## August 1st

- [x] Get list of parent emails who've made a booking but didn't pick photo service
  - [x] Enable parents to register for just photo service
  - [x] Fix tests relating to event options
- More new activities
  - [x] Futamatagawa
  - [x] Monzen
  - [x] Shin-urayasu

### LMS

- [x] Use host whitelist for video tutorial uploads
- [x] Remove the image component code from pdf_imageable
  - [x] rework into ImageValidatable concern
  - [x] Update the models that use it
- Add the actual backgrounds
  - [x] DailyActivity
  - [x] Exercise
- [x] Use the new image component in other plans
  - [x] And in the image page component
- [x] Add PDFBackground component
- [x] Switch the Keep Up/Specialist icons
- [x] Drop speaking from tests/results
- [x] Bring the locale toggle back for lesson view

## August 2nd

- More new activities
  - [x] MinamiMachida
  - [x] Kamata
  - [x] Omori
  - [x] Shinkawasaki
- [x] Fix kids being unable to register because of the orphan option check trying to access `registerable` on a hash
- [x] Add Daniel's activity attendance count by school table
  - [x] Haml refactor of activities chart page

### LMS

- [x] Add a 'Regenerate Guides' button for each lesson type (just me for now)
- [x] Add Exercise back to the list of types which skip generating guides for the moment
  - [x] Temporarily remove PDF expectations from tests
- Github issues
  - [x] #64 Writers can't propose changes to at least lesson 354, form just resets with no errors
    - was because it was trying to add phonics resources by an attachment that was already in use on the main lesson
    - solved by making the existing phonics resource attachments nil if a writer
    - [x] Also ensured phonics resources and resources are copied from proposal
    - [x] And extracted a comparable lesson partial
  - [x] #66 test form not in main element

## August 5th

- [x] Diagnose & solve issues caused by mysterious disappearance of Shinjo photo service option
  - [x] Fix the affected invoices so they're registered for the new one
  - [x] Prevent options being deleted if registered for (but only with destroy)
  - [x] Figure out how the heck the option got deleted in the first place
    - If you call #delete(record) on an AR relation, it deletes it from the DB, not the relation
- [x] Add the new photo service icon

### LMS

- [x] Remove ability to edit course_lessons/resources through course form, is insanity
- Github issues
  - #67 scope tests to organisations/courses somehow
    - [x] Modify test scope to go thru course for school staff
      - [x] Update seeds to take it into account
      - Will want to only see current or past tests

## August 6th

### LMS

- Github issues
  - [x] #67 scope tests to organisations/courses somehow
    - [x] Add accepts_nested_attributes to the form/controller/model for Test
- Calendar page
  - [x] Add a `#week_lessons` method to courseable
  - [x] Controller & view scaffold
  - [x] Make the lessons clickable buttons that reveal the lesson modal
  - Styling
    - [x] Columns/headers

## August 7th

### LMS

- Calendar page
  - Styling
    - [x] Row headers, type separators
    - [x] Lesson buttons
      - [x] Level dots
  - [x] Add the key popover
    - Try popover API
  - [x] Highlight whole columns for odd ones
  - [x] Create org nav
    - [x] Add the styled org nav to other places it could be used
  - [x] Add buttons to move forward a week
  - [x] Add a way for the calendar buttons to go straight to the requested level
  - [x] Admins can't access lessons from calendar

## August 8th

- [x] Monthly materials search is broken

### LMS

- [x] Exercise needs to be kindy/ele, kindy can have exercises instead of daily activity sometimes
- [x] Fix wrong day being passed to calendar buttons
- [x] Sticky day header
- [x] Switch keep up/specialist colors in tailwind
- [x] Add to key list
- [x] Skinnier empty cols
- [x] Specialist & specialist advanced overlap
- [x] Some rows not using custom row numbers when needed
- [x] On monthly materials page, stop the links showing up for teachers. Just give them the lesson name
- Notifications
  - I think I want to just store them as JSONB on the User record, delete them once seen if they exceed a certain number
  - Should have text and a link
  - [x] Figure out how to use StoreModel & get a factory working
  - Methods on User to
    - [x] add notifications
    - [x] mark as read
    - [x] mark all read
    - [x] delete
    - [x] validation to delete when > certain amount of read
  - Manually send notifications to subsets of people
    - [x] Request spec to verify the targeted users get the notification

## August 9th

- **THE LAST THING YOU PUSHED ON THE 8th CAUSED 2 PROBLEMS**
  - [x] Monthly materials is completely down, even for admins
    - Was calling `#any?` on @lessons when it could be nil, changed to just `if @lessons`
- [x] Add another million activities for Futamatagawa/Todoroki

### LMS

- Notifications
  - Manually send notifications to subsets of people
    - [x] Policy & tests
    - [x] Controller
      - [x] Create the job
      - [x] add a notifications queue
      - [x] Pass the manual creation tests
      - [x] Pass the user read/destroy tests
  - Views
    - [x] New
    - [x] Index
      - [x] If an admin, show the last 10 completed notification jobs
      - [x] Add created_at to Notification
      - [x] Add 'Mark all as read', bulk delete links
      - [x] Simplify notifiable API to allow single/bulk deletion with same method
    - [x] Taskbar icon
      - [x] Fix URL check failing on empty string

## Obon!

9 day holiday.

## August 19th

### LMS

- Notifications
  - [x] Views
    - [x] Popover
      - [x] Make the X submit to mark it read
        - Need all notifications so index is correct
      - [x] Add turbo response for marking it read
        - Just re-render the popover
      - [x] Add link to index at bottom
  - [x] To parents when a child's test result becomes available
  - [x] Auto-mark notifications read when link is followed
    - Probably needs to direct to show action first, which updates the notification and redirects
  - [x] When there are new (relevant) support messages
    - [x] Add `#participants` to support request
      - Returns an AR relation of Users who've commented or who sumbitted the request
    - [x] Notify admins & sales when new request created
    - [x] Notify participants when new message added to request
      - Other than the person who messaged

## August 20th

- **THE LAST THING YOU PUSHED ON THE 8th CAUSED 2 PROBLEMS**
  - Calendar can't look forward or back a week
  - It's a problem with those weeks specifically
  - [x] Was not handling SpecialLesson
- [x] Fix exercise thumbnail not being generated
- Coaching Jayson
  - [x] Fix testing setup
  - [x] Add evening class category resources
    - [x] Write tests for evening lesson_category
  - [] Lesson CSV upload
    - [x] Write system spec
    - [x] Write LessonUploadPolicy & spec
    - [x] Create new action and view
    - [] Add the JS StudentUploadController

### LMS

- [x] Finish using the new lesson_order_hash to order lessons for kindy/ele
- Update built queries for lessons to use the ? syntax, not string interpolation
  - [x] Day lessons
  - [x] Week lessons
    - [x] Fix the mismatched number of conditions and `?` in week query
    - [x] Write a spec for week lessons
    - [x] Change all references to `week_lessons` to `week_course_lessons` to accurately represent what it returns
  - [x] Available tests

## August 21st

### LMS

- [x] Should I be including StoreModel::NestedAttributes on User for notifications?
  - No, removed it
  - Never gonna be adding notifications to a specific user from their form
- [x] Change lesson_order_hash to lesson_type_order (an array)
- New customer form
  - [x] Write some basic factory/validity tests to scaffold how I want it all to work
    - Chooses the correct model using `StoreModel.one_of` as the factory, using `field_type`
  - Create FormTemplateFields
    - [x] FieldAttributes to hold/validate all the potential options
      - In the form, these will be part of the form for each field type
      - Can get the type of each attribute I allow like `FieldAttributes.new.type_for_attribute(:required).type` then use that to decide which field type to create
    - [x] TextField
    - [x] Textarea
    - [x] Checkbox
  - Create FormTemplate
    - Probably just a fields jsonb column then titles/descriptions/org_id
    - Use StoreModel for the fields column to ensure it has
      - attribute name
      - field type
      - order
      - explanation (optional)
      - field options
    - [x] Create migration & factory
    - [x] Test fields can be added
      - [x] Refactor field models to have input_type attr, which is used in form_helper
        - But still set by default
    - [x] And that their errors show up on FormTemplate

## August 22nd

### LMS

- New customer form
  - [x] Add `data` attribute to `InputAttributes`
    - Nah, complex & security risk when not even sure it's needed
  - [x] Create FormTemplate
    - [x] Create policy & tests
    - [x] Create controller & views
      - [x] Form/new/edit
        - [x] Field fields
        - [x] input attribute fields
      - [x] Create/update/destroy
  - Create FormSubmission
    - Associated with:
      - the parent who submitted it
      - staff who created it
      - the form it's a submission for
    - Main content is jsonb column with the answers keyed by the attribute they were answering
    - When creating a new one, select from the available form templates to base it off
    - Will then auto-generate a form based on the template
    - [x] Generate migration & create factory
    - [x] Create & test FormSubmissionPolicy
    - Create views & controller
      - [x] Index, with links to create from each template

## August 23rd

- [x] Bump some dependencies to fix security vulnerabilities
- [x] Create accounts for 3 staff who need to see all document uploads
- [x] Add & test out the halloween banners locally
  - Refactor login & welcome splash pages
    - [x] to HAML
    - [x] get the image to be correctly sized
    - [x] un-snake the ids
  - Maybe think up a way to add them without needing to update the code
  - Probably needs to be a model?
  - Or they could be uploaded as resources through the current file upload dialog
- [x] Run Leroy through creating the halloween parties

### LMS

- New customer form
  - Create FormSubmission
    - Associated with:
      - the parent who submitted it
      - staff who created it
      - the form it's a submission for
    - Main content is jsonb column with the answers keyed by the attribute they were answering
    - When creating a new one, select from the available form templates to base it off
    - Will then auto-generate a form based on the template
    - [x] Remember to add 'locked' boolean column
    - [x] Create views & controller
      - [x] Form/new/show
        - Form generated from template fields
      - [x] Create/update
        - [x] Add code to fill in the existing fields when editing
    - [x] Clean up the index display now I have something to look at

## August 27th

- [x] Endless attempts to get our new brilliant SSO system to work

### LMS

- New customer form
  - [x] Create FormSubmission
    - [x] Show/destroy
  - [x] Refactor existing input types into `SingleInput`
    - [x] And update the partials
    - [x] Add a `MultiInput` for select/radio
      - [x] Add the template form partials

## August 28th

- [x] Upload new seasonal site version with halloween banners
- [x] Make the early bird discount apply to each party attended
- [x] Hide everything expect the 1 course if event is party (has non-zero early bird)
- [x] Add early bird adjustments to JS calc (probably be creating an adjustment in the controller)
  - [x] Add a negative check to the JS calc
- [This kid](https://kids-up.app/en/events/173?child=12422)
  - is registered for some activities but they aren't checked
  - and the invoice cost is 0
  - [x] Fix
- [x] Meeting w/Jack & Leroy to discuss prep for me potentially leaving

### Leaving prep

- [x] Add list of kids who have > 5, 10 etc. for badges

### LMS

- [x] Fix the incorrect dates on teacher calendar (days are right but date number is +1)

## August 29th

- [x] Remove the morning Kanji from the activity names on reg page (all)
- [x] Add the new welcome splash images, with avif/png versions
- [x] Completely remove the see more thing on the bottom blue bar
- [x] Remove the don't apply for afternoon text
- [x] Add Action Text to the event model so we can have the text with link etc.
- [x] Remove price list table if it's a party
  - Do it by checking for an early bird discount
- [x] Don't render the coupon dropdown if it's a party
- [x] After Leroy tried to make the goal for all events something like 3 trillion, prevent him doing that again
  - The DB column can only handle up to the max value of a 4-byte int
- [x] General assistance/troubleshooting of Leroy's attempts to make the event
- [x] The JS for the total event cost has been changing the event name to Summer 2023 this whole time lol
- [x] Formatting on description
  - [x] Left align in editor so doesn't happen again
- [x] Change the opengraph title, just delete the seasonal bit
- [x] Send leroy sample change/confirm emails from party
- [x] Make the course summary say event instead

### Leaving prep

- Make it possible for Admins to
  - [x] remove/change ssids
  - [x] remove kids from parents/delete them
- Allow admins to create other admins
  - [x] Update policy
  - [x] And controller/views
- [x] Delete the activity list portion of the event sheet, and simplify the queries in the controller
  - [x] Refactor index to HAML
    - [x] Extract activity list bootstrap accordion to partial
    - [x] Change Bootstrap accordion to regular details element
    - [x] Use the filter_header partial

## August 30th

- [x] Bump both apps to Rails 7.2.1
  - Didn't end up doing this, tried but too many gems not updated for 7.2 yet

### Leaving prep

- [x] Refactor event_child to HAML
  - [x] Convert seen and update turbo stream responses to Haml
  - [x] Remove redundant 'view' link when invoice is changed
  - [x] 'Entered' cell seems to have a lot of complicated, duplicated code
    - [x] Email_sent is almost identical
- [x] Add a page where you can edit certain properties for all events with the same name
  - [x] Add BulkEventsController & views
  - [x] Button to release/hide all of an event
  - [x] Add BulkEventsPolicy & tests
    - Just used the EventPolicy
- [x] Add default times for time slots
  - [x] And explanatory text
