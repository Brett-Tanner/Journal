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

- [] Show remove from cart button on cards in cart
- [] Find out why empty cart message isn't displaying
- [] Split out increment, decrement and remove from cart callbacks as props to card, and define them in the shop component

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
