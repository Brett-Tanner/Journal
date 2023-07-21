# July 2023

## July 1st-3rd Entry (Long weekend)

### Personal Project - [Portfolio](https://www.theodinproject.com/lessons/advanced-html-and-css-personal-portfolio)

- Navbar

  - [x] Doesn't close on mobile when you click a link

- Wiki
  - [x] Added notes on JS Object Construction

## July 4th

### Odin Project - [Library](https://www.theodinproject.com/lessons/javascript-library)

- [x] Create the Book object constructor
  - [x] Learn how to create class properties in TS
- [] Create the HTML scaffold

### Personal Project - [Portfolio](https://www.theodinproject.com/lessons/advanced-html-and-css-personal-portfolio)

- Wiki
  - Lots of reading about TypeScript and adding notes to the TS page

## July 5th

### Personal Project - [Portfolio](https://www.theodinproject.com/lessons/advanced-html-and-css-personal-portfolio)

- Wiki
  - [x] Add TypeScript, Classes, Functions and Variables to the JS section

## July 6th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Changes

  - [x] Add Minami-Machida's extra special day
    - [x] And the logic to exclude the morning from special day charges
    - [x] And the logic to charge 1100 yen for the afternoon rather than 1500 (FE & BE)
  - [x] Show special day afternoons in the daily attendance
  - [x] Move invoice list next to total cost and change the heading for total cost to the new translation
  - [x] Don't version changes to Invoices once they're confirmed, so SMs toggling email sent/entered etc. doesn't create a million versions

- Features

  - [x] Added list of badge kids to Yoshi's homepage
    - [x] Sort them by activities registered for
    - [x] Include special days, even the afternoon slot
  - [x] Add a count of students registered for each time slot for all schools
  - [x] Give SMs a 'confirm with email' and 'confirm without email' button
    - [x] Migrate the DB column first, then make changes
    - [x] Add copy (summary) button to the invoice show view just for SMs
    - [x] Add a 'confirmation email sent' checkbox to the event sheet, same as 'entered'
      - [x] Set all invoices confirmed at the time of the second button being added to email sent: true, as that was the only option for them
    - [x] Set 'email sent' when SMs choose to send the automatic one
  - [x] List all invoices an SM has deleted (if any) on their page, with a summary modal so they can manually recreate
    - [x] exclude zero cost invoices as those are auto-deleted by child merges, or irrelevant if manually deleted
  - [x] Write a Stimulus controller allowing the condensed summary to be sorted by clicking a header
    - [x] Handle numbers with more digits correctly by reducing numbers to actual

## July 7th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Changes

  - [x] Choose a redirect path after deleting a student that actually works
  - [x] Delete the non_ss kid after merging them with their SS counterpart
  - [x] Add a method to the Child model concatenating all their names into a string so it can be displayed when they're being selected for merging

### Personal Project - [Portfolio](https://www.theodinproject.com/lessons/advanced-html-and-css-personal-portfolio)

- [x] Started scaffolding the carousel for images on the registration project page, but was interrupted by work stuff

## July 10th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Bugs

  - [x] Fix emails not sending unless specifically chosen to send when SM confirms invoice
    - conditional was catching ALL emails without the email sent field being true, including customer updates
    - added an exception ensuring emails are sent if the current user is a customer
  - [] Remove start-of-line whitespace on copied summaries

- SM Issues

  - [x] Fix Shin-Kawasaki kids merged to the wrong sibling
    - [x] First
      - Complicating factor was the very early registration for the pendant activity which had been confirmed, and thus seemed to appear from nowhere on the merge
    - [x] Second
      - Way too many children complicated things, but basically it was just the wrong non-ss kid being merged to the wrong sibling. Moved that invoice and then merged the remaining non-ss kid to the correct ss version

- Near event start features

  - [x] For special days, display the connection option between the morning and afternoon slots (on the daily attendance sheet)
    - [x] Also stop showing kindy and ele extension separately for special day
    - Maybe also show if kids are attending both morning and afternoon in that column for regular days
  - [x] Style the print output to be more like the current attendance sheets for slot attendance
  - [x] Prevent potential issues with #next_event returning nil, especially before the end of the current event
    - Move the check to the current day being before the end date, not the start date
    - [x] Check views where it's used to make sure nil values between events are handled
  - [x] Find kids with SSID and parent_id nil, as they are leftovers from when merging didn't delete the non_ss kid
    - check them to see if they have undeleted invoices which might be affecting the stats
    - 6 did, figure out what's happening with them and resolve
  - [x] Prevent slots closing on weekends, they should close the Friday before instead
    - Possibly hard code the relevant public holidays

