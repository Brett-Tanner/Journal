# July 2024

## July 1st

- [x] Wildcard Futamatagawa SM and schedule time to fix tomorrow
- [x] Identify & fix missing snack for special day afternoon
- [x] Change some kid's name for Kamata SM
- [x] Add document submission form to the event site
  - [x] Create controller/routes
    - Email sent to SM on submission
      - [x] Create DocumentUpload mailer
        - [x] And spec
        - [x] And preview
      - [x] Basically just says 'a {category} document has been submitted' with a link to the index
  - [x] Create views
    - [x] Create policy, scope & tests for index
    - [x] Index is table with all the details accessible by SM of school submitted to, AMs
      - [x] Create or re-use the nav to filter by school
    - [x] Figure out a way to show the signed in nav bar on index rather than signed out
      - Split into unathenticated layout explicitly used in controller
    - [x] Add KU logo to new form like for new sign ups
    - [x] Give admins/SMs/AMs a button to access the index
    - [x] Translations for index & form/new

### LMS

- [x] Add temp drawing SVG
- [x] KindyPhonic has lesson plans, the button is highlighted but no link to download
  - Since I'm rendering both PhonicsClass & KindyPhonic in that col, it was overlapping and preventing the link from being clicked
- [x] On category resources, the table headings are just the category now rather than the resource type
- [x] Try sorting kids on test result page with Ruby since AR doesn't want to help
- [x] Missing English translations for user roles in the support messages
- [x] Find where I haven't translated school names & add the translation call
  - Also correct 'Ikebukuro'
  - I'll do most of this as I see missing translations I think
- [x] Move some stuff out of the admin nav into an 'Admin tasks' card
  - [x] Tidy up plans index/show since we actually link to it now
- [x] Deleting a newly added phonics resource in the form stops you submitting the form
  - Probably something going wrong with the fields controller cleanup
  - Was checking if the lesson was a new resource, not the PhonicsResource
  - Led to the wrong cleanup logic being used

## July 2nd

- [x] Translation for password length is inverted, change from SM
- Identify & fix missing snack for special day afternoon
  - [x] Get a list of all the affected students
  - [x] recalculate their invoices
  - [x] Send the lists of affected students to the SMs
- [x] Add opengraph image to Event Site
  - [x] Remember it needs to be exlcluded from .dockerignore or the whole site dies
- DocumentUpload tweaks
  - [x] Update translations with newly provided ones
  - [x] Show ALL the schools
  - [x] Add 'other description' field to be filled in if they select 'other' as document category
    - [x] Validate its presence if category is 'other'
  - [x] Hide & disable 'other description' field unless they select 'other'
  - [x] use the 'other description' field as a fallback in index if the category is 'other'

### LMS

- [x] Fix unexpected formatting issue with levelled lesson grid
- [x] Add opengraph title & description
- Add a CSVExportsController to dump the data from various tables for export
  - [x] Create policy & tests
  - Controller & views
    - [x] Index gives you links to just dump the whole table for each allowed model
- Attempt to reproduce Luis' issue with EnglishClass topics not saving #56
  - Seems to happen when he releases the lesson
  - Probably cos there's no guard clause in the code setting the topic
  - [x] Add guard clause and test to verfiy it doesn't erase when released

## July 3rd

- DocumentUpload tweaks
  - [x] Update email translation
  - [x] Add an 'uploaded_at' field to the table
  - [x] Add filters by category
  - [x] Enable deleting them
  - [x] Reverse the order schools are displayed in when selecting from the dropdown

### LMS

- [x] Add grade method to student to calc from bday
- [x] Create Curriculum tasks partial like Admin tasks
  - [x] Add course/lesson matrix link
  - [x] Move other related stuff over
- [x] Add name & date (basics), grade cols to test_result
  - [x] Add basics column to test as well so max can be set
    - [x] Will need a form field on test to input the name & date points
    - Add to all relevant views
      - [x] Test index
      - [x] Test result index
      - [x] Student page in detailed results
  - [x] Set the grade from student grade when creating the test (only when creating)
  - [x] JS calc will need updating to take name/date score into account
- Add a CSVExportsController to dump the data from various tables for export
  - Controller & views
    - [x] Allow filtering results by test
    - [x] Export all lessons as CSV as well
      - [x] Add filtering by type
      - May need to think about how to do it with aliased names for cols

## July 4th

