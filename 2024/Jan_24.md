## January 4th

### Setsumeikai Calendar

- [x] Do the switch

### [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [x] Fix up some mising info on Schools/a missing SM
- [x] Add the 3 course to price lists
  - [x] Change the model
  - [x] Change the forms
  - [x] Push, then add the 3 course
  - [x] Change the code in Invoice#calc_cost

## January 5th

### [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Make other associated modifications to the costs
  - [x] Default lunch & dinner options from 660 > 770
  - [x] Repeater discount is now for 5 or more registrations, not 10
  - [x] There's now a 1 course (officially, price changed as well)
    - Ele and kindy pay same for the new 1 course, so no more pointless price
- Add close_date field to TimeSlot, saves me having to edit the hash every event
  - [x] Add & run the migration, push
  - [x] Add close_at tests
  - TDD kindy/ele modifiers
    - [x] Add the code to use them in calculations

## January 9th

- [x] Finish outline for Leroy
- [x] Alter WP site page slugs to match seasonal school ids
- [x] Edit WP theme templates to produce a URL in the correct format

### [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [x] Add temp exception to repeater discount being 5 till all SMs do their job
- [x] Let SMs delete inquiries since customers seem to like sending multiple
- [x] Fix an error where I was using the sum on every iteration when reducing the extra cost, regardless of whether it applied
- [x] Remove links to setsu/inquiry stuff from SM profiles
- Add close_date field to TimeSlot, saves me having to edit the hash every event
  - TDD kindy/ele modifiers
    - [x] Test their inclusion in the summary
  - [x] Show kindy/ele modifiers where extra cost is shown (as extra cost)
  - [x] Add form fields to actually set the values

#### HAML Refactors

- [x] TimeSlot event form
- [x] TimeSlot#event_slot_fields

## January 10th

### [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [x] Realise I'm missing policy/request tests for charts and write those
- [x] 'All/Area schools' for surveys is broken, individual schools fine
  - Was breaking due to children without parents, couldn't display phone/email for nil
  - Can end up with parentless children when merging, since the responses aren't copied and they prevent the SSIDless child being deleted
  - Added safe navigation, and copied survey responses during child merge
- [x] Bump Puma to 6.4.2 to avoid request smuggling vulnerability
- [x] Add English translations for Stats categories
- [x] And why none have been sent to GAS
  - They are being sent, but GAS isn't updating send_flg. No dupes so fine for now I guess
- [x] Let statistician see setsu/inquiry stats
- [x] When AM/Admin clicks on a school to view Setsu stats for, still shows all schools
  - [x] Add requested graphs (separate for held/created setsu, inquiry category pie chart etc.)
  - [x] Remove null from referrer pie chart
  - [x] Limit inquiries per setsumeikai to setsu inquiries
- [x] List events they apply to under price lists
  - [x] And in the edit view
- [x] Disallow blank survey response submissions

#### HAML Refactors

- [x] Charts#setsumeikais
- [x] PriceList partial
- [x] PriceList#index
- [x] PriceList#edit
- [x] PriceList#new

## January 11th

### [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [x] Adjustments snuck into the middle of the summary, put them back on the left edge
- [x] Figure out why/how there are inquiries for Online
  - It was because I also made them Ikebukero SM for some reason, was getting their inquries as well
  - Also had an issue with the inquiry index erroring because Online isn't a real school, so made default school the managed school
- [x] Do a run through of creating Spring School in dev env, check all the views etc. work with 2 events
- [x] Finish off the time slot edit form that got lost yesterday
- [x] Show multiple events on child/parent pages if available
- [x] Create Spring School
- [x] Manual adjustments to special arvo snacks and arvo close_at

#### HAML Refactors

- [x] TimeSlot#edit

## January 12th

To fix the rubocop linter in nvim using the wrong version, change the lsp setup like this:

```
require("lspconfig").rubocop.setup({
  cmd = { "/home/brett/.rbenv/shims/rubocop --lsp" },
})
```

- [x] Birthday/grade mapping was off because not using April as start of year or taking current date into account
- [x] Auto-scroll to top wasn't happening on Setsu form summary because pathname didn't change
  - So changed the useEffect dependency to the whole location object, which does change because of the hash

### [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [x] Modify auto afternoon creation to use the same close at as the morning, rather than the default
- [x] Sort events by school id within start date on index

##### Testing

- [x] Create copy of Spring school in my (desktop) local dev environment

## January 15th

### [Materials](https://github.com/Brett-Tanner/materials)

#### Documentation

- Create user stories for
  - [x] External teacher
  - [x] External manager
  - [x] KU teacher
  - [x] KU curriculum
  - [x] KU sales
  - [x] KU admin
- [x] Make & embed a quick outline of the DB schema

### [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [x] Filter inquiries by setsumeikai/general
- [x] Add auto-unsubscribe button to emails to meet gmail/yahoo requirements

## January 16th

### [Materials](https://github.com/Brett-Tanner/materials)

#### Views

- Scaffold course views

  - [x] Index
  - [x] Course table partial
  - [x] New/Edit
  - [x] Form partial
  - [x] Show

#### Files

