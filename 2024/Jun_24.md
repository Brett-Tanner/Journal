# June 2024

## June 3rd

- [x] Start cron job article on wiki
  - Set one up to sweep SQ jobs older than a week
    - [x] For LMS
    - [x] For event site
  - [x] One to get PGHero stats
    - Requires messing with RDS settings so skipping this one
- [x] Copy docker_entrypoint from event site
  - Tried but failed, I think an issue with the file extension? It looked different without a \* but adding one failed the deploy
  - Just trying it without the extension this time

## LMS

- [x] Bump propshaft to 0.9
- [x] Make the test result entry table at least readable with new styles
- Add level SVGs where appropriate
  - [x] Organise assets/icons into folders without breaking anything
  - [x] On teacher profile
- [x] Improve levelled lesson styling & add KeepUp/Specialist
- [x] Add a level_icon helper for lessons
  - [x] And refactor the icon_filename method out into a helper as well
- [x] Only allow PDF uploads for lesson guides
- Address Github issues
  - [x] Add separate columns for en names
  - [x] Add kindy row to levelled lessons

## June 4th

- [x] Only show the "don't select regular days" message to internal students
  - [x] Extract child switcher to a HAML partial
  - [x] Chase down potential 'copy_regs' issue
    - Was just because all the slots were closed on test event
- [x] Add a 'wildcard' carveout to the SM IP check so we can make sure we always have the ability to give them access
- [x] Add GTM to main layout and remove the page-specific tags
  - [x] Remove the Clarity tags
  - [x] And fix BS validations not applying on turboload
- [x] Chase phantom 'Allergy not entered' issue on event site
  - Can't reproduce

## LMS

- [x] Test new filepath helpers
- Change Exercise to not generate guides
  - [x] Add to list of skipped classes in Pdfable
  - [x] Cut down form fields to guide/resources/basic stuff required

## June 5th

#### In-office tasks

- [x] Try new docker_entrypoint
  - Failed again, with a permissions error
  - Tried changing the permissions, failed for a different reason
  - Gave up again for now and will just migrate manually
- [x] Manually fix the PPT guide uploads for lessons 48 & 49
  - [x] Discover and fix edge case with short name for keep up having space in it, leading to icon path breaking
- [x] Test whether the event site is correctly receiving IPs from the docker container
  - Certainly seems to be from the logging, will need to do some real-time testing with the affected SMs

## LMS

- [x] point 'materials' subdomain of 'kids-up.app' at the LMS
- [x] Make resource dropdowns absolutely positioned in a relative container so they don't shift the layout
- [x] Grey them out when there aren't any attached resources
- [x] Sort searchable resources by most recent, only show the last 10
  - But still show unlimited results for searches
- [x] Show kindy phonics on teacher page
- [x] Extract the logic for checking guides are uploaded to PdfUploadable concern
- [x] Fix resources details element having higher z-index than summaries that drop down from them
- Address Github issues
  - [x] Add KindyPhonics
    - [x] Write a system test for creating one
    - [x] Create model, factory and unit tests
      - [x] Alias 'example sentences' as 'blending words'
      - [x] Should automatically set level as kindy
      - [x] Exclude from guide generation
    - [x] Create and controller & views
  - [x] Add 'Special' (blank) lessons
    - [x] Write a system test for creating one
    - [x] Create model, factory and unit tests
      - [x] Exclude from guide generation, only resources and title
    - [x] Create views and controller
      - [x] Hide the guide partial
      - [x] Show them to teachers
- [x] Get a download SVG and add it where appropriate
  - [x] Resource dropdowns (internal)
- [x] Also add separator to the resource dropdown

## June 6th

- [x] Get constantly interrupted by fixing SM's IP addresses in the event site
- [x] Figure out why confirmation emails are failing
  - Was calling `calc_course_cost` directly, but not passing the new slots arg that's required
  - Also relied on the existence of @data
  - passed a list of slots, and removed reliance on @data (partially, probably a better solution than initializing it blank if not present)
  - [x] Wrote mailer tests to make sure it doesn't happen again
