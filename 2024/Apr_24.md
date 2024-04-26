## April 1st

- [x] Fix parents not being unable to unregister for activities if it dropped them below their previous invoice amount

### Materials

- Add lesson search
  - [x] Write system spec
  - [x] Add views
  - [x] Add controller
  - [x] Figure out how to integrate the DA short levels (mostly just ele) into the search
    - Either duplicate the Ele key somehow
    - Or when mapping the select options, map the integer as the value rather than the downcased key
  - Remove the need for turbo-target top on status toggles
    - [x] refactor 'after_update_url' to be on lesson

## April 2nd

- [x] Fall back to simplest implementation of blank invoice protection; just disable it till they change something

### Event Site

Request will contain an array of event names they want stats for (determined in sheets by the close dates in sheets for those events) and an API key.

Needs to return these values for each event at each school which is ongoing or closed less than a month ago, as a hash keyed by event name and school id.

#### Seasonal

- Number of internal + reservation
- Number of external
- Internal + res revenue
- External revenue
- Goal

#### Parties

- Total revenue
- Goal

- [x] Write a wiki page for the API
- [x] Write a request spec for the API
  - [x] Include it in the auth before action
- [x] Add a route & controller action
- [x] Add the Model methods to get the necessary data

### Materials

- Add lesson search
  - Remove the need for turbo-target top on status toggles
    - [x] Make the visibility badges actually visibility toggles
    - [x] Style the lesson index table to match others
    - [x] submit a hidden 'index' boolean in the toggles that redirects to the index after updating
- [x] Add start/quit date/birthday dates to student
  - [x] Also search by birthday

## April 3rd

### Materials

#### Lessons

