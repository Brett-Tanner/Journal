## September 1st

### Work Project - [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Features

  - Event creation

    - Add a way of uploading images to the S3 bucket from the site
      - [x] Upload to a specific folder based on purpose of image
        - [x] and on the event it's for
      - [x] Restrict the types of file that can be uploaded to image types
      - [x] Make sure large files work on live, they didn't the first time
        - Upload doesn't even seem to start, only thing in the logs is a get request to the same page
        - Figured it out, the POST is sent but the file is too big (was in nginx error logs)
        - Seems I need to set `client_max_body_size` in nginx.conf (locations to set it are http, server, location, you want to set it in server or it'll be overridden)
        - Can be done by following [this AWS help article](https://repost.aws/knowledge-center/elastic-beanstalk-nginx-configuration)
    - [] Time Slot step
      - [x] Allow slots to be edited individually from the slot index
        - [x] Allow editing an afternoon slot manually
          - [] Allow applying to all with same name, morning boolean and event_id
        - [x] Allow options to be edited
        - [x] Allow options to be added
        - [] Allow updating time slots with the same name, morning boolean and event_id
      - [] pre-select the existing image in the form
    - [x] Remove ability to destroy events from frontend

## September 2nd

### Odin Project - [Weather App](https://github.com/Brett-Tanner/weather)

- [] Display the info (all in a main element)
  - [x] Switch to Vite as a build tool
  - [x] Create containers for the layout elements and do a pulse effect while loading (if no data passed), replace with content once received
  - [x] Location info header at top of main
  - [] Current weather card, followed by three days of forecast cards
  - [] Change the border color/shadow (and background color) of the cards according to weather

## September 3rd

### Odin Project - [Weather App](https://github.com/Brett-Tanner/weather)

- [x] Display the info (all in a main element)
  - [x] Current weather card, followed by three days of forecast cards
  - [x] Change the border color/shadow (and background color) of the cards according to weather

### Odin Project - [JS Testing Practise](https://github.com/Brett-Tanner/js-testing-practise)

- [x] Decide on Vitest rather than Jest
  - works with ES6 modules
  - simple integration with Vite, which I plan to use where possible
- [x] Set up the repo with Vite/Vitest
  - Click `Vitest` in the bottom bar to start it in watch mode, show errors inline
- [] Write tests, then code for
  - [x] `capitalize`
  - [x] `reverseString`
  - [] `calculator`
  - [] `caesarCipher`
  - [] `analyzeArray`

## September 4th

### Odin Project - [JS Testing Practise](https://github.com/Brett-Tanner/js-testing-practise)

- [x] Write tests, then code for
  - [x] `calculator`
  - [x] `caesarCipher`
  - [x] `analyzeArray`

### Odin Project - [Battleship](https://github.com/Brett-Tanner/battleship)

- [x] Scaffold the types so I have an idea of the overall shape
- [x] Ships
  - [x] Write tests
  - [x] Write passing code
- [] Gameboard
  - [x] Write tests
  - [] Write passing code
- [] Player
  - [] Write tests
  - [] Write passing code

## September 5th

### Work Project - [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Event creation

  - Event step
    - [x] Refactor existing controller code
      - [x] To give more helpful error/success messages, in English
      - [x] To redirect to event index on update, slots should be updated from their form
    - [x] Allow updating all events with same name
  - Time Slot step
    - [x] When creating a new event, slots should be created for that event at all schools
    - [x] Group images by the folder they're in
    - [x] Allow creating all special afternoons from one special morning
    - [x] Allow creation of new time slots for an event from the index for that event
  - [x] Pre-select existing images in the form
  - [] Test out what needs changing when a second event is added
    - Seed some dummy registrations
  - [] Add instructions for each step

## September 6th

### Odin Project - [Battleship](https://github.com/Brett-Tanner/battleship)

- [x] Gameboard
  - [x] Test placeShip()
  - [x] Realise fill() fills the array with references to the passed object (it was literally in the MDN page I read)
  - [x] Clean up the atrocious code I wrote last night
  - [x] Realise the first index of rows is the y-axis, second index is the x-axis
  - [x] Test receiveAttack()
- [x] Spaces
- [x] Player
- [] DOM
  - [x] Initially just inputs for name, human or computer
  - [] Then switches to active player unobscured board, opponent obscured
  - [] Prompts for move (click, see possibilities, then click again)
  - [] Create displayMessage(), called when
    - Ship sinks
    - Attack hits or misses
    - Player wins

## September 7th

### Odin Project - [Battleship](https://github.com/Brett-Tanner/battleship)

- [] DOM
  - [] Active player unobscured board, opponent obscured
  - [] Prompts for move (click, see possibilities, then click again)
  - [] Create displayMessage(), called when
    - Ship sinks
    - Attack hits or misses
    - Player wins

### Work Project - [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Stats page

  - Adjustments
    - [] Number of each adjustment applied
    - [] Total effect on revenue from each (some will be negative)
      - [] Group any with a magnitude less than a certain amount into a misc data point
  - Edits
    - [] Total edits by staff/customers (subtract the total number of creates from updates)
  - Revenue
    - [] Pie chart of revenue by student category
    - [] Pie chart of revenue by time slot/option/adjustment (subtract others from total for time slot revenue)
  - [] Add filtering by school, student category, option/slot category etc.

- Code cleanup

  - [] Find all the stuff with hardcoded event ids/links between school id/event id/user id and refactor it

- DB

  - [] Remove email template column (invoices)
  - [] Remove description column (everything)
  - [] Change 'needs_hat' to 'first_seasonal' to match its meaning (child)
    - [] Update all kids who attended to have 'first_seasonal' = false
  - [] Remove old versions once I'm done making invoice table changes (invoices, children)
  - [] See if it's vacuuming/analyzing by default, if not make it do that
  - [] Add counter_cache where appropriate (TimeSlot children for sure)

- Invoices

  - [] Stop persisting blank invoices when registration page viewed
  - [] Simplify/modularize invoice code

- Per-activity costs

  - [] Add internal/external modifier cols to Time Slot
  - [] Add a snack boolean col to Time Slot
  - [] Add code to use them in
    - [] Invoice#calc_cost

- Platform Upgrades

  - TEST ALL ON STAGING FIRST
  - [] Bump AWS platform version
  - [] Try bumping Ruby version to latest stable (can maybe install manually with a pre-deploy hook)
  - [] Bump Rails versions
  - [] Bump gem versions that've received a major upgrade (not the mail one though, make sure that's locked)

- UX

  - Forms

    - [] Add useful error messages to all forms (from backend)
    - [] Add JS validation as well (constraint validation API, see the [Odin Project Lesson](https://www.theodinproject.com/lessons/javascript-form-validation-with-javascript))

  - Images

    - [] Use picture tags
    - [] Create a workflow for generating responsive versions

- Views

  - [] Split the User#show pages out into different pages for different roles
  - [] Look at moving to view components rather than partials for (apparently) better performance and easier testing
  - [] Stats Page
    - [] Add tabs for the type of stat
    - [] Add school-specific pages for each of the existing stats

- Future Plans

  - [] See if the occasional memory problems are actually something more like [this](https://www.engineyard.com/blog/thats-not-a-memory-leak-its-bloat/)
    - [] Also loading all the TimeSlots and Options from the start when calculating Invoice costs
    - [] Install and use Bullet gem
    - [] Also maybe Rack::Bug, or a newer version of something similar since it was last updated in 2015
    - [] Turnout gem to put it in maintenance mode?
  - [] Bump Ruby version and others as far as possible

    - [] Come up with a better logging system than just dumping them unsorted to S3 (apparently sending them to STDOUT sends them to Cloudwatch?)

  - [] Look into using our SES account/domain for the school emails to escape their 5000 email limit

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
