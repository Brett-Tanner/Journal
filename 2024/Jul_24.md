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

### LMS

- Tutorials Section
  - [x] Update seeds to include the required svg on tutorial categories
  - [x] And factory/tests to use it
  - [x] Styling
    - [x] Style new tutorial dropdown & new category link
    - [x] Show cards for each category on the tutorials page
    - [x] Remove the 'TurboModal' stimulus controller and use my lesson modals
    - [x] Style modal header
    - [x] Style FAQs section
    - [x] Style Files section
    - [x] Style Videos section
      - [x] And figure out how to open the videos in a separate modal
  - [x] Add TutorialPolicy/TutorialCategoryPolicy & tests
  - [x] Add edit/delete buttons for admins on tutorial categories/tutorials
  - [x] Remove the vestigal views for the old UI
- [x] Roll back to the previous file controller implementation that just sends it for now
- [x] Files index does not need to be human size for download count
- [x] Last column should be 'bandwidth used'
- [x] Update icons
- [x] Override hover effect on resolved badge
- [x] Stop videos playing when their dialog is minimized
- [x] Push to live, run migrations, and turn on/create Flipper features
  - [x] Lessons showing up multiple times
    - Was policy scope duplicating it endlessly
  - [x] Special lesson missing
  - [x] Evening class stuff overlaps the SVG

## July 28th

- Deal with SM issues
  - [x] Kid who was kindy/is now elementary needs extensions changed
  - [x] August 5th PM has the wrong name
  - [x] Kid needs to be linked with parent? Somehow created without SSID/link to a parent
    - Ended up being Leroy's job
- [x] People use the attendance sheet on iPads, and it goes off-screen on those
- Add new seasonal days
  - [x] Monzen 19-21
  - [x] Monzen 22
  - [x] Oi special day 31st
- [x] Stop SMs shooting themselves in the foot by adding children without SSIDs
- Add stuff I need to make parties work on the event site
  - [x] Add a 'released' column to events so we can test/modify them first
    - [x] Filter unreleased events out in customer/child controllers
    - [x] Add the checkbox to the form & the param to the controller
  - [x] Skip option creation and afternoon slot creation for party time slots
  - [] Have early bird discount dates, they can be different per school
    - [x] Add an early bird date & discount to the event table
    - [x] Add the early bird fields to the form
    - [x] Apply the early bird discount (as an adjustment) if before early bird date
    - [x] Refactor adjustment tests
      - use let to set change/reason
      - lets me use the same find adj method for all
  - [x] Some schools (new ones) can do free events
    - Just add a separate free price list for that event
    - [x] Create a 'Free Promo Event' price list to be used for these
    - [x] Check doing that works as expected
  - [x] Add seeds for parties

### LMS

- [x] Truncate goal/subheading text so it can't hide guides
- [x] Stand Show Speak dialog should be just like the others
  - The scripts are added as resources, the guide is just a general monthly one

## July 29th

- [x] Bring back staff ability to add kids, but make sure they're linked to a parent
- Add new activities for summer school
  - [x] Change dates/pics for Monzen
  - [x] Ikegami 9/7
  - [x] Togoshi 9/1
  - [x] Nagahara 9/1

### LMS

- [x] Next/prev day buttons don't target the frame
- [x] Language toggle gives you a white screen on lessons, just remove it?
- [x] Monthly materials should default to 1 week from now
- [x] Now that SSS is basically the same, really feel like I could just use the same partial for all lesson turboframes with some helpers
- [x] Figure out how to stop the headings overlapping the icon
- [x] Refactor the PDF generation
  - [x] Create factory for body items
  - [x] Extract footer logic to module
  - [x] Create factory for header items
- [x] Add pictures page to DailyActivity plans
  - [x] Add to list of attributes on model
  - [x] Add the form field
  - [x] Add the page generation logic as a module
  - [x] Refactor PDF footer component to include optional page numbers
- Create Exercise template
  - [x] Remove from list of skipped types
  - [x] Add (temp) background image
  - [x] Add missing fields
    - [x] To model
    - [x] Alias the ones that are egregiously different
    - [x] Update factory
    - [x] Update system & model specs to expect PDF

## July 31st

### LMS

- [x] Create Exercise template
  - [x] Add header section
  - [x] Add language goals
    - [x] Extract language goals to component from DailyActivity
  - [x] Add body text
    - Headings are all over the place with indentation, I'm gonna assume Alex cleaned that up
  - [x] Add body images
    - [x] Add to model
    - [x] Add to form
    - [x] Create a component to wrap them in bounding boxes for more reliable positioning
    - [x] Add them to the PDF template
  - [x] Refactor the factory calls to be one per type, name them separately
  - [x] Add the footer to each page
  - [x] Verify system & model specs pass
