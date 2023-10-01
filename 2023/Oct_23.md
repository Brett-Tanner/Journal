# October 2023

## October 3rd

### Work Project - [Setsumeikai Calendar](https://github.com/Brett-Tanner/setsumeikai_calendar.git)

- Initialize the project and verify ReactPress/Vite/Tailwind etc. all work together
- Add to the wiki page as I'm going, at minimum I'll need to do it again on my home computer
- Store the fetched school data in a Set?

### Work Project - [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Images
  - [] Use picture tags (or at least some way of loading smaller images on mobile)
  - [] Create a workflow for generating responsive versions
    - Probably just me doing it manually with Sharp, Leroy can't export as .avif
- [] Add invoice over time stats back in now that they're real
- [] Check everything works for Halloween Party type events
- [] Separate attendance sheets for morning/afternoon (all special days)
  - [] Also look into adding a tab that shows just the afternoon/morning attendance for all attendance sheets, not just special
- [] Stop 'なし' being an option, just add it in the view code so it can delete the others

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