- Write tests for all the other mailers
  - [x] InvoiceMailer.updated_notif
  - [x] InvoiceMailer.sm_updated_notif
  - [x] InquiryMailer.inquiry
  - [x] InquiryMailer.setsu_inquiry

## LMS

- [x] Add missing control svg (temp)
- [x] Create PhonicsLesson template
  - [x] Add background image
  - [x] Header section
    - Level, title, goal
  - [x] Image
  - [x] Materials
  - [x] Instructions
  - [x] Adding difficulty
  - [x] Extra fun
  - [x] Notes
  - [x] Links
  - [x] Footer level

## June 7th

- [x] Fix the preview when you paste it into a chat
- [x] Set up promo site repo for Mike
  - [x] Write some docs on how to use it
  - [x] Set up a branch to auto-deploy to cloudflare

## LMS

- [x] Set up emails now we have a domain
- [x] Add new icon and favicon
- [x] Update DailyActivity template with new bg image
  - [x] And tweak positions to fit
- Get a download SVG and add it where appropriate
  - [x] Guide buttons
  - [x] Guide preview download
  - [x] Lesson resource download (curriculum side)
  - [x] Sample CSV download
- [x] Add delete SVG to resource list
- [x] Add kindy/ele subtitles to unlevelled lessons
- Address Github issues
  - [x] Mask the corners of uploaded images to make them rounded
    - The idea I had doesn't work, so letting curriculum do this manually
  - [x] Add Evening Class
    - [x] Write a system test for creating them
    - [x] Create model, factory and unit tests
      - [x] Exclude from guide generation
      - [x] Custom levels enum with only specialist/keep up/tech up
    - [x] Create views and controller

## June 10th

- Lazy load images by default
  - [x] LMS
  - [x] Event Site

## LMS

- [x] Actually filter out unreleased lessons in the teacher view
  - tell Lu to approve them or I just bulk approve all existing lessons
- [x] Add next day/week arrows to the teacher profile
- [x] Don't download resources/guides in a new tab for no reason
- [x] Add a separate tab for KeepUp/Specialist
  - Just put it at the bottom of levelled lessons for now, will revisit when we add Keep Up
- Address Github issues
  - Sort resources
    - [x] On teacher profile
    - [x] On lesson#show
  - [x] When lessons are used multiple times in a course, show them with the correct dates

## June 11th

- [x] Remove mini-profiler
- Chase down intermittent JS issues
  - [x] Write a JS enabled system spec to run on a loop until it fails
  - [x] Check out stimulus/turbo rails issues on Github to see if it's a known issue
    - No luck
  - Create versions that work without JS if not loaded
    - [x] Allergy field
      - [x] Refactor child form to HAML
      - [x] Implement the fallback version if JS is not loaded
      - [x] Reimplement the original version with AllergyController
    - [x] Sign up form
      - Button enabled by default, JS disables until box checked
      - backend verification that policy accepted
- [x] Fix content missing for merge children form submission
  - Was missing '\_top' on the submit, meant it was trying to find a frame on child page

## June 12th

- [x] Check SQ isn't overloading the RDS instances
  - Sitting at 3 and 5% CPU usage, so probably not.
- [x] Realise vendor/javascript is required by sprockets, so recreate it and the .keep file to be safe
- [x] Approve all existing lessons after pushing the update with release filter for teachers
- [x] Create statistician accounts for Jack
  - [x] Add a way for admins to create users with other roles in the UI
    - [x] Policy & tests
    - [x] Controller, routes
    - [x] Views
    - [x] Add the ability to add managements in the form
      - HAML refactors
        - [x] Management fields partial
          - [x] And make it more generic
        - [x] Area form
        - [x] School form
  - [x] Point the "Edit SM" button on the SM profiles to the new form
  - [x] Remove the "allowed IPs" and other staff related stuff from the generic user form

## LMS

