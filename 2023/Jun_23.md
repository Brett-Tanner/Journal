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

  - [x] Remove unnecessarily large margins on login page
  - [x] Make the login form justified center, not start
  - [x] Remove unnecessary scroll bars on Chrome

- Time Sensitive Features

  - [x] Make authentication redirect the new splash page which links to login or sign up
    - [x] Style the new landing page
    - [x] Add the little arrows to the landing page buttons
  - [x] Add an instructional PDF to the login page
  - [x] Make the sign-up form fullscreen
  - [x] Make the activity names on the registration page labels linked to their checkboxes to avoid dead clicks
  - [x] Look into what Cloudwatch might be useful for
    - most of the free tier stuff we already get for free, and even if we get useful info from the paid tier when do I have time to look at it do anything about it?
  - [x] Re-add the ability to merge invoices from the active invoice
    - make the text in the dropdown the total cost
  - [x] Filter invoices shown on event sheet to only real ones, right now it's only filtering children with real ones but showing all
  - [x] Add the name of the day to the add slot partial date (in brackets)
  - [x] Change sorting order for admins to en_name on children
  - [x] Group children by school, same as for time slots

~~ - Invoice confirmation rework

~~ - [x] Add a user_confirmed field to Invoice model, which is set to true when they confirm on the confirm page - Allows us to save invoices so they persist when users hit back/abandon before confirming without showing in stats/sheets - By actually updating the invoice when the user goes to confirm from the registration page, but only using confirmed versions anywhere else ~~
~~ - [] Change the stats/sheets/indexes other places to decide what they show based on confirmation status ~~
~~ - [] Check all the logic that uses in_ss and think about how it could better use user_confirmed ~~
~~ - [] Use versions to handle cases where a user edits an existing booking but doesn't confirm it ~~
~~ - only the confirmed booking should be shown to staff/included in indexes/stats ~~
~~ - [] add a warning to the reg page/invoice index telling the user they have unconfirmed changes ~~
~~ - [] Change logic on which email is sent to use the new confirmed fields ~~

Abandoned the rework because saving invoices on the confirm screen also creates registrations, which has knock on effects to the rest of the site which shouldn't be caused by an unconfirmed invoice. In addition to the issue of displaying confirmed versions of the invoices themselves when the latest version can be unconfirmed, e.g. a user edits their existing booking but doesn't confirm it

## June 16th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Features

  - [x] Migrate the 'entered' boolean field into the Invoice table, default false
  - [x] Add a button for the SMs to set whether they entered a booking into the SS or not
    - There's an issue with the button displaying as entered when all a kid's invoices are confirmed
    - Might cause SMs to toggle it to not entered, which would unconfirm the last invoice
    - Probably not intended, so best to disable the buttons until I figure out the logic properly
    - Last commit **DID NOT ACTUALLY FIX IT** overwrite the changes when you get back
  - [x] Fix above issues by displaying a button per invoice
    - [x] And then go back and add an exception to display the big button again if there's only one invoice
    - [x] Disable the button unless the invoice in question is confirmed, so we don't skip confirmation emails to parents
    - [x] Restore seen at to its previous functionality as it can't be accurately updated via form
  - [x] Also update the list of invoices so they show as confirmed/unconfirmed correctly without a refresh
  - [x] Don't show the 'unconfirm' button if the child has other unconfirmed invoices

## June 19th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Bugfixes

  - [x] Prevent emails sending when admins edit invoices
  - [x] Figure out how to find accidentally deleted invoices (search papertrail versions by action, item type and created at)

### Work Project - [Registration Wiki](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [x] Import the 'Setting up a dev environment on WSL' tutorial I did
- [x] Make homepage use the doc layout so the sidebar is available, and autogenerate sidebar content from folders

### Odin Project - [Portfolio](https://www.theodinproject.com/lessons/advanced-html-and-css-personal-portfolio)

- [x] Scaffold the contents of each section

- Styling
  - [x] Give the main nav opacity and a cool frosted glass effect

## June 20th

### Odin Project - [Portfolio](https://www.theodinproject.com/lessons/advanced-html-and-css-personal-portfolio)

- [] Fill in each section

  - [x] Navbar

    - [x] Choose and add site logo
      - [x] Animate it bouncing on hover
      - [x] Animate it spinning on hover
      - [x] Filter it to orange when active
    - [x] Limit theme toggle triggering to the actual button

  - [x] Hero
    - [x] Greeting text in frosted div
    - [x] In Chrome/Safari this disappears and has to be scrolled into view?????
      - The grid seems to be huge, either the width or an overflow property is working differently to Firefox
      - Was caused by the min width of the columns being unlimited, need to use `minmax(0, something)` to keep it in check
    - [x] RGB background
  - [] Projects
    - [x] Slide up on visible, small delay on the second one

## June 21st

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Bugfixes

  - [] Copy_regs doesn't know about different arrival/depart options for kindy/elementary, teach it
  - [] Coupons (on the event sheet) still use the invoice id and are the only thing that does. Change it to the cost to match everything else

- Features

  - [] Make the summary tables responsive
    - Pretty sure there's just a BS class for that
  - [] Also make the daily attendance boxes responsive, they should just shift into a single column
  - [] Rather than completely blocking out regular days, put a red warning box on them (with the current text) and make the registerable as usual
    - [] Remove the check that removes registrations for regular days
  - [] Put the confirm page in a turbo-frame filled modal on the registration page
    - Then they can just close the modal and edit their booking without losing progress
  - [] Split the User#show pages out into different pages for different roles
  - [] Add a 'Latest Registrations' feed for staff
  - [] Change 'vh' units to 'dvh' because they solve the issue I had with stuff being cut off much more responsively

- Near event start features

  - [] Prevent slots closing on weekends, they should close the Friday before instead
    - Possibly hard code the relevant public holidays
  - [] For special days, display the connection option between the morning and afternoon slots (on the daily attendance sheet)
    - Maybe also show if kids are attending both morning and afternoon in that column for regular days
    - Just a different header/values
  - [] Style the print output to be more like the current attendance sheets for slot attendance
  - [] Allow staff to edit bookings for even closed activities
  - [] Add a search to the indexes (mainly for admins, there are too many pages and we don't know the order)

- Post event features

  - [] Look into using our SES account/domain for the school emails to escape their 5000 email limit
  - [] Have a way to stop sending emails when the event stops
  - [] Finish off the event creation features so someone other than me can actually do it
    - [] Add a way of uploading images to the S3 bucket from the site
    - [] Then selecting the blob to attach when creating an event/slot
    - [] Extend the 'all' option on event creation to allow specific schools to be selected
  - [] Stats page
    - [] Registrations per time
    - [] Average cost per invoice/school

- Security

  - [] SM can only log in from their school's IP address **requires IP list**

### Work Project - [Registration Wiki](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [] Add 'How to contribute'
  - [] Adding a page
  - [] Adding a section
- [] AWS section
  - [] Pushing a new version
  - [] Services we use and overview of what for

### Odin Project - [Portfolio](https://www.theodinproject.com/lessons/advanced-html-and-css-personal-portfolio)

- [] Fill in each section

  - [] About
  - [] Skills
    - [] On desktop, the BS list selector thingy
    - [] On mobile maybe the same but horizontal mode?
  - [] Projects
    - [] Links to github repo and live version
    - these cards can probably be an include
  - [] Contact

- Styling
  - [] Decide on a color scheme using [this site](https://realtimecolors.com/palettes/?colors=1e0f1f-eeddee-a151a4-e1c5e2-ad5eb0#generator)
