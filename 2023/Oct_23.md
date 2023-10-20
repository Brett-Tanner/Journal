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

`cd /Users/brett/Documents/Repos/kids-up/app/public/wp-content/reactpress/apps/setsumeikai_calendar`

- Set state in/from URL so you can link from external school pages
  - [] School and setsumeikai on form route?
  - [] Write tests for state getting set from params for Calendar and Form
- Basic tests
  - [] Form
- Scaffold components
  - [x] Form
  - [x] Various field components
- Features
  - [x] Tidy up FooterNav into Back and ForwardLink components
  - [x] Set blocked cursor on footer links when nothing selected
  - [] Highlight p elements in SchoolCard when their string matches a query
  - [] Redirect in Router Actions based on selections state i.e. if no school navigate to school
  - [] Add hiragana versions of school name/address to avoid blank screen while filtering?
  - [] Add loading states for SchoolList and Calendar
- API
  - [] Filter the events you send by future and not full
- Error Handling
  - [x] 404s
    - Used a navigate element, actions don't work as they're only on non-get requests

### Work Project - [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Future Plans

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