- [x] Teacher logins need to be locked to their school's IP
  - But only for KidsUP
  - Put the allowed IPs on the schools, since a Teacher can have multiple schools
  - Have a head office school with the wildcard IP
  - [x] Write request specs for the desired behaviour
  - [x] Write the filter in application controller

## June 13th

- [x] MEETINGS

## LMS

- Teacher logins need to be locked to their school's IP
  - Add the necessary fields
    - [x] IP on school form
      - [x] With backend validation
      - [x] And tests
        - they're breaking since IPAddr apparently needs a family now????
    - [x] Teacher fields (school teachers) on school form
      - [x] accepts_nested_attributes_for
      - [x] partials
  - [x] Add teacher list to School page
- [x] Add delay between uploads
- [x] Add en_name to student_uploads
  - [x] In model (constant passed to JS)
  - [x] In explainer
    - [x] Generate table headers and '...' from CSV_HEADERS
  - [x] In JS
    - [x] And refactor table creation to generate from CSV_HEADERS on model
  - [x] In turbo response
    - [x] And refactor to generate from CSV_HEADERS
  - Refactor the other uploads to also generate from CSV_HEADERS
    - Parents
      - [x] Explainer
      - [x] JS
      - [x] Turbo
    - Teachers
      - [x] Explainer
      - [x] JS
      - [x] Turbo
    - [x] Extract all types to declarations.d.ts
    - [x] Extract everything but the table header functions to the main table.ts
- [x] Get child data for test schools for Luis
  - Sent to Leroy to add the levels

## June 14th

## LMS

- [x] Change teacher welcome to Today's Lessons
- [x] Change guide text to 'Lesson Plan'
- [x] Make resources dropdown a pointer cursor
- [x] Shrink the icons on levelled lessons
- [x] Skip Sat & Sun when advancing day by day on teacher profile
- [x] Stop displaying "today's lessons" in the past
  - [x] And show 'Past lessons for #{date}' instead
- [x] Errors on teacher form throw a 500 because they're missing data for the selects
  - [x] Do a sweep for similar instances of not setting form data/to normalise the naming
- [x] Try out logidze for version tracking on students
  - [x] Install
  - [x] Run existing tests
- [x] Add current & former scopes to students
  - [x] Find and fix issue with some student params not being allowed in strong params
- [x] Remove ability to delete students (already no buttons, does the route exist?)
- [x] Add student list to School#show
- [x] And alter create links/controllers to autofill school
- [x] Refactor Lesson.replace to actually update the lesson in place rather than replacing it
  - [x] Then add logidze to track the last version of lessons
  - Add views and controllers to view the version and revert to them
    - [x] Controller
    - [x] View
  - [x] Figure out why there's an \r getting appended when updated with no changes
- [x] Open lesson guides in new tab, and inline by default

## June 17th

- [x] Chase down the JS/CSS issues with old browsers
  - Turns out they were two separate issues
  - Tailwind on the LMS uses stuff like `color-mix` which only has support in recent browsers, just for normal colors
  - Whereas on the event site it's the JS which wasn't working
- [x] CSS needed a PostCSS postprocessor plugin to add fallbacks to old browsers (seemingly mostly by hardcoding the colors)
- [x] JS was caused by turbo-rails > 2.0.1 dropping the shim that enables importmaps on old browsers
  - Meant none of the JS was being loaded as everything on the event site is through importmaps
  - So added the shim back myself and it was all good
- [x] add content-type to the FilesController (from the blob)
- [x] Add en_name to student form
- [x] Align the list of tests like #55
- Give staff the ability to add teachers to a class, not just students lol
  - [x] From school_class form
  - [x] From teacher form
- Figure out what's up with the test result entry
  - [x] Student page not loading when test result entered correctly
    - Because total score method is trying to sum all the answers, which are stored as strings
    - Added a before validation hook to map over answers and convert to int

## June 18th

## LMS