- [x] Need to migrate in new test/result cols after deploying LMS
- [x] Add some missing kids for Monzen (to LMS)
- [x] Ikebukero has kids from Ikegami, give them the right ones
- Fix curriculum's inability to count
  - [x] Download backups
  - [x] Migrate the first score from listening to the new name/date column
  - [x] Delete all non-reading scores for Sky
  - Probably need to manually add the grades for all existing test results
    - Nope did it automatically cos the grade was nil
- [x] HAML rework of CSV index
  - [x] Add a button to download the emails of all parents who've registered for each event

### LMS

- [x] Monthly list of materials by lesson
  - Just a list of lesson titles and the materials they need for now
  - Later on think about automatically generating the full list for a month
  - Monthly materials controller
  - [x] Add MonthlyMaterialsPolicy & spec
  - [x] Add views
  - [x] Allow searching by course, week and weeks into future
  - [x] Order by lesson type then week then day
  - [x] Make the materials a ul, create a 'list_from' in application helper
  - [x] Add translations
  - [x] Give teachers access
- [x] Sort the category resources displayed to teachers by filename
- [x] Explicitly include csv gem in gemfile since postgres-copy requires it and won't be in stdlib from 3.4
- [x] Currently no way to see what level test you're looking at on results screen
- [x] Make the released checkbox when searching lessons a radio button instead

## July 5th

- Look through answers to SS questions and make notes (on wiki)
  - [x] Students
  - [x] Contracts
  - [x] Lessons
  - [x] Schools
  - [x] Settings
- [x] Come up with a tentative schedule/timeframes for adding features

## July 8th

### LMS

- Create a new branch & start chipping away at the UI rework
  - [x] Make subtitle partial a header element
  - [x] Style login page for mobile
  - [x] Add new icons
    - Add placeholder icons for non-teacher navs
      - [x] Admins
    - [x] Manually edit new icons to fit in the middle of their viewbox and fill the entire viewbox
  - [x] Dynamically recolor icons
    - [x] Explore ways to recolor them without creating partials
      - Not a thing
    - [x] Create the partials
  - Side nav
    - [x] SVGs not created from main_nav_link are taller
    - [x] Apply Alex's fixed heights
      - Had to divide all by 2
    - [x] Add the JS controller to slide it out

## July 9th

- There's no way to add category resources to courses lol. Luckily I'm not filtering by that either yet
  - Oops I am for teachers, so they haven't been able to see them
  - [x] Add course resource fields partial to the category resource form

### LMS

- Create a new branch for the new navs (teacher_ui)
  - [x] Side nav
    - [x] Uniformly align icons/text
      - [x] Match upload nav item to others
      - [x] Match theme select nav item to others
    - Fix devise/welcome pages
      - [x] Nav offsets
      - [x] Locale toggle coloring
    - Individual user navs
      - [x] Admin
        - [x] Reorient uploads dropdown
        - [x] And theme select dropdown
      - [x] Teacher
      - [x] Writer
      - [x] School Manager
      - [x] OrgAdmin
      - [x] Parent
      - [x] Sales
  - Subtitle rework
    - [x] Move it to the layout, in a slot (optionally, rendering subtitle will still work)
    - [x] Create special one for teacher page with date arrows
    - [x] Move lang toggle in
    - [x] And restyle
  - [x] Do a sweep to look for formatting issues from the new layout
  - [x] Fix it up on mobile

## July 10th

- Minus 3 hours to online lessons

### LMS

- [x] Fix disappearing support dropdown on teacher_ui branch
  - And lesson_ui
- Check changing the default background didn't break the Devise views
  - [x] Fix for lesson_ui branch
  - [x] Fix for teacher_ui branch
- Create another branch for the new lesson view
  - Welcome page
    - [x] Add flipper to enable setting available levels by org
      - [x] Figure out how to automatically create groups from organisations
      - [x] Test by adding logos to the teacher page conditional on level being enabled
    - Has the three levels of course as icons, linking to lesson index for each level
      - [x] Create card class
      - [x] Style the main element and links for mobile/desktop
  - Lesson index
    - [x] Create turbo response in controller
    - [x] Modify the seeds to have only one of each lesson per day
    - [x] And to seed the levels as features

## July 11th

- [x] Add school name to the test result export
- [x] Change the title/opengraph title for the document upload page

### In office tasks

- [x] Add all existing category resources to KU course
- [x] Upload the version of the event site with updated confirmation invoice text
- [x] Delete the SSIDs of all kids with invalid SSIDs from Leroy's CSV
- [x] Separate SSID: 2312000217 from incorrect parent
- [x] delete "akikookihara0319@gmail.com" account
- [x] Talk to Leroy about regular days in event site
- [x] Chat with Junya to clarify what some of the SS stuff is

### LMS

