# June 2023

## June 1st

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Bugfixes

  - [x] Had one less column on the event sheet than needed because I was subtracting both special days from the number of columns, despite them only taking one

- Features

  - [x] Give big boss AM an overall summary for the company too

### Personal Project - Wiki

- [] Style the navs for each topic
  - [x] Ruby
  - [x] Rails
  - [x] Jekyll
  - [x] Git

### What I learned

- You can always just set the base height/width of an img in HTML properties, especially useful when a BS .img-fluid has gigantism
- Jekyll layouts can be nested, just use the parent layout as the layout of the child layout

## June 2nd

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Bugfixes

  - [x] Stopped a new child/schedule version being created each time they're updated due to manually setting created and updated at
  - [x] Set backup retention back to 14 days after it somehow got set to 2

## June 3rd

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Bugfixes

  - [x] Photo service is bugged, it's impossible to register for right now. Works in JS but is not present on confirm page or confirmed invoice
    - Was being caught by the orphan option check as event options never have an associated slot
    - Added a guard clause to except event options from said check

## June 5th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Bugfixes

  - [x] Two schools were in the wrong areas (Ikegami and Toyocho) so I switched them
    - Actually, they had their ids switched. The correct ids were in the correct areas, but those ids were associated to the wrong school/name
    - Means:
      - Anyone who signed up without associating their kid to an SSID is fine, they manually chose the school which reflects the order of the schools in the database
      - But any kid imported from the SS is at the wrong school, because it's mapped wrong.
        - So to fix, maybe we just change the mapping in the SS imports?
          - Nah change the names to avoid confusion on future. Name/id mapping is same everywhere
        - Then for both of those schools, check if any of their students have an invoice for an event at the other school, switch to the correct event if so
  - [x] Renamed the schools to match the SS mapping, then made sure all associated children/invoices/events/managers were associated with the right one

### Personal Project - Wiki

- [x] Style the navs for each topic
  - [x] HTML

## June 6th

### Personal Project - Wiki

- [x] Added a table of contents to the css/animations page, will re-use on others

### Odin Project

