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
- DOM
  - [x] Initially just inputs for name, human or computer

## September 7th

### Odin Project - [Battleship](https://github.com/Brett-Tanner/battleship)

- [x] Add possibleEnds(currentCoords) to ship
- [x] Add possible property to spaces
- DOM
  - [x] Create basic board

## September 8th

### Odin Project - [Battleship](https://github.com/Brett-Tanner/battleship)

- [x] Add getCoordinates() to get the coordinates of a domSpace in the rows array of the representation in memory
- [x] Add test to reject a space for possible ends if it contains a ship
- [x] Very possible I want to remove the possible property from spaces and just do that through event listeners in the DOM
- [x] Add placeShips() to player
  - takes main as an argument
  - [x] creates a new board as innerHTML of main (w/heading saying Player $ place your $)
    - [x] remember to show ships already placed
    - [x] and not add start listeners to cells already occupied by a ship
  - for each ship of that player's gameBoard
    - [x] attach listeners to every cell of the board which set it as the start point (and generates a new board without listeners)
    - [x] await the promise around that listener resolving (in the listener callback)
    - [x] use the value of the resolved promise (the start cell) to show the possible spaces the ship can end on
      - [x] return a promise, resolved by added listeners with end coordinates to them
    - [x] use the start and end coordinates to place the ship
    - [x] recursively call the function till you run out of ships, at which point you resolve the promise placeShips returns and let the game loop know it's ok to move on
- DOM
  - [x] Create basic board
    - [] Add a an optional board type argument (placement, obscured) to createBoard
  - [] Prompts for move (click, see possibilities, then click again)
    - [] Countdown timer before board obscurity is switched
  - [] Create displayMessage(), called when
    - Ship sinks
    - Attack hits or misses
    - Player wins
  - [] Prevent ships crossing each other at points other than the end
  - [] Figure out what sometimes causes end overlaps to not be notice

## September 9th

### Odin Project - [Battleship](https://github.com/Brett-Tanner/battleship)