- [x] Class fields are outside the main form, move them inside so they actually work
- [x] Figure out what's up with the test result entry
  - [x] JS not showing the reason popup
    - Is actually an issue with the backend validation, I think it's taking the first threshold it finds rather than the highest one
  - [x] Luis also having an issue with the flash message not showing, nothing happening when form is submitted
    - Can repro on Chrome, it's probably the form being wrapped around the table row again
    - Might be something Firefox allows but isn't part of the spec so the others don't
- [x] Fix various `accepts_nested_attributes_for` issues
- [x] Bulk assign the uploaded students to their school's classes
- [x] In student errors partial the Japanese name is filled into the en_name field, saves as JA value
- [x] Add logidze policy and tests for the lesson versions controller
  - Can be handled by LessonPolicy
- [x] Get Jack a list of which emails sent to staff contain kids' personal info
- [x] Initial setup of new laptop
- Close other resource dropdowns when one is opened
  - [x] Using the name attr (only in newer browsers)

## June 19th

## LMS

- [x] Add english 'you need a reason' translation
- [x] Fix reason box still being shown when reselecting recommended level
- [x] Don't automatically move up kids if they're going to an evening course
  - [x] Highlight row and add flag if evening course threshold passed
  - [x] Also highlight rows if they could go to evening course when the row is first loaded
  - [x] Change the backend automove code to move to Galaxy 2 if they'd go to evening
- Close other resource dropdowns when one is opened
  - [x] Add stimulus controller as a fallback
- Need to add Resource model & controller for stuff like BrushUp/Get Up & Go/Snack
  - [x] Generate resource/migration
  - [x] Add validations of resource type by lesson type & test
  - [x] Add controller/policy/policy specs
  - [x] Link to courses so all aren't available to everyone
    - Maybe make course_lessons a polymorphic association
    - But I think probably better to just make it a course_resource
    - [x] Add a course_resource join model
    - [x] Add category_resources method to Teacher that fetches through course & join model
      - Turned out I could just delegate to the course

## June 20th

- [x] Remove student names from emails on Event Site
  - [x] SM update email
  - [x] General Inquiry email
  - [x] Setsu Inquiry email
  - [x] Online Sets Inquiry email

## LMS

- [x] Check JS lvl rec also doesn't just pick last that matches
  - It has the same problem the backend one did, will pick a lower level if it's the last it looks at
  - Restructured to use an object holding the lvl and percent for comparisons to make sure the highest possible level is chosen
- [x] Add translations on test result index
- [x] Add view results button for teachers
- [x] Style the list of tests for better separation between tests
- [x] Add level icons to tests
- [x] Remove Tests#show
- [x] When picking parent, it shows Object not org name in dropdown
- [x] Change to 'Specialist Check Required'
- [x] On teacher page, translation button kicks them back to current day
- Need to add Resource model & controller for stuff like BrushUp/Get Up & Go/Snack
  - [x] Prevent deletion if associated with a course
  - Add views
    - [x] For management by staff
    - [x] To show on the teacher page
- [x] Clean up the styling on the shared form errors a bit
- [x] Modify the tests that broke because of IP requirements/translations changing
- [x] Switch fonts to the ones Alex gave me
- [x] Add some missing translations

## June 21st

- Look into languages rendomly toggling on Event site
  - [x] Use around action to set it
  - [x] Fix tests broken by doing that
  - [x] Add for LMS as well
  - [x] And figure out how to make the tests work for that
- [x] More constant interruptions by SMs with the wrong IP

## LMS

- [x] Apply the fonts to the devise layout too lol, you literally had it open
  - Should probably find a way to share the code between those two, maybe sub-layouts?
- [x] Update font weights requested by Alex
- [x] Add remaining missing translations for Teacher section
- [x] Teachers shouldn't be able to see the add parent form
- For Phonics category_resources, you should be able to add them for a week using an existing uploaded resource
  - [x] Create the join model
    - [x] Should change it to being related to the blob directly
      - Just gets the blob ID through the category_resources
      - [x] Don't need map when setting form data in lessons controller, know how to SQL it now (from phonics resources query)
        - Actually do need map cos it's the signed id
  - [x] Add the partial/accepts_nested_attributes_for so you can add them from the Phonics class form

