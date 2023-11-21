# November

## November 1st

### Work Project - [Setsumeikai Calendar](https://github.com/Brett-Tanner/setsumeikai_calendar.git)

`cd /Users/brett/Documents/Repos/kids-up/app/public/wp-content/reactpress/apps/setsumeikai_calendar`

- Inquiry Form

  - [x] Find the path: `public/wp-content/themes/kidsup/page-inquiry.php`
  - [] Add a plain HTML form pointing at my site's create_inquiry endpoint
    - [x] Figure out how to edit the template (through the Theme File Editor under appearance in WP)
    - [x] Duplicate the styles from the iframe in a style tag in the template
    - [x] change the `attend` input to separate `kindy` and `ele_school` inputs to match my DB

### Work Project - [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [x] Create a new API controller for the GAS sheet's endpoints
  - [x] update
    - [x] figure out how to parse the string GAS sends as readable JSON
- [x] Rework inquiries relations into school and setsumeikai
  - [x] Rename the area relations for inquiries from `school_inquiries` to `setsumeikai_inquiries`
- [] Create '池袋' (Ikebukero) school
  - [x] and adjust the event partial to not error stuff when there are no events at the school

## November 2nd

### Work Project - [Setsumeikai Calendar](https://github.com/Brett-Tanner/setsumeikai_calendar.git)

- Inquiry Form

  - [x] Add a plain HTML form pointing at my site's create_inquiry endpoint
    - [x] show a summary of the inquiry before sending
    - [x] preserve form state when using the back button
    - [x] on final submission, intercept the form data, wrap it in inquiry, and send it to the seasonal DB
    - [x] Then redirect to the current place it's meant to go
    - [x] Style everything involved in that

- Features

  - [x] Apply animations when searching schools
  - [x] Send school_id as well since it's a field on Inquiry now

### Work Project - [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [x] Remove null constraint on Inquiry.setsumeikai_id
- [x] Add User.all_inquiries to get all inquiries of any type for managers
- [x] Create '池袋' (Ikebukero) school

## November 6th

### Work Project - [Setsumeikai Calendar](https://github.com/Brett-Tanner/setsumeikai_calendar.git)

- Inquiry Form

  - [x] Map school_id in summary to school names
  - [x] Re-attach the form's showSummary event listener when back button is clicked

- Setsumeikai Form

  - [x] Change `planned_school` to `school_id`
    - because it's the school they should be shown for, better way to do the association

### Work Project - [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Inquiries

  - [x] Add referrer to Inquiry form
  - [x] Remove `planned_school` column
    - That info is now found in `school_id` foreign key/school association
  - [x] Setsumeikais need to be assignable to multiple schools
    - [x] Through a `SetsumeikaiInvolvements` join table
    - [x] Setsumeikais need to accept nested attributes for `Setsumeikai Involvement`
    - [x] show on all involved school's calendars/setsumeikai indexes
    - `school_id` on Setsumeikai will now refer only to the school it's physically held at
    - the school it's held at will also be linked through `SetsumeikaiInvolvements`
    - [x] Inquiries go on the sheet for the school they want to attend (was `planned_school`, now just the associated school)
    - [x] the school that inquiry's setsumeikai is at goes in one of the columns
  - [x] The table needs a `release_date`, when it becomes available to be seen on the calendar
    - [x] don't send setsumeikais where the release date hasn't passed, same as full ones
  - [x] Check ALL inquiries are sent from the API, not just the setsumeikai ones

- General

  - [x] Add address to user profile (behind PIN)

## November 7th

### Work Project - [Setsumeikai Calendar](https://github.com/Brett-Tanner/setsumeikai_calendar.git)

- Setsumeikai Form

  - [x] Style SchoolCard
  - [x] Clean up other assorted styling
  - Translations
    - [x] Stuff I have
    - [] Stuff I need to ask Miki about
  - [x] Override site styles
  - [x] Remove the fade-in effect
    - didn't end up managing it
    - hidden away somewhere, not worth the effort/time when other stuff to work on

### Work Project - [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Inquiries

  - [x] Change setsumeikai form to add involved schools on a separate row
  - [x] On inquiry creation, send an email to the school, parent and HQ
    - [x] for setsumeikai inquiries
    - [x] for general inquiries
  - [x] Planned school doesn't show in summary anymore
    - was still using planned school, not school_id
  - Translations
    - [x] Stuff I have
    - [] Stuff I need to ask Miki about