- [x] Fix some rounded color bleed on navs
- [x] Separate evening into keep_up/specialist features
- Lesson index
  - [x] Get the list of lessons to display
  - [x] Level nav
  - [x] Add in the universal stuff like brush up or snack

## July 12th

### LMS

- Lesson index
  - [x] Add the textless keep up/specialist svgs
  - [x] Conditionally show arrival/brush up etc only for kindy/ele
  - [x] Make sure daily activity shows up in the elementary list
    - [x] Migrate the levels up 1 to match the others (so kindy is 1, ele is land_1 which is included in ele filter)
  - [x] Merge main into lesson_ui
  - [x] Figure out how to handle the subtitle
    - Needed to use turbo streams instead of frames, not with, when updating multiple things from a single response
  - [x] Once you get here, add the changes to extend the white bg full width & adjust for mobile
- Add the modal for lesson details/resources
  - [x] Add the dialog element to the page & style
  - [x] Add the controller action and base turbo stream view
- Split out the teacher lessons/views into their own controller
  - [x] New controller
  - [x] Update all the paths
- Add the modal for lesson details/resources
  - [x] Add the tabbed one for phonics

## July 16th

### LMS

- Add the modal for lesson details/resources
  - [x] Add KindyPhonic
    - [x] And color the bottom border for phonics/kindy phonics properly
  - [x] Add the tabbed one for english class
    - [x] Extract logic for title color to helper
    - [x] Extract tabs to partial
  - [x] Add the tabbed one for daily activity subtypes
  - [x] Add the tabbed one for stand show speak
    - Didn't go with tabs since it's just the guide for each
  - [x] Add the views for category resources
    - Probably better to link them to a separate page, the existing teacher resources controller
  - [x] Add Daily Gathering after DailyActivity
  - [x] Switch to main and constrain exercise to all levels/kindy/ele, then deploy & merge back into lesson_ui
  - [x] Add tabbed exercise card
    - [x] Include all levels in all the scopes
  - [x] Add evening class cards
  - [x] Pretty sure I can condense all the send methods in teacher_lessons_controller except maybe stand_show_speak & phonics
  - [x] Close modals when you click outside them
  - [x] Do a mobile styling pass
    - [x] Extract guide section to partial
    - [x] Extract resource list to partial

## July 17th

### LMS

- Github Issues
  - [x] Move old english classes to evening classes
  - [x] Show count of students by category on index
- Add the modal for lesson details/resources
  - Do a mobile styling pass
    - [x] Login page spacing
    - [x] Teacher homepage
    - Resources card
      - [x] Header
      - [x] Guide/resources
      - [x] Size
      - [x] Stand show speak
      - [x] Tabs
- [x] Add cards to evening courses, blank links until they actually give me stuff

## July 18th

### LMS

- [x] See if I can control the title of file download tabs to be filename, not url
- [x] Allow organisations to have multiple courses again
  - [x] Add tests checking that multiple courses work
- [x] Scope phonics resources by the current week (on lesson_ui branch)
- Add a weekly/monthly calendar view of missing lessons
  - [x] Add the table and display logic

## July 19th

- [x] New LMS timeline stuff for Leroy

### LMS

- [x] Courseable should be on the organisation, not users
- Add a weekly/monthly calendar view of missing lessons
  - [x] Only show released lessons
  - [x] Allow filtering by date
  - [x] Allow filtering by org
- [x] Move the code fetching phonics resources to the controller, same with the regular resources
- [x] Basic missing lessons styling on lesson_ui branch
- Support pages styling
  - [x] Index
    - [x] Request summary partials
    - [x] Add priority col to support request
  - [x] Show
    - [x] Mobile views
  - Form
    - [x] Add priority to form & controller
    - [x] Add images to form & controller
    - [x] Overall layout

## July 22nd

- [x] Come up with a way to stop parents registering blank invoices
- [x] Remove ability to create orphans

### LMS

- Support pages styling
  - [x] Form
    - Add images to form & controller
      - [x] Validate images are of correct type
      - [x] Add image attachments to support messages
      - [x] Show them in request/message views
    - [x] Priority toggles
    - [x] File upload
  - [x] Separate the index into active/resolved

## July 23rd

- Come up with a way to stop parents registering blank invoices
  - [x] And show them in the list so they can be deleted if they exist
  - [x] Fix the one Leroy messaged me about
  - [x] Fix 6964
  - [x] Delete the orphaned 'Kokono Teshima's
- [x] Possible issue with Magome SM link to old summer school 2023

### LMS

- Add a list of blobs, sorted by file size, or by file size x download count
  - [x] Add the route, and update policies/tests
  - [x] Create the view/action