- DOM
  - [x] Create basic board
    - [x] Add a an optional obscured boolean to createBoard
  - [x] Prompts for attack
    - [x] Display hit marker if hit, miss if miss
    - [x] Display message showing which ship was hit if any, or a "You missed" message
    - [x] Figure out which modules the methods should be on (in takeTurn on player)
    - [x] Figure out how to loop between the players (recursively call take turn on the other player until allSunk for one of them)
    - [x] Render button to pass to other player (lack of this is why the hit/miss messages don't show)
  - [x] Stop hit markers displaying twice on the unobscured board (was being rendered once in the ship marker, once outside)
  - [x] End the game and display victory message if all a player's ships are sunk
  - [x] Prevent ships intersecting each other at points other than the end
  - [x] Figure out what sometimes causes end overlaps to not be noticed (I only checked for them on the up possible end)
  - [x] Don't add listeners to squares you already hit or missed

## September 10th

### Odin Project - [CV App](https://github.com/Brett-Tanner/odin-cv)

- Create a CV, where info is displayed by default and can be edited/saved by clicking a button
- Sections for basic info, education and work experience
- [x] Create forms (editing state)
- [x] Create edit/save button component
- [x] Create display versions (not editing state)
- [x] Deploy to Netlify, Cloudflare or Vercel
  - Vercel, it was the only one where I could find [instructions](https://maximevermeeren.medium.com/how-to-use-bun-on-vercel-7512383153d7) for deploying using a Bun runtime
  - You'll also want to switch the build command in package.json to be `"~/.bun/bin/bun vite build"`, cos bun won't be in the path after install

## September 11th

- Buy brett-tanner.dev!
- Create a new personal site with Astro/Starlight and deploy it to my new domain
- Add the React docs page and my notes on useEffect
- In Astro/Starlight, if you have trouble importing `astro:content` in a page, just drag it into the main pages directory then back into the one you want????????
  - I guess maybe because I made it before exporting the collection types???
  - This one was really weird
  - [Github issue](https://github.com/withastro/astro/issues/5711) which I don't think helped much but certainly gave a lot of options to try

## September 12th

- Starlight splash page colors match up with Tailwind grays, 900 is the main background color
- Decide to switch to separate repos for wiki/portfolio, portfolio will be plain Astro while wiki sticks with Starlight
- Remove my domain from the current one, delete the pages project and redirect the domain to my current GH pages site
  - Has the handy side effect of all my GH pages sites redirecting to brett-tanner.dev/repo-name now as well

### Odin Project - [Pokemon Memory Game](https://github.com/Brett-Tanner/odin-memory)

- API stuff

  - [x] get list of all pokemon URLs and put it in state
  - [x] pick 20 random ones to fetch details for from the api
    - [x] create a pokemon object for each { id, name, src, clicked } and add them to an activePokemon state
    - [x] filter out pokemon with no front sprite
    - [x] filter out pokemon with the same ID

- Render a pokemon component for each pokemon retrieved

  - [x] key is the id
  - [x] Sprite, name under, pokemon themed styling
  - [] on click
    - [] if not clicked, set its clicked property to true, increment score by one and randomize the active pokemon (set it to a reversed copy of itself)
    - [] update PB if necessary
    - [] if clicked, display game over message and offer to play again

- Score component at the top, shows current score, best score (each their own state)

- Later, add ability to choose number of active pokemon/region they're from (by id, they're in release order)

  - this will be a filter state object

## September 13th

- [x] Start the new wiki repo using Starlight/tailwind
  - and copy over existing react page/necessary settings
  - make some notes on React testing
- [x] Get it online under wiki.brett-tanner.dev

### Odin Project - [Pokemon Memory Game](https://github.com/Brett-Tanner/odin-memory)

- Pokemon cards

  - [x] on click
    - [x] increment the click counter by one
    - [x] if clicked more than once, display game over message
    - [x] randomize the activePokemon array
    - [x] update score
    - [x] update PB if necessary

- Score component at the top, shows current score, best score (each their own state)

  - [x] show score and personal best
  - [x] reset score when game resets, but keep PB

- Live version
  - [x] Remember the package.json script I use to push to GH pages
  - [x] Remember I need to modify the base in vite.config or stylesheets/js won't load

## September 14th

- Added a bunch of notes to the React section of the wiki on

  - React Router
  - Fetching Data

- Took a brief look over the shopping cart project, big fan of the MTG version someone did. Maybe a similar LOR/Mobalytics API I could use? Yu-Gi-Oh?

## September 15th

### Odin Project - [Shopping Cart](https://github.com/Brett-Tanner/shopping-cart)

Components without state to get the layout/loading view, then write tests for what they should be like with state, then add all the state and data fetching.

- Homepage/landing page
- Shopping cart
- Individual product pages?
- Sidebar to filter the cards you see

- Skeleton components
  - [x] Nav bar
  - Hero
    - [x] background image & shadow

## September 16th

### Odin Project - [Shopping Cart](https://github.com/Brett-Tanner/shopping-cart)

Ported my HTML notes over to the new wiki.
Didn't actually write any tests, but set up testing and some skeleton files.

- Skeleton components
  - Hero
    - [x] contents
  - [x] Setup React Router so I can go to the other page for testing

## September 17th

### Odin Project - [Shopping Cart](https://github.com/Brett-Tanner/shopping-cart)

- Write tests
  - [x] Card card

## September 19th

### Odin Project - [Shopping Cart](https://github.com/Brett-Tanner/shopping-cart)

- [x] Test and implement increment/decrement buttons
- [x] Reverse side w/card details
- [x] Style shop variant
- [x] Cart variant (w/different styles)
- [x] Add cart modal

## September 20th

### Odin Project - [Shopping Cart](https://github.com/Brett-Tanner/shopping-cart)

- [x] Fetch the cards from MTG API
- [x] Create a loading state

### Work Project - [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- DB

  - [x] Remove email template, billing date columns (invoices)
  - [x] Remove description column (time slots, options)
  - [x] Remove name, combinable, discount from coupons
  - [x] Remove IP from users
    - (I never liked it, Jack seems to have forgotten about it, potential scandal if someone sees the code and thinks we're collecting IP addresses? IDK probably not an issue anyway but we don't need it)
  - Change 'needs_hat' to 'first_seasonal' to match its meaning (child)
    - [x] Add first_seasonal
    - [x] Migrate existing needs_hat values to first_seasonal
      - The old attr_accessor workaround I had with a fake first seasonal param was preventing me setting the new col
    - [x] Update all kids who attended to have 'first_seasonal' = false
    - [x] Remove all references to needs_hat and replace with first_seasonal
    - [x] Remove needs_hat col
  - Time Slot table
    - [x] Internal/external modifier
    - [x] Snack boolean
  - Add counter_cache
    - TimeSlot registrations
      - [x] Update daily attendance to use #size so it'll use the counter_cache
    - Option registrations
      - [] Where is this useful?
  - [] Remove old PaperTrail versions once I'm done making invoice table changes (invoices, children)
  - [] See if it's vacuuming/analyzing by default, if not make it do that

- Per-activity costs

  - Use per-slot/int/ext modifiers and snack boolean in
    - [x] Afternoon slot auto-creation (set to true unless a special day)
    - [x] Invoice#calc_cost
    - [x] In JS cost calculation
    - [] Display extra cost if any on the registration form
    - [] Add fields for them on time slot forms

## September 21st

### Odin Project - [Shopping Cart](https://github.com/Brett-Tanner/shopping-cart)

- [x] Show remove from cart button on cards in cart
- [x] Find out why empty cart message isn't displaying
- [x] Host on Vercel

### Work Project - [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- DB

  - [x] Remove old PaperTrail versions once I'm done making invoice table changes
    - Add a check to anything that relies on versions that versions actually exist for it
      - [x] Mailer whodunnit
      - [x] Invoice changes col in event sheet
    - [x] Make sure I'm not creating unnecessary versions when stuff like seen is updated on invoices
  - [x] See if it's vacuuming/analyzing by default, if not make it do that
    - Seems its fine, using the AR method [here](https://stackoverflow.com/questions/14824453/rails-raw-sql-example) with the query [here](https://aws.amazon.com/blogs/database/understanding-autovacuum-in-amazon-rds-for-postgresql-environments/) under 'Dead Tuples' showed recent vacuums and analyzes for all tables I'd expect them on
  - [x] Add real scope to schools (excludes online and test)

- Event Creation

  - Find all the stuff with hardcoded event ids/links between school id/event id/user id and refactor it
    - [x] Diff school reg seems to be hardlinked to an event id that's related to the school id?
      - Yeah was just the school id lol. Changed it to a proc which gets the id of the next event instead
      - Still not ideal cos querying n+1 in the view, but can be left for my big optimisation run if it ever happens
    - [x] In condensed summary, all events show up
    - [x] School stats summary shows past events
    - [x] Daily activities list activities for all events
      - [x] Added the ability for SMs to see attendance for past events while I was there
    - [x] Realise a whole bunch of stuff breaks when there are no upcoming events, and add checks to prevent that
    - [] Stats page uses data from all events together

- Invoices

  - [x] Only show real invoices in index

- Per-activity costs

  - [x] Generate data attributes with the modifiers in SSR
    - If not done JS gives NaN when existing regs added to, because SSR p elements didn't have a data attribute
  - [x] Display extra cost if any on the registration form
    - [x] Add the translations for 'extra charge' when I get them, here and to replace special day in the invoice
  - Add fields on time slot forms
    - [x] modifiers
    - [x] snack

- UX

  - [x] Add 'don't refresh' warning to time slot forms
    - causes the current image to be swapped out in some cases
    - also some option category issues for individual slot edits
  - [x] Sort invoice index by event date
  - [x] Change close/reopen button color on hover/active for daily activities

- Views

  - Charts Page
    - [x] Show action takes school id as a param and shows stats for only that school
    - [x] Add nav for admin/AM to look at each school's stats

## September 22nd

### Work Project - [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- DB

  - Add counter_cache
    - Invoice slot regs
      - [x] Use as the new real scope

- Invoices

  - [x] Remember why the 'real' scope has a distinct on it

- Stats page

  - [x] Add tabs for the type of stat
    - Add dynamic show page for
      - [x] Activities
      - [x] Bookings
      - [x] Children
      - [x] Coupons
      - [x] Edits
      - [x] Options

## September 25th

- Finish my notes on React

### Work Project - [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [x] Condense the nav filters on stats page into a dropdown for each filter
- [x] Refactor categories to partials so they can be reused in index
- Get tabs working on Index for
  - [x] Activities
  - [x] Bookings
    - [x] Add charts for bookings by hour of day and day of week

## September 26th

### Work Project - [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [x] Options with radio buttons cause the FE JS calculation to fail

  - Was checking name !== null for some reason
  - too narrow because name could be undefined
  - changed it to just be `if name` since both null & undefined are falsy

- DB

  - Add counter_cache
    - TimeSlot registrations
      - [x] Use in stats to dramatically reduce joins
    - Option registrations
      - [] Where is this useful?
        - It had to be added as part of tracking registrations for time slots, but not sure where it could be used
    - [x] All counter_cache cols should be 0 by default, not nil
      - [x] Make sure all existing counters in prod are set to an integer

- Invoices

  - [x] Stop persisting blank invoices when registration page viewed

- Stats page

  - Get tabs working on Index for
    - [x] Children
    - [x] Coupons
    - [x] Edits
    - [x] Options
  - [x] Add option stats by category
  - [x] Chase down a few assorted bugs/typos
  - [x] Let Leroy download stats per event from the CSV export

## September 27th

### Work Project - [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- UX

  - [x] Sort activities on Invoice summary
  - [x] Exclude kids who received a hat from hat kids list
  - [x] Sort arrival/departure options by modifier
    - different directions for each
    - right now they're in creation order, potential problem now we can manually edit
  - Forms
    - Add useful error messages to all forms
      - [x] Login
        - was missing translations for the validation messages
      - [x] Password reset
        - was also pretty ugly, so I tidied up the styling a bit
      - [x] Sign up
        - FE validation wasn't triggering
        - br tags littered everywhere
        - padding was too thick on mobile
      - [x] Child form
        - Was ignoring the BS ones and rendering the form full-screen with backend errors
        - Switched back to HTML validation, and styled the backend errors so they look nicer if displayed

- Views

  - User
    - Split show pages into dynamic routes based on role
      - [x] Customer
      - [x] SM
      - [x] AM
      - [] Admin

- Future Plans

  - See if the occasional memory problems are actually something more like [this](https://www.engineyard.com/blog/thats-not-a-memory-leak-its-bloat/)
    - [x] Install and use Bullet gem

## September 28th

### Work Project - [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Invoices

  - PDF Invoice Generation
    - [x] Pick a gem from prawn or hexapdf
      - WickedPDF and pdfKit are based on HTML to PDF converters, so slower and more dependencies. They're out
      - Went with prawn, hexapdf requires a license for commercial use
      - [x] Learn to use Prawn
        - [x] And write a wiki page with the useful bits
    - Setup the basic layout
      - [x] Header

- UX

  - [x] Move condensed stats table and headers into the partial as well
    - means sorting out something else to pass
  - [x] Give AMs the ability to sort condensed stats as well

- Views

  - User
    - Split show pages into dynamic routes based on role
      - [x] Admin
    - [x] Kill all the N+1 queries for User#show
    - [x] Fix some bugs caused by no upcoming events

### Work Project - [Seasonal Wiki](https://github.com/Brett-Tanner/KU-wiki)

- [x] PDF Generation

## September 29th

### Work Project - [Setsumeikai Calendar](https://github.com/Brett-Tanner/setsumeikai_calendar.git)

- Initialize the project and verify ReactPress/Vite/Tailwind etc. all work together
  - [x] Export site from Tools, and download theme from the themes folder in the file manager
  - [x] Figure out how to set up WPLocal
    - Download it, start a new project, import the .xml file from the main site and the theme .zip I downloaded from the file manager
    - React app goes in a subfolder of the Local project, I'll make that folder the git repo and just have two identical Local setups on my PCs

### Work Project - [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Invoices

  - PDF Invoice Generation
    - Setup the basic layout
      - [x] Summary
      - [x] Footer
    - [x] Fill it with details