- General

  - [x] Send emails on create as well as update
    - previously creates meant nothing, but now they're important
  - [x] Add `#manager` convenience method to `School`
    - `school.managers.first` is awful, but I wanna keep the possibility of multiple SMs open
  - [x] Allow creation of inquiries without a setsumeikai (general/ 'I')
  - Create translation sheets for Miki
    - [x] Inquiries
    - [x] Stats

### Personal Project - [Budgeting Site](https://github.com/Brett-Tanner/budgeting-site)

- [x] Try `auth-astro`
  - rejected it because there was some un-google-able import error
- [x] Add Supabase auth

## November 8th

### Work Project - [Setsumeikai Calendar](https://github.com/Brett-Tanner/setsumeikai_calendar.git)

- [x] Copy school sheets from my fake one so SMs can use
- [x] Write the instructions for testing
- Make comparison documents

  - [x] Add old pics

### Work Project - [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [x] Fix naming collision between slot_regs and slot_regs_count

  - It actually counter cached all registrations, not just on slots
  - Renamed to registrations_count
  - Stops it counting all registrations for num_regs in calc_cost

- [x] Remove all old empty invoices

## November 9th

### Work Project - [Setsumeikai Calendar](https://github.com/Brett-Tanner/setsumeikai_calendar.git)

- Make comparison/testing documents

  - [x] Add new pics
  - [x] update testing pics
  - [x] add survey at the end
  - [x] add Japanese translation

- Setsumeikai Form

  - Translations
    - [x] Stuff I need to ask Miki about
  - [x] Override site styles on the form/summary for borders
  - [x] Final styling pass on the whole app
  - [x] Scroll to top on page nav
  - [x] Keep bottom navbar above site nav on mobile
    - Only worked when logged in as WP Admin????
    - So rolled it back
  - [x] Add required badges

### Work Project - [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Inquiries

  - Translations
    - Stuff I need to ask Miki about
      - [x] Stats
      - [x] Inquiries & Setsumeikais
    - [x] Comment out the setsumeikai links before pushing to live, not ready yet

### Personal Project - [Budgeting Site](https://github.com/Brett-Tanner/budgeting-site)

- [x] Set up basic CSV parsing
  - Just an API route which logs the result for now

## November 10th

### [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- General

  - [] Leroy's survey thing
    - [x] Create Survey model/controller
    - [x] Create Survey access policies
    - [x] Create the views to create a survey
    - [x] Create the views to display and manage surveys
    - Write the logic to decide which kids are shown the surveys
      - [x] Based on criteria
      - [] And whether they or a sibling has already filled it out
    - [x] Create SurveyResponse model/controller
    - [x] Create SurveyResponse access policies
    - [x] Create associations to other relevant models/fill in associated controller actions/views
    - [x] Create the basic form for submitting survey responses on invoice confirmation screen
      - [x] Implement generic field partial
      - [x] Implement check field partial
      - [x] Implement radio field partial
      - [x] Implement select field partial
    - [x] Create views for displaying and managing responses
    - [x] Sort response table to ensure values line up with headers

### [KU-Wiki](https://github.com/Brett-Tanner/KU-wiki)

- [x] Switch all the testing guide/comparison images to .avif

## November 12th

### Personal Project - [Budgeting Site](https://github.com/Brett-Tanner/budgeting-site)

- [x] Go through the insane ordeal of parsing Japanese CSVs to something displayable by JS
- [x] Create UploadApp React component, parent of
  - [x] Upload form, to send the CSV to the parse endpoint
  - [] Edit form, to edit the parsed CSV data for saving as transactions

## November 13th

### [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [x] Fix reservation kids not being members for the new 3 course
- [x] Use direnv and binstubs to make rspec faster to run
- [x] remove unused test files
- [x] update testing gems

- General

  - [x] Leroy's survey thing
    - Write the logic to decide which kids are shown the surveys
      - Write tests
        - create updated factories for
          - [x] School
          - [x] Child
          - [x] Survey
        - [x] figure out how to write test helpers & require them in the test
      - [x] false if all criteria blank
      - [x] false if they have already filled it out
      - [x] false if a sibling has already filled it out
      - [x] true when random enum values match
      - [x] true when random string values match
      - [x] true when SSID values match
      - [x] true when random boolean values match
      - [x] true when date values match
    - [x] Fix checkbox component

