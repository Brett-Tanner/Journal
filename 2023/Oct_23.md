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

### Work Project - [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [] Go over SM requests with Leroy when he gets back
- [] Let admins create/edit new schools/areas and assign managers to them

- Check everything works for party type events

  - [] Add an exception to auto-creating afternoon slots for party days as well
  - [] Currently next event seems to show the furthest, not the closest (at least on activities index)
  - [] Activities index shows multiple schools when multiple upcoming events, better to make a tab for each event like stats

- Images

  - [] Use picture tags (or at least some way of loading smaller images on mobile)
  - [] Create a workflow for generating responsive versions
    - Probably just me doing it manually with Sharp, Leroy can't export as .avif

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
    - [] Bump Rails versions
    - [] Bump gem versions that've received a major upgrade (not the mail one though, make sure that's locked)

### Work Project - [Setsumeikai Calendar](https://github.com/Brett-Tanner/setsumeikai_calendar.git)

- Initialize the project and verify ReactPress/Vite/Tailwind etc. all work together
- Add to the wiki page as I'm going, at minimum I'll need to do it again on my home computer
- Store the fetched school data in a Set?

### Work Project - [Seasonal Wiki](https://github.com/Brett-Tanner/KU-wiki)

- [] Add 'How to contribute'
  - [] Adding a page
  - [] Adding a section
- [] AWS section
  - [] Pushing a new version
  - [] Services we use and overview of what for
- [] Rails section
  - [] Overview
  - [] Useful Commands
