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

### Odin Project - [Library](https://www.theodinproject.com/lessons/javascript-library)

- [] Create the HTML scaffold

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Near event start features

  - [] For special days, display the connection option between the morning and afternoon slots (on the daily attendance sheet)
    - Maybe also show if kids are attending both morning and afternoon in that column for regular days
    - Just a different header/values
  - [] Style the print output to be more like the current attendance sheets for slot attendance
  - [] Prevent slots closing on weekends, they should close the Friday before instead
    - Possibly hard code the relevant public holidays

- Post event features

  - [] Remove all references to the email template column, then remove the column
    - [] Split the User#show pages out into different pages for different roles
  - [] Have a way to stop sending emails when the event stops
  - [] Finish off the event creation features so someone other than me can actually do it
    - [] Add a way of uploading images to the S3 bucket from the site
    - [] Then selecting the blob to attach when creating an event/slot
    - [] Extend the 'all' option on event creation to allow specific schools to be selected
  - [] Stats page
    - [] Registrations per time
    - [] Average cost per invoice/school
    - [] Bar graph of activity popularity (and by school)
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

### Work Project - WordPress Reservation Plugin

### Personal Project - [Portfolio](https://www.theodinproject.com/lessons/advanced-html-and-css-personal-portfolio)

- Navbar
  - Button on theme toggle goes outside on wide mobile screens
- [] About
  - [] Write a dev CV
- [] Projects

  - [] Expanding view transition between projects and their page
  - [] Fill in content for KU Regs tabs
    - [] Backend
    - [] Customer frontend
    - [] Staff frontend
    - [] Admin frontend

- Styling

  - [] Use [this site](https://realtimecolors.com/palettes/?colors=1e0f1f-eeddee-a151a4-e1c5e2-ad5eb0#generator) to get accent colors for stuff like the ring around the theme toggle
  - [] use CQI units for text scaling
