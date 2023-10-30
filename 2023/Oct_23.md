# October 2023

## October 2nd

### Work Project - [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [x] Discovered and fixed an issue where Price Lists couldn't be updated or properly created from FE
- [x] Refactor the code for uploading assets
  - [x] Allow uploads to arbitrary event names
- [x] Make the VIP kid's names links to their profile
- [x] Add invoice over time stats back in now that they're real

## October 3rd

### Work Project - [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [x] Make event cards smaller on the index, especially on admin index it's ridiculous
- [x] Paginate the event index

## October 5th

### Work Project - [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [x] Make my changes to the invoice index responsive
- [x] Don't show diff school events that have already happened in preference to upcoming events on child profile
- [x] Add next_event convenience method for upcoming events on school/child
- [x] Stop 'なし' being an option, just add it in the view code so it can delete the others
- [x] Split out the radio buttons from add_slot into smaller option partials for readability/DRY
- [x] Install `rack-mini-profiler` for performance monitoring
  - [x] Configure for production (use memory cache rather than default file cache which doesn't expire)
  - [x] Figure out how to read results like [flamegraphs](https://samsaffron.com/archive/2013/03/19/flame-graphs-in-ruby-miniprofiler)
- [x] Separate attendance sheets for special morning/afternoon
  - [x] Required a big ol' rework of the view/controller code for this, it was a mess from all the random exceptions I had to add
  - [x] Also general tidy-up of the view/controller code for readability

## October 6th

### Work Project - [Setsumeikai Calendar](https://github.com/Brett-Tanner/setsumeikai_calendar.git)

- Initialize the project
  - [x] Tailwind
  - [x] React Router
  - [x] Test by uploading to live test page
  - [x] Setup testing with Bun and happy-dom

### Work Project - [Wiki](https://github.com/Brett-Tanner/KU-wiki)

- Add Setsumeikai calendar page
  - [x] How to set up a local dev env

## October 10th

### Work Project - [Wiki](https://github.com/Brett-Tanner/KU-wiki)

- [x] Tidy up hero page and docs organisation
- [x] Add guide for creating new events
- [x] Push it up to live on my domain/Cloudflare pages
- [x] Merge Paolo's contribution

### Work Project - [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [x] Refactor TimeSlot controller
- [x] Let admins create/edit new schools/areas

  - [x] and assign managers to them
  - [x] add the JSON cols for the API and the ability to edit them

- Check everything works for party type events

  - [x] Add an exception to auto-creating afternoon slots for party days as well

## October 11th

### Work Project - [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Check everything works for party type events

  - [x] Activities index shows multiple schools when multiple upcoming events, better to make a tab for each event like stats
    - [x] and add tabs for past events
    - [x] automatically select the next event by default
  - [x] Profile stats count every upcoming event
  - [x] Users can see all events, past and upcoming

## October 12th

### Work Project - [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [x] Missing translation for extra cost in add slot
  - Was still in en mode?
- [x] Add the new school
  - [x] and its event
- [x] Add the .avifs for all time slots because I forgot to add the form field to the event slot partial
- [x] Add the missing form field
- Remove extraneous options from Shin Urayasu and Minami Machida
  - [x] Shin urayasu: no 8:30 arrival
  - [x] Minami machida: no arrival
- [x] Add an exception for the new 3 course

  - [x] in invoice#calc_cost
  - [x] in the JS

- [x] Add create staff button on the area and user indexes

  - nah, don't want it exposed on the FE at all, security risk

- Images

  - [x] Figure out how to create .avif versions of our images through Sharp
  - Find a way to show .avif images to everyone not on Edge, and .jpg to Edge users
    - [x] In CSS
    - [x] Allow attaching .avifs to Time Slots/Events
    - [x] Use them in views

## October 13th

### Work Project - [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [x] Create Yoshi's new account
- [x] Add the goals for each school

### Work Project - [Setsumeikai Calendar](https://github.com/Brett-Tanner/setsumeikai_calendar.git)

- Write basic tests
  - [x] ProgressNav
  - [x] Breadcrumbs
- Scaffold components
  - [x] ProgressNav
  - [x] Breadcrumbs

## October 16th

- [x] Get rid of the red bar on registration site sign up page

### Work Project - [Setsumeikai Calendar](https://github.com/Brett-Tanner/setsumeikai_calendar.git)

- Write basic tests
  - [x] School Card
  - [x] School List
- Scaffold components
  - [x] School Card
  - [x] School List
    - [x] Create test school data

## October 17th

### Work Project - [Setsumeikai Calendar](https://github.com/Brett-Tanner/setsumeikai_calendar.git)

- [x] Basic layout styling for school list/progress nav
- Basic tests
  - [x] School Search
  - [x] School selection
  - [x] Footer
- Scaffold components
  - [x] School Search
  - [x] Footer

## October 18th

### Work Project - [Setsumeikai Calendar](https://github.com/Brett-Tanner/setsumeikai_calendar.git)

- [x] Switch to NavLinks for SchoolCard for better UX

- Set state in/from URL so you can link from external school pages

  - [x] School on calendar route

- FullCalendar and plugins
  - [x] Install
  - [x] Dynamically choose to render calendar or list view based on screen width
  - [x] Read the docs and figure out the bits we need
  - [x] Configure Events on calendar to send user to form when clicked

### Work Project - [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [x] TimeSlot partial for special afternoon says close AM, despite being close PM
- [x] Also the AM special shows a button to close PM, which won't update the PM partial when clicked. Remove it
- [x] Manually add 3 course to the price list shown on Event#show
- [x] Blank coupons are being created with every invoice, thought I fixed that?
- [x] Add a section on the admin page that links to each SM page so I can easily check in on them (or maybe on user index?)

## October 19th

### Work Project - [Setsumeikai Calendar](https://github.com/Brett-Tanner/setsumeikai_calendar.git)

- Set state in/from URL so you can link from external school pages
  - [x] School and setsumeikai on form route?
  - [x] Maintain state using NavLinks
- Basic tests
  - Footer Link components
    - [x] BackLink
    - [x] ForwardLink
  - Form components
    - [x] InputField
    - [x] RadioField
    - [x] SelectField
- Scaffold components
  - [x] Form
  - [x] Various field components
- Error Handling
  - [x] 404s
    - Used a navigate element, actions don't work as they're only on non-get requests
- Features
  - [x] Tidy up FooterNav into Back and ForwardLink components
  - [x] Set blocked cursor on footer links when nothing selected
  - [x] Update id types to be strings, makes more sense on JS side
    - [x] Update tests accordingly
  - [x] Basic Form styling

### Work Project - [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [x] Special afternoon is still saying close AM, make it say close PM
- [x] Separate manager list into SM/AM

## October 23rd

### Personal Project - [Budgeting Site](https://github.com/Brett-Tanner/budgeting-site)

- [x] Set up Vercel PG db

## October 24th

### Work Project - [Setsumeikai Calendar](https://github.com/Brett-Tanner/setsumeikai_calendar.git)

- [x] Test `jaFormat` date helper

- API

  - [x] Finalize API response structure for schools and update types/componenets to match
  - [x] Decide between [jbuilder](https://www.ruby-toolbox.com/projects/jbuilder), [grape](https://www.ruby-toolbox.com/projects/grape) and [active_model_serializers](https://www.ruby-toolbox.com/projects/active_model_serializers) for the API builder
    - went with jbuilder as it's the most commonly used/not a full API generator like Grape, and OJ for JSON parsing cos it's fast
  - [x] Then ditched Jbuilder as it unnecessarily abstracts away stuff I can do on my own

- School API

  - [x] Build the school API
    - [x] Limit to real schools
    - [x] Include available setsumeikais
  - [x] Add the real details to the live Schools, then test the API with them
    - [] Move the API route out of the authenticated namespace so it's publicly accessible
  - [x] Add setsumeikais to the seasonal DB
    - [x] Will need a columns for attendance limit, counter cache for current attendees so we know if full
    - [] Set up the counter_cache on the inquiry side when you create them
  - [x] Create setsumeikai views
    - [x] Form
    - [x] Index
    - [x] Restrict schools they can be created for with a policy

## October 26th

### Work Project - [Setsumeikai Calendar](https://github.com/Brett-Tanner/setsumeikai_calendar.git)

- School API

  - [x] Create the React loader which fetches and handles the school API response

- Inquiry API

  - [x] Add inquiries to the seasonal DB
    - [x] Forms
    - [x] Index
    - [x] Partial
  - [x] Create the inquiry API
  - [x] Create the React action to create inquiries through the API
  - [x] Create the seasonal app views for staff to interact with inquiries
  - [x] Show a summary of the created inquiry after creation

- Features

  - [x] Add hiragana versions of school name/address to avoid blank screen while filtering
    - [] Fill in the hiragana on prod

- Bugs

  - [x] Refreshing the form keeps the school but loses the setsumeikai
    - Rails was sending a number for the id rather than a string
  - [x] NavLink for Calendar not showing active from SchoolCard click
    - Noticed it worked if the setsuId param was 'undefined' but not 0 for some reason, so changed the SchoolCard url to use undefined

### Work Project - [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [x] Add rack-cors so the API accepts requests from the React app
- [x] Add hiragana to schools so searching doesn't go blank
- [x] Add the referrer column I forgot on Inquiry
- [x] Provide a json response to API Inquiry#create calls
- [x] Display the inquiry list on setsumeikai show page
- [x] Set counter_cache on Setsumeikais for inquiries
  - [] And update it for existing ones after pushing the change

### Personal Project - [Budgeting Site](https://github.com/Brett-Tanner/budgeting-site)

- [x] Create the schema with drizzle
  - [x] Plan out the schema
    - Users
    - Categories
    - Transactions
    - Budgets
  - [x] Migrate

## October 27th

### Work Project - [Setsumeikai Calendar](https://github.com/Brett-Tanner/setsumeikai_calendar.git)

Went on an archaeology expedition with Leroy.

- Features

  - [x] Add hiragana versions of school name/address to avoid blank screen while filtering
    - [x] Fill in the hiragana on prod
    - [x] Add the images

### Work Project - [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [x] Set counter_cache on Setsumeikais for inquiries
  - [x] And update it for existing ones after pushing the change
- [x] Use table to display setsumeikais
- [x] Edit them in a row at the top
- [x] Setup links between various setsumeikai/inquiry pages, misc. polish
- [x] Add images to schools, and a way to upload/attach them
- [x] Add photo service stats to options
  - [x] Fix event options not being found
    - Was pushing an array of them, not concatenating it
- [x] Add total children who attended each event
- [x] Fix price calculation where exactly 4 activities are registered for
  - Wasn't taking advantage of the 3 course plus one

## October 30th

### Work Project - [Wiki](https://github.com/Brett-Tanner/KU-wiki)

- Document GAS
  - [x] The spreadsheet
  - [x] `Main.gs`
  - [] `kidsCustomerGAS`
    - [x] `getCustomer`
    - [x] `getSchool`
    - [x] `createRecordMain`

### Work Project - [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [x] VIP kids are only shown if attending the current event, but their invoices for all events are summed

## October 31st

### Work Project - [Wiki](https://github.com/Brett-Tanner/KU-wiki)

- Document GAS
  - [] `kidsCustomerGAS`
    - [] `createSetsumeikaiMeibo`
    - [] `moveLast`

### Work Project - [Setsumeikai Calendar](https://github.com/Brett-Tanner/setsumeikai_calendar.git)

`cd /Users/brett/Documents/Repos/kids-up/app/public/wp-content/reactpress/apps/setsumeikai_calendar`

- Features

  - [] Display images in school list
  - [] Display some kind of indicator that a school has setsumeikais scheduled
    - If that's ever in question, seems they always should
  - [] Highlight p elements in SchoolCard when their string matches a query
  - [] Add loading states for SchoolList and Calendar

### Work Project - [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [] Add setsumeikai stats

  - Monthly and yearly setsumeikais scheduled
  - Monthly and weekly inquiries
  - Average setsumeikais per month

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