- [x] Add basic uploads
- [x] Add basic downloads
- [x] Add breadcrumbs
- [x] Add ability to make new folders
- [x] Implement uploads to current folder
- [x] Add navigation back to previous folder
- [x] Add navigation forward to nested folders

## January 17th

- Set Jayson up with an AWS account for his Elastic Beanstalk
  - [x] Invite his personal account
  - [x] Then cancel that, bad idea
  - [x] Make him get a new account just for work
- Add a search to the school index on main site
  - [x] Write basic JS to hide/show results
  - [x] Basic HTML for the form
- [x] Endless meetings
- [x] Talk out a basic structure for lessons with Daniel, took pictures of the sketches

### [Materials](https://github.com/Brett-Tanner/materials)

- [x] Bump to Rails 7.1.3

### [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [x] Add the event_summary table to one of the charts views

## January 18th

### [Materials](https://github.com/Brett-Tanner/materials)

- Files controller is now just a file explorer rather than primary method of access/storage, so decouple from courses
  - [x] Add index action that lists all course folders
  - [x] Decouple all the partials from reliance on course_id
  - [x] General cleanup of code quality in those views/controllers

#### Lessons

- Model for each category, all inheriting from a base class
  - Base class has title, summary, category, week, day, references a course and has attached materials (attached files)
  - Start with daily activity & exercise
    - Links and steps for both as array column
    - Each have different subcategory enums
- Has to be backed by a single database table so it can be referenced from other tables
- Each model can generate a PDF plan from a template

- [x] Create & test base Lesson model
- [x] Add a basic main nav
- [x] Write a system test for creating a DailyActivity lesson
- Pass that test by:
  - [x] Adding the role enum to User
  - [x] Creating a migration/model/factory for Organisations so Users can be associated with them
  - [x] Adding steps and links columns to Lesson
  - [x] Creating the DailyActivity model & testing its validity
  - [x] Fiddle with rails_helper for a while to get system tests running with Rack::Test, not selenium
  - [x] Correctly subclass DailyActivity from Lesson, and reorganise folders to match
  - [x] Add an 'Add lesson' dropdown to Course#show
  - [x] Create controller actions for DailyActivity creation
  - [x] Make day an enum on Lesson so we have human readable days mapped
  - [x] Create views for DailyActivity creation

## January 19th

### [Materials](https://github.com/Brett-Tanner/materials)

- [x] Long meeting to get Jayson set up with organisation AWS account
- [x] Set up an SCP so he can only access EB
- [x] Stop pretending the 1 course is spot use on invoices
- Main site tweaks
  - [x] Limit month range to next 2 months
    - [x] Write tests
    - Can do with validRange prop to calendar component
    - Takes start and end arguments in form 'YYYY-MM-DD'
  - [x] Add month title/navigation to footer as well as header
  - [x] Scroll to top of calendar when month changes
- Realise Rails has built in STI support and try using that
  - [x] Rename category enums to a 'type' string column
  - [x] And subcategory to subtype
  - [x] Add inclusion validations to compensate for the removal of enums
  - [x] Update tests if needed
  - Had quite a few issues compared to using the enum I had set up already
  - Will need to look into it properly and weigh pros/cons

## January 20th

### [Materials](https://github.com/Brett-Tanner/materials)

- [x] Switch to Rails' built-in STI
- [x] Add #split_on_capitals to Applicationhelper
- [x] Split shared lesson form fields into their own partial
- [x] Create Exercise model/form

## January 22nd

- [] Finish off the search functionality for the main site school index

### [Materials](https://github.com/Brett-Tanner/materials)

- [x] Create form errors partial and include it in the lesson form/all others going forward
- [] Use '\_url' helpers in #redirect_to to conform to spec

#### Lessons

- Write a system test for creating a DailyActivity lesson
  - Pass that test by:
    - [x] Adding a DailyActivities controller with only a create action
    - [x] Creating Lesson#show action/view and daily_activity partial
- [x] Rather than rendering a form for each lesson type, render the shared form then a partial for each lesson type
- [x] Extract lesson_params into a concern that can be included in and merged in type controllers
- [x] Write scaffold tests for DailyActivity#set_links & #set_steps
- [x] Move lesson controllers to a subfolder
- [] Add has_one_attached :guide to Lesson
  - [x] Test guide PDF generated with correct key
  - [x] Add level enum to base Lesson
  - [x] Autocreate guide on lesson creation

## January 24th

### [Materials](https://github.com/Brett-Tanner/materials)

#### Lessons

- [x] Add has_one_attached :guide to Lesson
  - [x] Remove unnecessary whitespace from links
  - [x] Fix infinite loop when updating lesson
    - Was caused by calling purge on the guide attachment
    - Moved the call to save_guide to the controller in an after_action hook
    - But not happy with this solution, should be on the model
    - Revisit later
  - [x] Add check for guide download link to system test
  - [x] Test PDF content
  - [x] Resolve a bunch of gem dependency issues with poppler
  - [x] Add check for guide preview to system test
  - [x] Add guide preview to Lesson#show
