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
  - [] Views
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

- [] Need a separate column for food allergy, boolean
  - Talk to leroy about it
  - [] After Summer School, change it so allergy kids can't see the option for lunch
  - [] When merging children the food allergy or not needs to be copied
  - [] When finding by SSID, make them select food allergy or not in addition to first seasonal or not
  - Set by a radio button
  - Parents get a splash on their page & kid's page telling them to update, redirected if they try to register
- [] Try switching on force.ssl for both sites
- [] Look into setting up emails for our new domains
- [] SMs need a test school on event site for training
  - Will need to exclude it from the real scope

### Leaving prep

- [] Make it possible for Admins to remove/change ssids
- [] Remove kids from parents/delete them
  - [] Also change schools
- [] Apply changes to all events with same name
  - [] Including to release/hide all of an event
- [] Add default times for time slots
- [] Hide images uploaded after n months from select box
- [] Add ability to create admin accounts to both
- [] Clean up event#show (and also make it invoice#new, which it should always have been)
- [] Figure out how to get the splash/login working with just an image/picture tag rather than bg-image

### LMS

- [] Put the general category materials behind a feature flag for the expo & hide in:
  - [] Teacher lessons
  - [] Teacher resources
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
- [] ['Shallowify'](https://guides.rubyonrails.org/routing.html?ref=blog.bullettrain.co#shallow-nesting) all the nested routes
- [] Style student/report/test pages
- [] Add organisation ID to kids
  - [] Add automatically when uploading from CSV
  - [] Use in policies
  - [] Make student ID unique within org, not school
  - [] Form and strong params too
  - [] And migrate the existing ones
- [] Fonts might look weird cos I'm just making them bold, not using the actual bold version
  - A guy on the Syntax podcast mentioned this mattered
- [] Add a UI for viewing/rolling back to previous versions of students
  - [] Remove limit on versions of students stored
- [] Might need to reverse the lesson form/fields relationship at some point, partial locals are an issue
  - Noticed this on phonics class, with the associated phonics resources
- [] Delete the 'LessonUses' controller and move it to CourseLessons#index, since that's what it really is
  - [] See if there's anything stopping me just using a CourseLesson form, rather than `fields_for` in a form
  - [] Add the date fields and CourseLesson update/create actions to enable adding lessons to courses easily
- [] When updating upload progress, decrement failures if sum of all > total

#### Jayson Stuff

- [] Add ability to upload lessons from a CSV (for showcase)
- [] Add announcements
  - [] Will need a message, validity period, maybe a link
  - [] Shown conditionally based on User attributes, preferably only attributes w/out joins
- [] Add event lessons
  - [] They're gonna need an attached image to display
  - [] Use the cards for teacher lessons as a template, same basic layout too
  - Can probably be handled by same controller?
  - [] Style to match Alex's mockup
- [] Provide a summary of kid's test results per test, like the input view but minimal, maybe sorted by the level they moved to and just showing name/prev level/score
- Automatically (for kidsUP):
  - [] Create default teacher and class when new schools create
  - [] Add uploaded students to their school's default class
- [] Add reviews to lessons
  - [] Need stars and text
  - [] Text pops up after star rating given
  - [] on the teacher_lesson modal
  - [] Button on the lesson page to mark all reviews acted on, they won't count to the current score
    - Maybe show the score for active reviews and all? And have an index with all of them

### Event Site

- [] Document refactored invoice calculation
- [] Need to add event summary stats to the charts
- Extract PDF generation into a concern
  - [] Generate it in a SQ job when the invoice is modified
    - [] And make it available to download from the invoice partial
  - [] Refactor to use the cost info object
- [] Login isn't showing an error when it fails
- [] Refactor the Event#show page and move it to Invoice#new
- Can do a lot of stuff with cron/background jobs/APIs
  - [] Sync the day's invoices to the new SS in the AM
  - [] Grab a student's test results as JSON to show in the seasonal app

##### Testing

- Write tests for Invoice#calc_cost to prepare for the rewrite
  - Summary
    - [] Test that event options are removed from blank invoices
      - They're currently shown, and the registration remains on the invoice, but not charged for
      - Did not end up doing this because the logic is too entangled
      - Obvious solution is to mark them for destruction in orphan option check, but that's also used with hashes, not just models
      - So can't call #mark_for_destruction, #destroy or set the \_destroy flag
  - [] PDF creation (or at least that one is created)
- Rewrite Invoice#calc_cost as separate classes for cost calculation, summary generation and PDF creation
  - Can test it separately with unit tests till ready, then swap it in when done
- [] Refactor request specs to use rails path helpers
- [] Test emails with [email_spec](https://github.com/email-spec/email-spec) gem
- [] Create `rails predeploy` task to run all the tests and brakeman prior to deployments

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
- Rather than manually setting `_destroy`, use `#mark_for_destruction`
  - [] Will be used by invoice calculations, maybe in the confirm controller too?
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
  - [] Also loading all the TimeSlots and Options from the start when calculating Invoice costs
  - [] Also maybe Rack::Bug, or a newer version of something similar since it was last updated in 2015
- Simplify/modularize invoice code
  - [] Split out PDF functionality
  - [] Preload all the stuff I need for calc_cost at the start and pass it explicitly
  - [] Create columns for each type of cost?
- [] use read/write_attribute or bracked notation in my custom getters/setters
  - Not sure what I'm using now, but probably not those
- [] Use AWS Cloudfront to serve images?
  - [Useful article](https://headey.net/rails-assets-active-storage-and-a-cloudfront-cdn)
- [] Can probably speed up queries for ChartController with pluck
- [] If indexing FK columns which can be null, exclude null from the index

##### Views

- [] Extract conditonal info display into its own partial
  - Already done for the child one, just make more general for parents & move to shared folder
- [] Remember you can use partials in turbo-stream responses, I'm sure there's some stuff to clean up there
- [] Move set_shared_vars in the mailer to a before_action, is fine to apply to all mailers I think
- [] Use @layer to section off old BS styles so I can switch to tailwind
  - But both tailwind and BS using !important liberally might make that problematic
- [] Use `current_page` helpers in partials to conditionally render stuff like diff school selection on event partial
- [] Add a photo_for helper to encapsulate nil checks for associated images and return empty string if missing
- [] Check for missing translations with `i18n-tasks`
- [] Remove locale param from number_to_currency calls, shouldn't need it
- [] number_to_phone_number exists
- [] there's also a number_to_percentage helper, but may be more verbose than what I'm doing now
- [] Change the current event#show to be Invoice#new, since that's what it really is
  - [] Rework the current add_slot partials into a container, morning and afternoon
    - They can likely use fieldsets (with a form attribute matching the invoice form's id) to be submitted with the form directly
    - reduces the JS I need on that page [MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset)
- [] If you wanna show fallback content (like on the invoice index) use `render 'partial' || 'fallback text/content'`
- [] Extract form error messages into a shared partial
- [] Potentially also extract fields shared between multiple models into a partial (e.g. names for kids/parents)
  - Or just partials for each type of form group? As a fieldset
- [] Apparently there are undocumented ControllerHelper methods I can use to generate the ID for for main elements
- [] Use time_tag helper when outputting date or time, generates a `time` element which apparently is a thing
- [] Use number_to_human_size when I add the blob index etc.

### SS Replacement

- We need an electronic version of the new student application form
  - Maybe prefill behind a PIN
  - Could use the PIN field on event site users for that
  - Have an open, blank one anyone can use
  - Multi-stage? With stage by stage validations