- [x] Only show toggle to release if the lesson is approved (or it's a course)
- [x] Allow writers to update proposals without creating a new one
- [x] Extract lesson attributes to a common partial rather than one per lesson type
- Proposed change rework - Make them just a state of Lesson
  - [x] Delete proposed change table
  - [x] Refactor ProposedChange tests to match proposals being a state of Lesson
  - [x] Write shared factory validity tests of proposals for each lesson type
  - [x] Add new proposal trait to base Lesson factory
  - Add columns to Lesson to duplicate the functionality
    - [x] Add an enum column to Lesson to indicate its proposal status
      - Accepted
      - Changes Needed
      - Proposed
      - Rejected
    - [x] Add an optional belongs_to ChangedLesson and has_many ProposedChanges on Lesson
  - [x] Refactor references to ProposedChange to match them being a state of Lesson
  - Need to be able to compare proposed change and current version side by side
    - [x] Create ProposalsController to handle the changes
    - [x] Create ProposalsController#show
    - [x] Update links where applicable to point at ProposalsController#show rather than LessonType#show
    - [x] Basic styling for ProposalsController#show

## April 4th

### Materials

#### Lessons

- [x] Add status to Lesson search
- [x] Remove proposing changes condition on attach guide to close issue 12
- [x] Add status to visibility toggles
- Proposed change rework - Make them just a state of Lesson
  - [x] Write tests for and create ProposalPolicy
  - Create ProposalsController#update, which
    - [x] Improve system spec expectations
    - [x] Updates proposal with new status/comments if not accepted
    - [x] deletes a Lesson and replaces it with the Proposal if proposal is accepted
      - [x] Add a class method to Lesson which handles the replacement
      - [x] Fix original lesson not being deleted due to destroy: option on associations
    - [x] otherwise does a normal update (only accepting status and internal comments as params)
  - [x] Write a model spec for accepting a proposed change and having it replace the existing one
  - [x] Have proposals table use the proposal form
  - [x] Remove changed_lesson_id field from proposal form as we can just get it from the proposal

## April 5th

### Materials

- Add site themes by
  - [x] Renaming all the `ku-purple` etc to more generic stuff like `color-primary`
  - [x] Add 'tailwind-theme-switcher' tailwind plugin and some demo themes
  - [x] Add dropdown component from [tailwindcss-stimulus-components](https://github.com/excid3/tailwindcss-stimulus-components)
  - [x] Create Stimulus theme switcher for admins
  - [x] Allow the theme to be set for an organisation
    - Add a helper which retrieves the theme based on a user's org id
    - Needs to fall back to the default if org doesn't have a theme
    - Name the theme like `org-n`
- [x] Write a wiki entry for the theme setup

## April 8th

### Materials

- [x] Review Jayson's PR
  - Doesn't work for non-admin users
  - Requested he add a highlight for tests when on test result page
- [x] Add an auto-expanding text area helper with StimulusComponents
  - Integrate it automatically into every text area by making a custom form builder and setting it as default
- Add scrolling to a given skill in the test results input
  - [x] Create stimulus controller
  - [x] Create the nav component
- Add slideover component for main nav on mobile
  - [x] Add stimulus controller
  - [x] Style

## April 9th

- [x] Help Leroy with some kids whose parents registered them for events at online
  - This took a really long time, and ended with two invoices being off by 1000yen combined -\_\_-
- [x] Send invoice change emails to all SMs, like we do for inquiries

### Materials

- [x] Require authorization on ProposalsController
- Add slideover component for main nav on mobile
  - [x] Keep signout link on far right for desktop, put in slideover for mobile
  - Reduce nav links to minimum necessary
    - [x] Admin

## April 10th

- If a kid is an online student, don't show the online event as their default.
  - [x] Render a highlighted message telling them they have to choose another school in place of the calendar/link
    - 参加希望のスクールをお選びください。
  - [x] Keep the image, but without a link or event name
  - [x] Show the expanded 'choose another school' option
  - [x] Add Event#with_sibling_events and an attr_reader to simplify getting & accessing sibling events in controller

### Materials

- [x] Add organisations#show
  - Plan
  - List of schools & school student counts
  - List of OrgAdmins
  - Student count
- [x] Style schools table header
- [x] Add list of classes & teachers to schools#show
- Reduce nav links to minimum necessary
  - [x] Writer
  - [x] Sales
  - [x] OrgAdmin
  - [x] SchoolManager
  - [x] Teacher
  - [x] Parent
- [x] Modify org theme helper to support use with no user/org params

## April 11th

### Materials

#### Auth

- [x] Remove Admins from visible types for Admin
- [x] Attempt 2 at merging Jayson's PR
  - [x] Restore the hover effect
- [x] Move theme selector out of role links, next to the lang toggle
  - [x] And find an icon for it
- [x] Give a link to sign up per-org with hidden field for the org id
  - [x] And a global sign up form with a select box for org
  - [x] Show the org signup link on OrgAdmin & SM homepages, as well as the Org#show page
  - [x] Add clipboard stimulus controller
- Add Alex's icons
  - [x] Teacher profile
  - [x] Lesson pages
  - [x] Course page, for the sections

## April 12th

### Materials

- [x] Address some issues Luis added to the repo, and help him/Jayson clarify tutorials requirements
- [x] Add support requests & messages to seeds
- [x] Fix the purple box around tutorials not reaching the top
- [x] Wrap activities on teacher page for large numbers of activities
- [x] Add extra emails jsonb column to users
  - They can add emails but not delete
    - [x] Write tests
    - [x] Write code
    - [x] Modify views/controllers
      - [x] And add a check for email validity
- [x] Add requester name to support requests
- [x] Style support requests

### Event Site

- [x] Create a page/scaffold for the downtime plan

## April 13th

### Materials

- [x] Respond to GH issues

### Event Site

- [x] Long meeting with leroy to plan out next year
- Update seeds to make testing easier, let other people actually set up a dev environment
  - [x] Test accounts, areas, schools, users & children
  - [x] Price Lists, Events & Time Slots
    - [x] Suppress STDOUT while adding images cos libvips has pointless errors
  - [x] Invoices
- Modify PriceList to use store_accessor for courses
  - [x] No point I think, you can't use numbers as keys

## April 14th

### Materials

#### CSV Upload

- [x] Write JS enabled system spec to lay it all out
  - Deliberately trigger some errors like not uploading a file, poorly formatted CSV
  - Check kids are shown as uploaded on current page once done
  - Check for successful upload by going to the index page
- [x] Scaffold Controller with new, update & create actions
- [x] Scaffold new view

## April 15th

### Materials

- Handle daily attendance in the LMS?

#### CSV Upload

- [x] Write tests for StudentUploadPolicy
  - [x] Create & enforce StudentUploadPolicy
- [x] Use PapaParse to parse CSV into student objects

## April 18th

### Materials

- Handle daily attendance in the LMS?

#### CSV Upload

- [x] Use Typescript for the Stimulus controller
- [x] Create a student table
- [x] Create rows for each student parsed from the CSV
- [x] Set their ID from the array index
- [x] Add an optional param for row creation which sets the status. Default is pending

## April 19th

#### CSV Upload

- Add an optional param for row creation which sets the status. Default is pending
  - [x] Make this an enumerated type with pending, uploading, done
- Should check is row is a valid child
  - [x] If the field is required, outline the row in red and the field in red with missing
  - [x] If it's optional, just have yellow text showing it's missing and a yellow outline on the cell
  - [x] Add icons for each status
- Style the generated table of uploads
  - [x] Header row
  - [x] Body rows
  - [x] Statuses/icons
- [x] Use [@rails/request.js](https://github.com/rails/request.js) to get turbo-stream responses
- Write response templates
  - [x] Create

## April 22nd

- [x] Move some AMs around
- [x] PDF research
- [x] Attempt to resolve rubocop issues

#### CSV Upload

- [x] Displays overall status as sticky heading at top, moves between checking, uploading, done

## April 23rd

### Materials

#### PDFs

- DailyActivity PDF
  - [x] Background
    - Doesn't show up when attached by adding in background option to ::new constructor
    - Unsure if ::generate works as decent amount of refactoring required
    - [x] Spend a lot of time working with Luis to get the background perfectly lined up with the page size

## April 24th

### Materials

#### PDFs

- DailyActivity PDF
  - [x] Subtype
  - [x] Title
  - [x] Goal

## April 25th

### Materials

#### PDFs

- DailyActivity PDF
  - [x] Lang goals by level
  - [x] Materials
  - [x] Intro
  - [x] Instructions
    - [x] Large groups
  - [x] Outro

## April 26th

### Materials

- Handle daily attendance in the LMS?

#### PDFs

- [x] Add 'Warning' column to lessons
- DailyActivity PDF
  - [x] Warning
    - Shown conditionally, hide if there isn't one
  - [x] Image
    - [x] Show the currently uploaded image in the form
  - Intro
    - [x] Interesting fact
  - [x] Elementary/Kindy
  - [x] Add Shingo Pro as the font