- [x] Preprocess guide thumbnails as AVIF
- [x] Add timestamp to last part of guide key
- [x] Figure out how to have lesson factories inherit from a base factory like the models
- [x] Create & test guide creation for Exercise

## January 25th

### [Setsumeikai Calendar](https://github.com/Brett-Tanner/setsumeikai_calendar)

- [x] Just don't show next buttons if they can't be clicked

### [Materials](https://github.com/Brett-Tanner/materials)

### Lessons

- Extract link and step logic into concerns to be shared amongst lesson types
  - [x] Create the new concerns
  - [x] And DRY the tests once I've verified they still pass using concerns
  - [x] Same for the related partials
  - Add tests for more complex validations and their errors like
    - [x] empty/partial inputs
    - [x] valid URLs (just checking for http:// or https://)
- [x] Figure out a way of moving the save_guide method to the model without infinite loops
  - Or maybe just inherit the controllers so you can have the after action in all subs automatically?
  - Ended up extracting it to the LessonsController and inheriting from that in all the subtypes
- [x] Minor styling tweaks for meeting
- Create CourseLessons to allow lessons to belong to multiple courses
  - [x] Migrate in the table
  - [x] Change associations
  - [x] Create a partial for CourseLesson fields and add a Stimulus FieldsController
  - [x] Change routes/controller code
  - [x] Create Lessons#index and subcontroller indexes + view

## January 26th

- [x] 3 hour meeting with Leroy/Daniel/Luis
- [x] Add setsu stats Jack wanted (like in the admin chat)
  - [x] Add totals for each col at the top

### [Materials](https://github.com/Brett-Tanner/materials)

- [x] Remove root_path from Course, not necessary anymore

### Lessons

- [x] Styling tweaks, sorting lessons by type on Courses#show
- Create CourseLessons to allow lessons to belong to multiple courses
  - [x] Move week and day from Lesson to CourseLesson table
  - [x] Add lesson_fields partial for adding lessons to courses
  - [x] merge lesson_fields partial with courses_fields partial
  - [x] move concern callbacks (linkable, steppable) into their concerns
  - [x] test adding an image to a PDF with exercise

## January 29th

- [x] If a month is empty on the setsumeikai calendar, immediately show the next month
  - [x] Also check how far in the future we are and stop if > 3 months to avoid infinite scroll

### [Materials](https://github.com/Brett-Tanner/materials)

- [x] Add basic seeds using FactoryBot to save me some typing
- [x] Rename curriculum type to writer
- [x] Remove students_count from organisation, add it to school later & calculate from Organisation#students_count
- Generate Devise views
  - [x] Convert to HAML
  - [x] Add basic styling

### Lessons

- Require authentication to access site
  - [x] Add welcome page & devise sign in/up links
  - [x] Add devise layout
  - [x] Create different roots for authenticated/unauthenticated users
  - [x] Require sign_in for all actions
  - [x] Add locale scoped routes and locale switching based on them
  - [x] Modify User#is?() to take array of roles and test
  - [x] Auto-redirect user based on type at sign-in
- Add Pundit for Lessons
  - [x] Add scaffold for other user types so they can be included in auth testing
  - [x] Tests
    - [x] Add requirement to be part of KidsUP
    - [x] Add policy_scope tests
    - [x] Actually call policy_scope/authorize in controllers and enforce them being called
    - [x] Inherit policy_class from Lesson so I don't need to write a new one for each subclass
  - [x] Write the pundit models

## January 30th

### [Materials](https://github.com/Brett-Tanner/materials)

- [x] Create JS flash_controller
- [x] Start using SolidQueue
- [x] Install & secure PGHero

#### Organisations

- [x] System test for sales creating an organisation
- [x] Create & test pundit policy
- [x] Add validations
  - presence of name, email
  - uniqueness of name, email
- Scaffold views
  - [x] Index
  - [x] Card
  - [x] New/Edit/form

#### Users

- Create & test pundit policy for each user type
  - [x] Validate that admins, curriculum and sales can only be created for KU
  - [x] Policy scopes for all users
  - [x] Scaffold School & Managements join table

## January 31st

- [x] Give Jack his total attendance count in the setsu stats table

### [Materials](https://github.com/Brett-Tanner/materials)

#### Users

- [x] Extract authorized user shared examples to support folder if possible
- Create & test pundit policy for each user type
  - [x] AdminPolicy
  - [x] WriterPolicy
  - [x] SalesPolicy
  - [x] Only include VISIBLE_TYPES in sales' user policy scope (remove admin and writers)
- System test for creating each user as lowest permissioned user who can
  - [x] Writer
  - [x] Sales
- Scaffold user views so I can test out how STI links work with Pundit
  - [x] New/Edit/shared user fields
  - Nav for each type
    - [x] Admin
    - [x] Writer
    - [x] Sales
  - Show for each type
    - [x] Admin
    - [x] Writer
    - [x] Sales
  - Form partial for each type
    - [x] Admin
    - [x] Writer
    - [x] Sales
  - Per-type Index
    - [x] All users
      - [x] Split navs into partials
      - [x] Extract user scoping into controller method
      - [x] Decide to just use default index for now & super the scoped users