## November 14th

### [Setsumeikai Calendar](https://github.com/Brett-Tanner/setsumeikai_calendar.git)

- Setsumeikai Form

  - [x] Still send full setsumeikais to the app
    - [x] Add a boolean to the response JSON indicating if full or not
    - [x] Display full setsumeikais differently and disable clicking them (maybe the title & classes based on boolean)
    - [x] Delete all setsumeikais before pushing new version, they didn't have a default for inquiries_count
  - [x] Allow attendance_limit to be 0

### [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Inquiries

  - [x] Add nakagawa's translation suggestions
  - [x] Add school selection for AMs
  - [x] Send `involved_setsumeikais` to the calendar, with upcoming and visible scopes applied
  - [x] Auto-select current school in setsumeikai form for admin/AM
  - [x] Refactor Setsumeikais#index controller logic
  - Modify forms to do everything I can to make sure schools are involved in their own setsumeikai
    - [x] autofill the current school on the form
    - [x] add model-level validation that involved schools includes host school
  - [x] Add 'copy' button to existing setsumeikais
  - [x] Refactor Inquiries#index controller logic
  - [x] Move the table filter headers into a partial
    - [x] Do the same for every other instance of filter headers in the site (except event sheet)
  - [x] Modify inquiry index to more closely match the sheet
  - [x] Allow deleting setsumeikais
    - [x] But throw an error if there are associated inquiries

### Personal Project - [Budgeting Site](https://github.com/Brett-Tanner/budgeting-site)

- [x] Add inputs to the parsed transactions

## November 15th

### [Setsumeikai Calendar](https://github.com/Brett-Tanner/setsumeikai_calendar.git)

- [x] Figure out how to trigger GTM when the form submits
  - [x] Figure out there's a way to send custom events to the data layer with `useEffect`
  - [x] Add the code to do so (the custom event is `setsu_success`)
  - [x] Configure GTM to listen for it
    - [x] Test the workspace

### [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Inquiries

- [x] use `involved_setsumeikais` everywhere `all_setsumeikais` was
- [x] Scope the setsumeikai index with a combo of the policy scope and @school.id

- General

  - [x] Only hide the unconfirm button if there are unconfirmed invoices for **the same event**
  - [x] Correctly associate checkbox labels to their checkboxes on survey response forms
  - [x] Add translation for thank you message
  - [x] Format the list of options in a more readable way
  - [x] Stretch the main (colored) heading across the width of the card
  - Fix layout of checkbox results in survey response tables
    - [x] make sure you're only showing responses for that survey, on live it's showing all for that Q for all surveys
    - [x] fit all checkbox responses in one column
  - [x] Add custom error pages
  - [x] Optimise DB requests for Surveys
  - [x] In recent invoices, kids who registered then unregistered down to 0 are shown
    - was a missing `real` scope
  - [x] Add columns to survey_response table
    - en_name
    - grade
    - email
    - phone
  - [x] Add a notes field, text area which SMs can submit to add notes on the survey
  - [x] Give AMs and SMs access to surveys and tweak the permissions/stuff that's displayed
  - [x] Stop error controller responding to spam requests and throwing errors
    - just removed it again lol

## November 16th

### [Setsumeikai Calendar](https://github.com/Brett-Tanner/setsumeikai_calendar.git)

- Styling
  - Nav
    - [x] School breadcrumb
    - [x] Calendar breadcrumb
    - [x] Form breadcrumb
    - [x] Fix Breadcrumb borders being overridden by WP styles
    - [x] FooterNav
  - Main
    - [x] background
  - School List
    - [x] Cards
    - [x] Search box

### [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [x] Show nav with schools to choose which responses are shown
- [x] Filter responses by AM schools

## November 17th

### [Setsumeikai Calendar](https://github.com/Brett-Tanner/setsumeikai_calendar.git)

- Styling
  - Nav
    - [x] Form breadcrumb isn't squared when just a heading
    - [x] Round the corners of breadcrumbs
- Calendar
  - [x] Header
  - [x] Body
    - [x] Table spacing & borders
    - [x] Cell contents
