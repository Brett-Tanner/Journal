# May 2024

## May 8th

- [x] Sort out new AM areas
- [x] Manually get summary stats for last 2 events

### Materials

- Handle daily attendance in the LMS?

#### CSV Upload

- Displays overall status as sticky heading at top, moves between checking, uploading, done
  - [x] Also track totals for pending, failures, successes
    - Use a separate Stimulus controller on the turbo response whose connect action updates the count appropriately

## May 9th

### Documentation

- Lessons
  - [x] Inheritance
  - [x] Guide generation
  - [x] Form construction

### Lessons

- Tweaks to warning box on DA PDF
  - [x] Round box border
  - [x] Add padding
- [x] Use correct ShingMGo
- [x] Remove unused `includes` from PDF generation
- [x] Update PDF generation tests to be less specific
- [x] Actually use S3 for file storage
- Sort out permissions for the app to upload files
  - [x] Worked with Yamamoto-san to rule out IAM permissions issue
  - [x] Roll back to using local storage so Luis can actually test stuff
- [x] Try setting up swap space again
  - [This one](https://repost.aws/knowledge-center/ec2-memory-swap-file) works fine while the instance is running, unsure if works when restarted though
  - [x] Try seeing if it persists after modifying dockerrun to use a swap file and deploying
    - It does, not 100% sure the container is using it but the swap file is there after a new deploy
- Research possible solutions to Aws::S3::Errors::AccessDenied (Access Denied)

## May 10th

- [x] Attempt to add new version of the dumb tracking thing
  - Script they gave me does nothing
  - Might create a script tag loaded from their servers that does something?
  - But I want an explanation at least before running arbitrary code from someone else's server

### Materials

#### CSV Upload

- [x] Modify system spec setup to pass
- Write response templates
  - [x] Update
  - [x] Make the error forms submit to the correct endpoints for them to function
  - [x] Get a form in a table row to work correctly
    - Had to put it in a cell and reference the form with the `form` attribute on inputs
  - [x] Troubleshoot possible incorrect 'student already taken' error
- [x] Add a dropdown to the nav that lets you select the type of upload
- Teachers
  - [x] Write system spec

## May 13th

- [x] Set up production summary API for Paolo

### Materials

#### CSV Upload

- [x] Troubleshoot flaky upload tests when running multiple together
  - It was because I had `#create_csv` defined for each, so they were overwriting each other in non-deterministic ways
  - Causing the test CSVs to not be created, or the wrong one to be created at the wrong time
  - [x] Refactor the CSV creation code to just be part of `#create_{}_csv`
- [x] Fix tests not running the request JS, so full flow can be tested
  - Was because the test was generating a CSV with a bunch of fields not used by the controller, was messing something up either with the data being sent or in the controller
- [x] Teachers
  - [x] Refactor system spec to not interfere with other upload tests
  - [x] Test & write TeacherPolicySpec
  - [x] Create controller/views
  - [x] Create Stimulus controllers for teacher upload
  - [x] Fix a bug caused by relying on potentially blank fields for tubro dom ids
  - [x] Fix a bug caused by sending the (JS) index of the upload as an attribute of the record being uploaded
- Parents
  - [x] Write system spec
  - [x] Test & write ParentUploadPolicySpec

## May 14th

### Materials

- [x] Bump Ruby version to 3.3.1
- [x] Include `csv` in Gemfile since it's out of stdlib from 3.4.0

#### CSV Upload

- [x] Parents
  - [x] Create controller/views
  - [x] Refactor Stimulus controllers
- [x] Seems there's actually an issue with student uploads, chase that down
  - Might be why it's the only one whose tests don't pass the whole way through
    - Wasn't, that's still a problem
  - Was a typo, using 'hidden_field' rather than 'hidden_field_tag'

### Event Site

- Dockerize
  - [x] upgrade to Ruby 3.3.1
  - [x] Customize Dockerfile to build successfully

## May 15th

### Materials

#### CSV Upload

- [x] Add school creation link to Org page & make title of the table a link to the full school index

### Event Site

- Dockerize
  - [x] Customise docker-compose.yml to run the whole app successfully
    - Up to the S3 SDK causing issues with docker-compose
  - [x] customise .dockerignore
  - [x] take a look at the entrypoint, and config/dockerfile.yml
- Add wiki notes on getting docker-compose working locally
  - [x] .env files and contents
  - [x] DB setup required & how to do it
    - e.g. creating the DB, migrating, adding a user to log in with
- Add wiki notes on transferring domain
- [x] Try getting dockerized app running on KU account
  - IT WORKED FIRST TRY! Just remember to add an S3 bucket name or it'll crash
- [x] Backup the DB in every way possible
  - Copied latest snapshot, figured out how to share, will export to S3 tomorrow morning
- [x] Switch the domain registrar to Cloudflare

## May 16th

- [x] In setsu calendar, auto select the school they're attending the setsu at as the default one they're interested in on form

### Event Site

#### In-office tasks

- [x] Resize swap space because there's not room to pull docker images lol
- IT WORKED FIRST TRY! Just remember to add an S3 bucket name or rails server will crash
- [x] Try creating an S3 bucket specifically for each app
- [x] Share the latest RDS snapshot with the P-UP account
- [x] Spin up a new version with the shared snapshot on the PUP account and get it working
  - [x] Verify accounts still exist and are accessible
- [x] Set up eb CLI for new server
- [x] Reinstate Leroy as online SM
- [x] Figure out the S3 permissions issue, then:
  - [x] Once it's working, point the setsumeikai calendar at the new version temp URL
  - [x] Also change the GAS sheets URLs to point at the new version temp URL
  - [x] May need to reupload all the images that were on S3

## May 17th

- [x] Troubleshoot & fix network error on Setsu calendar when pointed at new server
  - Was just an origin header issue, because the main site is https and the generated URL for the new server was http
  - Just pointed Cloudflare at the new server to give it https and we were all good
- [x] Copy the inquiries that came in to the old server before I pointed Cloudflare at the new server
- [x] Point the domain at the new URL with a CNAME record
- [x] Bump Rails and some XML gem versions to avoid security vulnerabilities (both apps)

### Materials

- [x] 500 error on org page is caused by not having a plan, so when you try to call name on nil it crashes

#### CSV Upload

- [x] Include correcting an invalid record in upload system specs

### Event Site

- IP lock SM accounts
  - [x] Write request specs with mocked IPs
  - [x] Redirect SM to their profile with flash message if not at correct IP
  - [x] Allow their own profile to avoid infinite redirects
  - [x] Allow signing out
  - [x] Write model spec for adding IPs
  - [x] Write model code to pass the tests

## May 20th

### Event Site

- IP lock SM accounts
  - [x] Add fields for Admins to add allowed_ips to SM accounts
  - [x] And refactor the form partial to HAML
  - [x] Add first/family name methods to User
  - [x] Same for kana
    - Added both as helpers instead
    - [x] Refactor other potential uses of the new name helpers
  - [x] Refactor sign up form to HAML
- Invoice calc refactor
  - [x] Extract cost calculation into a concern
    - Returns an object containing all the cost info
  - [x] Extract PDF generation into a concern
  - [x] Extract summary generation into a concern

## May 21st

### Materials

### Event Site

- [x] Allow missing fields in price_list form
- Invoice calc refactor
  - Extract cost calculation into a concern
    - [x] Refactor calc_course_cost
      - [x] Extract into `CourseCalculator` module
      - [x] Extract summary related code to `InvoiceSummarisable`
    - [x] Refactor calc_option_cost
      - [x] Extract into `OptionCalculator` module
      - [x] Extract summary related code to `InvoiceSummarisable`
    - [x] Refactor calc_adjustment_cost
      - [x] Extract into `AdjustmentCalculator` module
      - [x] Extract summary related code to `InvoiceSummarisable`
  - Extract summary generation into a concern
    - [x] Refactor to use cost info object
  - [x] Extract the main loop into `calc_cost` in 'invoice.rb'

## May 22nd

- [x] change setsu calendar text from "内容の確認へ" to "無料体験レッスンを申し込む"

### Materials

### Event Site

- Invoice calc refactor
  - Extract cost calculation into a concern
    - Refactor calc_course_cost
      - [x] Refactor best_price to iterate over courses and handle missing fields
      - [x] Improve related tests to not give false positives with 1-1 courses
  - Extract summary generation into a concern
    - [x] Generally clean up/put things in the right order
    - [x] Fetch `@data[:time_slots]` with options included
    - [x] Get a list of all registered option ids once, prior to filtering the registered slot options with them
    - [x] Add test for not including slot options not registered for in summary
    - [x] Visually inspect and clean up stuff like unjoined arrays

## May 23rd

### Materials

- [x] Bump SolidQueue and MissionControlJobs

### Event Site

- [x] Add GTM scripts to sign_up, sign_in and success pages
  - [x] And set up the customer account with a blank invoice Junya can use to trigger the invoice creation GTM
  - id is 12101
- [x] Check the allowed IPs thing works with the app in a Docker container
- [x] Install SolidQueue and MissionControlJobs
- [x] Stop using opt_regs to get the option IDs, they don't filter ignored opts. Use @data instead

#### In-office tasks

- [x] Delete the test PriceList I accidentally created
- [x] Move Jayson's photobook site
- [x] Install SQ and MissionControl
- [x] Run migrations for User.allowed_ips & SolidQueue
- [x] Push a version with Puma managing SQ
- Close our old AWS accounts
  - [x] terminate all our resources so we're not being billed
  - [x] And Jayson's member account
- [x] Try adding swap space on deploy in a hook

## May 24th

- [x] Hide Online from the school list on setsu calendar, but still enable linking directly to its calendar

### Materials

- Address Github issues
  - [x] Create lesson use matrix
    - [x] Create controller, routes and policy
    - [x] Create the view
  - [x] Show subtypes for relevant lessons on Course#show
  - [x] Show resource list with links on Lesson#show
  - [x] Change lesson details layout to not just be a big column
- Update the new color scheme from Alex's style guide
  - [x] Add new scheme colors
  - [x] Try using CSS vars to set the logo with theme
    - Ended up using a helper method since we need favicon to match
  - Add the new rules to the theme switcher, then find and replace
    - [x] Border radius
    - [x] Lighter versions of main & secondary colors
  - [x] Rename all the new colors to not require the '-color-' prefix

## May 27th

## Materials

- [x] Sweep the site for style guide violations
  - [x] Create classes for table headers
  - [x] Grug-far btn-info to btn-secondary
  - [x] Match new lesson/student dropdowns to style guide
- Address Github issues
  - [x] Language switcher doesn't work on new lesson form; loses the lesson type param
  - [x] Give writers/admins a dropdown to see the homepage of a teacher from each org
  - [x] Find out why images aren't being added to PDF guides
    - potentially the SolidQueue polling rate?
    - was me using :attr in the partial rather than just attr
  - [x] Send Devise emails later with SolidQueue
  - [x] Possible issues changing week on course_lessons
    - 99% sure this is just them moving when updated cos they're not sorted
  - Ensure Lessons have unique title within level and subtype
    - Postponed as not everything has subtype, want to clarify if just level is ok

## May 28th

## Materials

- [x] Add header styles to explainer tables
- [x] Add a button to download a blank sample CSV to use in uploads
  - In the show action
- [x] Autogenerate required fields from Model constant CSV_HEADERS
  - [x] Also use for params
  - [x] And in views
  - [x] And in the JS for table column creation
  - [x] and in tests to generate test headers & data
- [x] Realise password confirmation isn't necessary when uploading, remove from JS validation
  - But keep in form cos it's needed there

### Event Site

- [x] Check if events with no activities can be used as a banner
- [x] Update seeds to give customer children and use string course costs
- [x] Add the placeholder event
  - [x] Fix an issue with goals of 0

## May 29th

## Materials

- [x] Add 'New Plan' button to org pages if no plan present
  - [x] Automatically select the org you followed the link from
- [x] Chase down the intermittent failure to update course_lessons from date_fields partial

### Event Site

- [x] Separate out reservation kids in summary API response

## May 30th

### Event Site

- [x] PUSH UPDATE FOR PAOLO
- [x] Add child partial on customer profile is getting 'content_missing' as a response
  - It's going to '/en/children/new?parent=4', 'ChildrenController#new as HTML'
  - Was using '-' on one and '\_' on another
- [x] Fix malformed magic comments
- [x] Update SM IPs
- [x] Add grouping by folder to event photo selection like for time slots
  - [x] Extract the controller code that splits them by folder to a concern
  - [x] And refactor to HAML
- [x] Add IPs from the sheet for each SM account
- [x] Create new event
  - [x] Make changes to Minamimachida
    - [x] Time Slots & calendar
    - [x] Options
  - [x] Make changes to Shinurayasu
    - [x] Time Slots & calendar
    - [x] Options
  - [x] Check & fix incorrectly named activities
  - [x] Some are outdoor that shouldn't be

## May 31st

## Materials

- [x] Reassign lessons partial needs some padding
- [x] Increase nginx max_body_size to 100MB
- [x] Retain uploaded resources if new ones aren't uploaded
- [x] Add new resources and keep original ones when new resources uploaded
- [x] Add button to delete resources on lesson#show
- [x] Add FilePolicy
  - [x] and tests
- [x] Remove red box around warning text, align with bottom of picture
- [x] Show first 3 letters of days in date fields for course_lessons
- [x] Remove underscores from lesson subtypes in date table
- [x] Move edit button to top of lesson page
- [x] Filter lessons shown on course page to accepted lessons
- [x] Make lesson names in the use matrix link to the lesson page
- [x] Tutorial link formatting is broken for teachers
- [x] Add missing 'Today' button on teacher nav

### Event Site

- [x] Add goals for each school
- [x] Skip courses with no cost associated on event info page
  - [x] And refactor/extract out to HAML partial
  - [x] Refactor the whole 'more_info' section into the HAML partial
- [x] Add edit button to SMs if viewed by admin
  - [x] Modify the user form so the first and last name fields are merged for SMs
- [x] Fix JS calculation with missing 3 course
  - [x] Also an issue caused by showing the currency amount in adjustment change
- [x] Test emails are sent for registrations once we create the new event
  - Checked the Job queue after making a test reservation and it worked
