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

## November 4th

### Work Project - [Setsumeikai Calendar](https://github.com/Brett-Tanner/setsumeikai_calendar.git)

`cd /Users/brett/Documents/Repos/kids-up/app/public/wp-content/reactpress/apps/setsumeikai_calendar`

- [] Make comparison documents
- [] Write the instructions for testing

- Inquiry Form

  - [x] Map school_id in summary to school names
  - [x] Re-attach the form's showSummary event listener when back button is clicked
  - [] Rather than school_id, the select box should be `planned_school`

- Setsumeikai Form

  - [x] Change `planned_school` to `school_id`
    - because it's the school they should be shown for, better way to do the association
  - [] Figure out how to trigger GTM when the form submits
    - remember you have access to the dashboard
    - and there's something which tracks form submissions
  - [] Remove the fade-in effect
    - it's a class in the theme, but which one?
    - whole page may fade in separate to any sections
  - [] Add loading states for SchoolList (use `Suspense`)

### Work Project - [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Inquiries

  - [x] Add referrer to Inquiry form
  - [x] Remove `planned_school` column
    - That info is now found in `school_id` foreign key/school association
  - [] Setsumeikais need to be assignable to multiple schools, and show on all those school's calendars
    - [x] Through a `SetsumeikaiInvolvements` join table
    - [x] Setsumeikais need to accept nested attributes for `Setsumeikai Involvement`
    - `school_id` on Setsumeikai will now refer only to the school it's physically held at
    - the school it's held at will also be linked through `SetsumeikaiInvolvements`
    - [] Inquiries go on the sheet for the school they want to attend (was `planned_school`, now just the associated school)
    - [] the school that inquiry's setsumeikai is at goes in one of the columns
  - [x] The table needs a `release_date`, when it becomes available to be seen on the calendar
    - [x] don't send setsumeikais where the release date hasn't passed, same as full ones
  - [] Check ALL inquiries are sent from the API, not just the setsumeikai ones
  - [] On inquiry creation, send an email to the school, parent and HQ
    - [] For setsumeikai inquiries, the school is the school they want to attend
  - [] Tidy up the Inquiry/Setsu UI keeping in mind the fact that there are actually gonna be multiple categories

- General

  - [] In recent invoices, kids who registered then unregistered down to 0 are shown
    - see if we can auto-delete that
    - if not, check the leftover adjustments aren't included in any stats
  - [] Add setsumeikai stats
    - Monthly and yearly setsumeikais scheduled
    - Monthly and weekly inquiries
    - Average setsumeikais per month
  - [] Leroy's survey thing
  - [] Show all upcoming events in order on parent/child pages so we can handle parties better

- Future Plans

  - [] Move control of the domain from that Japanese site to Cloudflare
  - [] Add a 'download PDF invoice' button
    - Just for staff or for everyone?
  - [] Add button to generate photo service armband PDF for parties

    - Printable template with kids' names and a color which shows their photo status

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

### Work Project - [Wiki](https://github.com/Brett-Tanner/KU-wiki)

- Add Setsumeikai calendar page
  - [] Overview of the flow/types
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

- Import transactions to the database
  - [] Create UI scaffold
  - [] Auto-categorize based on rules
    - [] Add rules table
  - [] If transactions are uploaded for last day already in the DB and they have the same amount, ask if duplicates
    - [] If uploaded for any time prior to the last day in the database, just ignore them