- [x] Make the pdf_image field flex-col so it doesn't disappear if a big image is uploaded
  - [x] Add a small info with image size, filetypes
  - [x] Stop the rendering error when there's a validation error and they're sent back, caused by uploaded image not being persisted
- Tutorials Section
  - [x] Merge Jayson's changes
    - Can push with to the PR `git push git@github.com:JaysonPye/materials.git HEAD:main`
    - [x] Seed rickroll
    - Refactor VideoTutorial link conversion to be done in model
      - [x] Add tests
      - [x] Refactor to pass
    - [x] Tidy forms
      - [x] Use the VideoTutorial valid hosts constants to provide guidance on form
      - [x] Use string interpolation to render correct forms
    - [x] Fix the failing tests
      - [x] Figure out the stimulus generator messed up my index.js again
      - [x] Change Tutorial Category name to title in tests

## July 23rd

- [x] Fix invisible fonts in event site confirmation PDF
  - This took 2.5 hours, turned out to be an obscure edge case in the new version of Prawn
- [x] Chase down issues Luis is having with viewing resources
  - [x] Info from Jayson lead me to noticing PPTx files can't be embedded plain in browsers

### LMS

- Tutorials Section
  - [x] Add attached SVG to TutorialCategory
  - [x] Add 'sanitized_svg' helper to display SVGs from ActiveRecord
  - [x] Fix the update links for tutorials, turns out they actually did need to be set manually

## July 24th

- [] Writers can't propose changes to at least lesson 354, form just resets with no errors
  - Can propose changes to some others though
- Need some way of doing the early bird discounts for parties
  - They could be different per school
  - Some schools (new ones) can do free events
    - Just add a separate 0 cost price list for that event
- [] Need a separate column for food allergy, boolean
  - [] After Summer School, change it so allergy kids can't see the option for lunch
  - Set by a radio button
  - Parents get a splash on their page & kid's page telling them to update, redirected if they try to register
- [] Try switching on force.ssl for both sites
- [] Look into setting up emails for our new domains
- [] SMs need a test school on event site for training
  - Will need to exclude it from the real scope
- [] Add Alex's new notification svg once I merge all the UI stuff

### LMS

- Tutorials Section
  - [] Styling
    - [] Style new tutorial dropdown & new category link
    - [] Show cards for each category on the tutorials page
    - [] Remove the 'TurboModal' stimulus controller and use my lesson modals
      - [] Refactor a bit to make the modal more general
      - e.g. make the id/classes more generic, create a partial
  - [] Add TutorialPolicy/TutorialCategoryPolicy & tests
- [] Add conditional to files controller to download rather than embed if .pptx
  - [] Find out what other filetypes this might apply to
- [] Change the custom key generation for plans to put the lesson title first
- [] Add pictures page to DailyActivity plans
  - [] Add the has many and form fields/controller stuff
  - [] Add to list of attributes on model
- [] Create Exercise template
  - [] Refactor the code for PDF templates to be more reusable across different types
- [] Textless icons from Alex
- [] Fonts might look weird cos I'm just making them bold, not using the actual bold version
  - A guy on the Syntax podcast mentioned this mattered
- [] Add a way to upload lessons from a CSV
- Automatically:
  - [] Create default teacher and class when new schools create
  - [] Add uploaded students to their school's default class
- [] Add a UI for viewing/rolling back to previous versions of students
  - [] Remove limit on versions of students stored
- [] Might need to reverse the lesson form/fields relationship at some point, partial locals are an issue
  - Noticed this on phonics class, with the associated phonics resources
- [] Provide a list of kids who could move up for each test
- [] Delete the 'LessonUses' controller and move it to CourseLessons#index, since that's what it really is
  - [] See if there's anything stopping me just using a CourseLesson form, rather than `fields_for` in a form
  - [] Add the date fields and CourseLesson update/create actions to enable adding lessons to courses easily
- [] When updating upload progress, decrement failures if sum of all > total
- [] Refactor the PDF generation
  - The endless 'draw\_\_\_\_' methods seem like they could be extracted
  - Probably different versions for plaintext, lists and links
- [] Add a 'quit_chance' enum to students, next to the comments section
  - Revisit after SS meeting to decide what the enum values will be
- [] Add filtering by date to Lesson search
- [] Add filtering by unattached to lesson search
- Implement notifications
  - From listening to podcasts these can often be different types with STI, if we even need that much complexity
  - [] When lessons haven't been updated in 2 years
  - [] When there are new (relevant) support messages
  - [] Manually send notifications to subsets of people

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