- Form
  - [x] SelectionFields
  - [x] Inputs

## November 20th

### [Setsumeikai Calendar](https://github.com/Brett-Tanner/setsumeikai_calendar.git)

- Calendar
- Form
  - [x] Add outline styles on input focus
  - [x] Style placeholder text in date fields
  - [x] Irregular fields
  - [x] Change search input to ku-faded, white background
  - [x] Options text is styled orange, probably inherits. Set it to black.
- [x] Scroll to the correct point on navigation
- [x] Search box borders (active and not) overridden by WP styles

### [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [x] Add a statistician role, and the appropriate policies/views
- [x] Make a list of things AMs requested and my responses
- [x] Live diagnosed an issue one of Yoshi's customers was having

## November 21st

### [Setsumeikai Calendar](https://github.com/Brett-Tanner/setsumeikai_calendar.git)

- [x] Summary
    - [x] Move hidden fields into the actual form -__-
    - [x] Add and style selectionsBox
    - [x] Style Summary body
    - [x] Add 4pm callout
- [x] Mobile pass
    - [x] Calendar
    - [x] Make the breadcrumbs not skewed
    - [x] use jaFormat in SelectionFields
- [x] Error page

Inquiry form

- Style to match setsu form
  - [x] Form
  - [x] Summary

## November 21st

### [Setsumeikai Calendar](https://github.com/Brett-Tanner/setsumeikai_calendar.git)

### [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [] Registering for both AM and PM means the kid shows up twice on the attendance sheet, I probably missed a uniq or distinct somewhere
- [] Fix what seems to be a lot of N+1 requests getting schools from setsu endpoint
- [] Since we can apparently have children without a school id, need a better way of handling that

  - e.g. currently causes the parent's profile to error on login

- General

  - [] Add setsumeikai stats
    - Monthly and yearly setsumeikais scheduled
    - Monthly and weekly inquiries
    - Average setsumeikais per month
    - Breakdown of referrers
  - [] Show all upcoming events in order on parent/child pages so we can handle parties better
  - [] Write the refactoring guide and do some small examples so others can work on it

- Future Plans

  - [] In August 2022, RDS certificate [expires](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/UsingWithRDS.SSL-certificate-rotation.html#UsingWithRDS.SSL-certificate-rotation-updating). Will need to rotate to avoid connectivity issues.
  - [] Move control of the domain from that Japanese site to Cloudflare
  - [] Add a 'download PDF invoice' button
    - Just for staff or for everyone?
  - [] Add button to generate photo service armband PDF for parties

    - Printable template with kids' names and a color which shows their photo status

  - [] Look into HAML for templating rather than ERB, as well as the other options like phlex or components
  - See if the occasional memory problems are actually something more like [this](https://www.engineyard.com/blog/thats-not-a-memory-leak-its-bloat/)
    - [] Also loading all the TimeSlots and Options from the start when calculating Invoice costs
    - [] Also maybe Rack::Bug, or a newer version of something similar since it was last updated in 2015
  - Simplify/modularize invoice code
    - [] Split out PDF functionality
    - [] Preload all the stuff I need for calc_cost at the start and pass it explicitly
    - [] Create columns for each type of cost?
  - Platform Upgrades
    - TEST ALL ON STAGING FIRST
    - [] Bump AWS platform version
    - [] Try bumping Ruby version to latest stable (can maybe install manually with a pre-deploy hook)
    - [] Bump Rails version
    - [] Bump gem versions that've received a major upgrade (not the mail one though, make sure that's locked)

### [KU-Wiki](https://github.com/Brett-Tanner/KU-wiki)

- [] Create refactoring guide
- [] Add 'How to contribute'
  - [] Adding a page
  - [] Adding a section
- [] AWS section
  - [] Pushing a new version
  - [] Services we use and overview of what for
- [] Rails section
  - [] Overview
  - [] Useful Commands

### Personal Project - [Budgeting Site](https://github.com/Brett-Tanner/budgeting-site)

- Features

- [] wire the upload form up to submit to
- [] an endpoint to create DB records
- [] Auto-categorize based on rules
  - [] Add rules table
- [] If transactions are uploaded for last day already in the DB and they have the same amount, ask if duplicates
  - [] If uploaded for any time prior to the last day in the database, just ignore them