## July 12th

### Personal Project - [Portfolio](https://www.theodinproject.com/lessons/advanced-html-and-css-personal-portfolio)

- [x] Run Lighthouse on the site and follow the recommendations
  - [x] get and use differently sized images for different screen sizes

### Odin Project - [Library](https://www.theodinproject.com/lessons/javascript-library)

- [x] Create library array and addBook()
- [] Create showLibrary() to populate the bookshelf div
  - Learned documentFragment is not actually a more performant way to append a bunch of stuff than just looping
  - Also you can append all at once using `.append()` and the spread notation rather than `.appendChild()`

## July 13th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Changes

  - [x] Take away SM foot gun by removing manual SSID entry from child forms
  - [x] And their ability to delete children
  - [] Remove start-of-line whitespace on copied summaries

- Testing

  - [x] Merge all the Okurayama kids (at least those with SS counterparts) to check it works when the user can read

- Features

  - [x] Give SMs a button to toggle first seasonal status on Child#show
  - [x] Make it unbelievably obvious which child is being merged from by rendering full forms with different tables for each
    - [x] Put the SS kid and candidate non-ss kids in a table right next to each other, color coded
    - [x] Have the merge button pop up a modal that asks them if they're really, really sure
    - [x] The actual form to submit is in the modal footer as a button
    - [x] Add the new translations/warnings
  - [x] Stats page
    - [x] Choose between the chartkick and gruff gems
      - Chartkick, much more popular and fully developed
    - [x] Scaffold the page, install gems, figure out how they work etc.
    - [x] Registrations per day/week
    - [x] Per day of the week
    - [x] Revenue per day/week
    - [x] Average cost per invoice/by school
    - [x] Number of activities per booking (not by school yet)
    - [x] Number of attendees by category
    - [] Bar graph of activity popularity (and by school)

## July 15th

### Odin Project - [Library](https://www.theodinproject.com/lessons/javascript-library)

- [x] Create showLibrary() to populate the bookshelf div
  - Learned documentFragment is not actually a more performant way to append a bunch of stuff than just looping
  - Also you can append all at once using `.append()` and the spread notation rather than `.appendChild()`
- [] Add a button that brings up a form for adding books
  - [x] Add & style the button
  - [x] Add form
  - [] Put the form in a modal triggered by the add book button

## July 17th

### Odin Project - [Library](https://www.theodinproject.com/lessons/javascript-library)

- [x] Add a button that brings up a form for adding books
  - [x] Put the form in a modal triggered by the add book button
- [x] Add a button on each book to remove it from the library
- [x] Add a button on each book to toggle its read status

## July 18th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Changes

  - [x] Remove online test event from stats
  - [x] Add some color to the charts
  - [x] Remove the unnecessary timezones causing weird behaviour with the current day's bookings
  - [x] Fix the header row overlapping the first row (on chrome at least) whe printing attendance sheets
    - Seems to be an issue with sticky? Position changes when scrolling in devtools print mode
    - Was the offset I use on the sticky header to avoid it overlapping the navbar. Removed it in the print media query
  - [x] Link the afternoon special days (on daily attendance sheet) to the morning slot's attendance sheet
    - [x] On a related note, afternoon only kids aren't shown for special days. Fix that
    - [x] And stop the allergy column on attendance tables causing them to overflow
  - [x] Remove whitespace on copied summaries

- Features

  - [] Finish off the event creation features so someone other than me can actually do it
    - [] Event step
      - [x] Allow an image to be selected from the 'events' S3 folder
      - [x] Generally update the fields/controller/routing with new knowledge
      - [] Extend the 'all' option on event creation to allow specific schools to be selected

## July 19th

### Work Project - WP Reservation Plugin

- [x] Add accounts for each school
- [x] Add a Setsumeikai service for each school
- [x] Customise the form to match the current one
- [] Make an API available on the WP site so GAS can access the data it needs
  - [x] Set up Postman to test/check the contents of old/new APIs
  - [x] For customers
  - [x] For schools
    - But getting an empty response every time, maybe they're deleted after relevant so nothing there?
    - Or maybe my school value in the payload is wrong in some way
  - It's possible the API is actually set up on the new site somehow, so look into that
  - The current site's API is v2, while the one I was given is v1. Wonder where the v1 is?
- [] Add filtering by
  - [] name
  - [] closest station
  - [] area (kanagawa, tokyo etc.)
  - Add script tag to the template (and search box)
    - Gets the school cards by class
    - Reads their names, which are used as keys to a hash in the script tag that contains the other info
    - Hide everything that doesn't match the entered string in some way