## June 24th

- _Lost 1.5 hours to online lessons_
- [x] Learning how to do level check for online lessons

## LMS

- Add PhonicsResource join model
  - [x] Show on the lesson page for curriculum
  - [x] Add controller & routes to hande deleting
    - [x] And policy/spec
  - Add the fields partial to category_resources form
    - Bad idea, potentially confusing on what should be a simple form
    - [x] Show a list of the classes that use it instead in a table
  - [x] Show them as resources in the teacher view
- [x] Add the JS controller to show the dates for course lessons for Luis
  - [x] Courses also need a list of all their plans and their start dates
  - [x] Show the date for each plan/organisation, updated on connect and when fields changed
  - [x] Add a method to the Course model to generate the plan data
  - [x] Include organisations when querying plans from course by default
  - [x] DRY up the JS controller
- [x] Add the Brush Up category_resources to the teacher view as a card linking to another page
  - [x] Create a TeacherResourcesController
    - Index filters by category based on a param
  - [x] Add index view

## June 25th

- _Lost 30min to missing class meeting_
- Plan out SS replacement DB structure
  - [x] Student search page

## LMS

- [x] Filter Luis' date thing by selected course name
  - [x] Check the accuracy of the dates
- [x] Figure out how to safely whitelist all params when switching languages, so I don't have to manually add them
- [x] Fix dangerous send in teacher_resources index
- [x] Remove SSID, Kanji name from test results table
  - Add a nav for admins to switch between schools/orgs
    - [x] Views & basic controller vars
    - [x] Filtering dependant vars by preceding ones
      - [x] And the children
    - [x] Refactor
- [x] Add translations for school names

## June 26th

- _Lost 3 hours to online lessons_
- [x] Fix students not having their 'first seasonal' status updated from spring, leading to repeater discounts not being applied
  - 12 students affected
  - [x] Add a note to the cron page on the wiki about updating first seasonal at the end of each event
- Questions for new SS
  - [x] Student data import
  - [x] Bulk student deletion
  - [x] Medical Records
  - [x] Medical record upload
  - [x] Messages
  - [x] Email distribution

## LMS

- [x] Resolve issue causing error on teacher page when trying to combine phonics courses with regular courses
- [x] Add levels to category resources, optional for anything but phonics and brush up
  - [x] And group brush up by them
- [x] Seems to be an issue with the brush up link
  - Wasn't actually calling the function to set lesson category
- [x] Added order by en_name to the children on test results index

## June 27th

- Questions for new SS
  - [x] Student announcements
  - [x] Attendance
  - [x] School year
  - [x] School year update
  - [x] Contract management
  - [x] Lesson management
  - [x] Instructor management

## LMS

- [x] Make test results entry use selects, not number fields
- Added order by en_name to the children on test results index
  - But seems to not apply correctly, was getting T > O > Q or O > T > Q depending on length of the T name
  - [x] Think I needed :desc rather than :asc. should be fixed now
- [x] Update file_paths to open in new tabs
- [x] Try out the new method of masking guide images
  - Works by putting the mask after the thing to be masked, as long as I fix the position with `at`

## June 28th

- Questions for new SS
  - [x] School Management
  - [x] System settings (kinda done, need to sit down & talk w/admins)
  - [x] Go thru & clarify questions for Misaki
- Add document submission form the event site
  - [x] Create migration, model
    - needs student name, school, file and file category
    - file categories are schedule_change/school_letter/infectious_disease/other
  - [x] Create factory/unit test
    - [x] Limit filetypes to jpg/jpeg/png/pdf/doc/docx/heic
  - Create controller/routes
    - [x] Add unauthenticated routes for new/create
  - Create views
    - [x] Fake nav
    - [x] New & form
      - [x] Limit filetypes to jpg/jpeg/png/pdf/doc/docx/heic
    - [x] Show page as a splash message that it worked
