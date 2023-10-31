# November

## November 1st

### Work Project - [Setsumeikai Calendar](https://github.com/Brett-Tanner/setsumeikai_calendar.git)

`cd /Users/brett/Documents/Repos/kids-up/app/public/wp-content/reactpress/apps/setsumeikai_calendar`

- Features

  - [] Display images in school list
  - [] Highlight p elements in SchoolCard when their string matches a query
  - [] Add loading states for SchoolList and Calendar

### Work Project - [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [] Create a new API controller for the GAS sheet's endpoints
  - [] update
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