- [x] [Transforms](https://www.theodinproject.com/lessons/advanced-html-and-css-transforms)
- [x] [Transitions](https://www.theodinproject.com/lessons/advanced-html-and-css-transitions)

## June 7th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Bugfixes

  - [x] Fixed one of the invoices broken by the Toyocho/Ikegami switch as a proof
    - [] Fix the others (2?)

### Odin Project

- [x] [Keyframes](https://www.theodinproject.com/lessons/advanced-html-and-css-keyframes)
- [x] [Animation Exercises](https://github.com/TheOdinProject/css-exercises/tree/main/animation)
- [x] [Intro to Accessibility](https://www.theodinproject.com/lessons/advanced-html-and-css-introduction-to-web-accessibility)
- [x] [Web Content Accessibility Guidelines](https://www.theodinproject.com/lessons/advanced-html-and-css-the-web-content-accessibility-guidelines-wcag)
- [x] [Semantic HTML](https://www.theodinproject.com/lessons/advanced-html-and-css-semantic-html)
- [x] [Accessible Colors](https://www.theodinproject.com/lessons/advanced-html-and-css-accessible-colors)
- [x] [Keyboard Navigation](https://www.theodinproject.com/lessons/advanced-html-and-css-keyboard-navigation)
- [x] [Meaningful Text](https://www.theodinproject.com/lessons/advanced-html-and-css-meaningful-text)

## June 8th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Bugfixes

  - [x] Fixed one of the invoices broken by the Toyocho/Ikegami switch as a proof
    - [x] Fix the others (2?)
  - [x] On the event sheet in the coupon column, it says 'Booking#246' in English
    - Change to just be the number, it's right next to it
  - [x] Transfer the kid's registrations who registered for their regular school but wanted to go to a different one
  - [x] Make event partial calendar image full width
  - [x] School never displays on child profile, should be the name or dashes but it's just blank
    - It was just a missing English translation for the admin accounts

- Chores

  - [x] Change dev seeds to use the Summer event

- Features

  - [x] When generating invoice details, just skip if the option name is 'なし'
  - [x] Give parents an easy way to register their kid for an event at a different school
    - Add to the event partial, as a form that lets them select another school to register at
  - [x] Highlight students from other schools on the event sheet
    - Add a col (titled 担当校舎) which contains the kid's regular school and is highlighted if different to the event school
    - [x] pop up the name of their regular school in a popover
  - [x] Add conditional to show correct event partial if registered for an event at a school other than their regular one
  - [x] Add Clarity to the site so we can use heatmaps
  - [x] All AMs want the all schools summary, so remove special code for big boss and maybe condense admin/AM conditionals a bit

## June 9th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Bugfixes

  - [x] Ensure regular days are not registered for when copying registrations during child merge
    - [x] But only for afternoon, merge invoices was also preventing for mornings as well

### Odin Project

- [x] [WAI-ARIA](https://www.theodinproject.com/lessons/advanced-html-and-css-wai-aria)
- [x] [Accessibility Auditing](https://www.theodinproject.com/lessons/advanced-html-and-css-accessibility-auditing)

## June 10th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Bugfixes

  - [x] Hide the card with invoices, mailer subscriptions etc. when the parent has no children, clearly its too distracting for them
  - [x] Hide the invoice index button for children/parents without real invoices, similar reason
  - [x] Only show real invoices in Invoice#index
  - [x] Still default to showing events at the kid's school unless they've actually registered for something at another school
  - [x] Get rid of the weird margin at the bottom of login page on certain mobile viewports

## June 11th

### Odin Project

- [x] [Intro to Responsive Design](https://www.theodinproject.com/lessons/advanced-html-and-css-introduction-to-responsive-design)
- [x] [Natural Responsiveness](https://www.theodinproject.com/lessons/advanced-html-and-css-natural-responsiveness)
- [x] [Responsive Images](https://www.theodinproject.com/lessons/advanced-html-and-css-responsive-images)

## June 12th

### Work Project - [Registration Wiki](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [x] Initialize the Astro project

### Odin Project - [Personal Portfolio](https://www.theodinproject.com/lessons/advanced-html-and-css-personal-portfolio)

- [x] [Media Queries](https://www.theodinproject.com/lessons/advanced-html-and-css-media-queries)

- [x] Scaffold the homepage, top nav and contact info footer
- [] Add a light/dark mode toggle like the one on [this guy's blog](https://vanntile.com/blog/next-to-astro/)

## June 13th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Bugfixes

  - [x] Ensure options are also unregistered when unregistering from regular day afternoons

### Odin Project - [Personal Portfolio](https://www.theodinproject.com/lessons/advanced-html-and-css-personal-portfolio)

- [x] Add a light/dark mode toggle like the one on [this guy's blog](https://vanntile.com/blog/next-to-astro/)
- [x] Persist user theme preference across browser sessions
- [x] Automatically set the theme (and slider position) from browser preference

### Personal Project - [Personal Wiki](https://brett-tanner.github.io/)

- [x] Added the JS section that was missing for some reason

## June 15th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Bugfixes

  - []

- Features

  - [x] Make authentication redirect the new splash page which links to login or sign up
    - [x] Style the new landing page
    - [x] Add the little arrows to the landing page buttons
  - [x] Add an instructional PDF to the login page
  - [] Possibly bring the recalculate button back, e.g. for children whose category in the SS changed since their booking was made
  - [] Make the activity names on the registration page labels linked to their checkboxes to avoid dead clicks
  - [] Add a search to the indexes (mainly for admins, there are too many pages and we don't know the order)
  - [] Add a 'Latest Registrations' feed for staff
  - [] Add an 'Incomplete Registrations' feed as well
  - [] Rather than showing a blank page on the invoice index when there're no real invoices, show a 'No confirmed invoices, #{num} unconfirmed" message
  - [] Prevent slots closing on weekends, they should close the Friday before instead
    - Possibly hard code the relevant public holidays
  - [] For special days, display the connection option between the morning and afternoon slots (on the daily attendance sheet)
    - Maybe also show if kids are attending both morning and afternoon in that column for regular days
    - Just a different header/values
  - [] Look into using our SES account/domain for the school emails to escape their 5000 email limit

- Invoice confirmation rework

  1. Migrate the new user_confirmed column in, check nothing is on fire
  2. Then try out the other changes locally before pushing

  - [] Add a user_confirmed field to Invoice model, which is set to true when they confirm on the confirm page
    - Allows us to save invoices so they persist when users hit back/abandon before confirming without showing in stats/sheets
    - By actually updating the invoice when the user goes to confirm from the registration page, but only using confirmed versions anywhere else
    - [] Change the stats/sheets/indexes other places to decide what they show based on confirmation status
    - [] Check all the logic that uses in_ss and think about how it could better use user_confirmed
  - [] Use versions to handle cases where a user edits an existing booking but doesn't confirm it
    - only the confirmed booking should be shown to staff/included in indexes/stats
    - [] add a warning to the reg page/invoice index telling the user they have unconfirmed changes
  - [] Change logic on which email is sent to use the new confirmed fields

- Security

  - [] SM can only log in from their school's IP address **requires IP list**

### Work Project - [Registration Wiki](https://github.com/Brett-Tanner/db_prototype_v2.git)

- []

### Odin Project - [Portfolio](https://www.theodinproject.com/lessons/advanced-html-and-css-personal-portfolio)

- [] Scaffold the contents of each section
- [] Fill in each section
  - [] Hero
  - [] About
  - [] Skills
    - [] On desktop, the BS list selector thingy
    - [] On mobile maybe the same but horizontal mode?
  - [] Projects
    - [] Slide up on visible, small delay on the second one
    - [] Links to github repo and live version
    - these cards can probably be an include
  - [] Contact

### Personal Project - [Personal Wiki](https://brett-tanner.github.io/)

- []