- [] Multi-school selection
  - Not sure it's even possible

## July 20th

### Work Project - WP Reservation Plugin

**Realised it might not actually be possible to set up the schedule the way we need it. Special days seem to get ignored, and services can't be set on a day by day basis**

- [] Make an API available on the WP site so GAS can access the data it needs
  - [] Read up on WP APIs
    - Endpoints have a controller which provides data much like Rails
    - You can pass an authentication function to check authorization, or just return true if public
      - Maybe also use [Application Passwords](https://developer.wordpress.org/rest-api/using-the-rest-api/authentication/#basic-authentication-with-application-passwords) for auth
  - [] Find the table BP is submitting to
  - [] Create an API for it
  - [] Inquiry form needs to submit to the database too so the API can retrieve the parents
- [] Add filtering by
  - [] name
  - [] closest station
  - [] area (kanagawa, tokyo etc.)
  - [] by text and dropdown
  - Add script tag to the template (and search box)
    - Gets the school cards by class
    - Reads their names, which are used as keys to a hash in the script tag that contains the other info
    - Hide everything that doesn't match the entered string in some way
- Styling
  - [x] Make the school cards flex row so they're smaller
  - [x] Stop the main content scrolling
  - [x] Stretch the school card grid to take up the whole container
  - [x] Center the header
  - [] Make it clear which days are available with an orange circle
  - [] Also a bigger calendar if possible
- [] Multi-school selection
  - Not sure it's even possible

## July 21st

### Work Project - WP Reservation Plugin

**Plugin won't work for our purposes**

- Rewrote the possible solutions in light of this
- Looked up a calendar gem if I get to do it in Rails, picked [Simple Calendar](https://www.ruby-toolbox.com/projects/simple_calendar)

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Features

  - [] Finish off the event creation features so someone other than me can actually do it
    - [] Event step
      - [] Extend the 'all' option on event creation to allow specific schools to be selected
    - [] Time Slot step
      - [x] Show the event partial at the top of the form
      - [x] Give them an 'add time slot' button
      - [x] Add a dropdown to select an image from available active storage blobs (group images by event?)
      - [] Allow updating time slots for all events with the same name
    - [] Add a way of uploading images to the S3 bucket from the site
      - [] Upload to a specific folder based on purpose of image
      - [] Make sure large files work, they didn't the first time
    - [] Remove ability to destroy events from frontend when I'm done testing (no route for it)

## July 22nd

### Work Project - Setsumeikai

- Rails DB setup
  - Each school gets a setsumeikai event (add a setsumeikai category to that enumerable)
    - The actual setsumeikai is a time slot on that event, SMs can create and edit those time slots for their schools
  - I add area and nearby train stations to the school table so we can sort by those
  - New table for something like 'leads' which will be where we store the info customers submit when requesting a setsumeikai
- Will need SM interfaces for
  - List of leads (per setsumeikai and overall)
  - Calendar view where they can see their setsumeikais
- Customer interface needs
  - School selection
    - with filter by area/station/name etc
  - Then date selection with the calendar
  - Then the form
  - Then a confirmation which shows the details they entered

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Features

  - [] Finish off the event creation features so someone other than me can actually do it
    - [] Event step
      - [] Extend the 'all' option on event creation to allow specific schools to be selected
    - [] Time Slot step
      - [x] Show the event partial at the top of the form
      - [x] Give them an 'add time slot' button
      - [x] Add a dropdown to select an image from available active storage blobs (group images by event?)
      - [] Allow updating time slots for all events with the same name
    - [] Add a way of uploading images to the S3 bucket from the site
      - [] Upload to a specific folder based on purpose of image
      - [] Make sure large files work, they didn't the first time
    - [] Remove ability to destroy events from frontend when I'm done testing (no route for it)
  - Stats page
    - [] Add school-specific pages for each of the existing stats
  - [] Figure out what needs to change to stop persisting a blank invoice when there are no unconfirmed invoices available for a child and someone looks at their registration page
  - [] Remove all references to the email template column, then remove the column
    - [] Split the User#show pages out into different pages for different roles
  - [] Have a way to stop sending emails when the event stops
  - [] Look into using our SES account/domain for the school emails to escape their 5000 email limit

### Work Project - [Registration Wiki](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [] Add 'How to contribute'
  - [] Adding a page
  - [] Adding a section
- [] AWS section
  - [] Pushing a new version
  - [] Services we use and overview of what for
- [] Rails section
  - [] Overview
  - [] Useful Commands
