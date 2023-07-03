# July 2023

## July 1st-3rd Entry (Long weekend)

### Personal Project - [Portfolio](https://www.theodinproject.com/lessons/advanced-html-and-css-personal-portfolio)

- Navbar

  - [x] Doesn't close on mobile when you click a link

- Wiki
  - [x] Added notes on JS Object Construction

## July 4th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Changes

  - [] Move invoice list next to total cost and change the heading for total cost to the new translation
    - [] Migrate the DB column first, then make changes

- Features

  - [] Change the dependent option on all the invoice's associations to nil so they're still there if it's reified
    - [] List all deleted invoices on SMs page if there are any, with a restore button
    - Or look into [this](https://github.com/westonganger/paper_trail-association_tracking) if necessary
  - [] Add a count of students registered for each time slot, for all schools (or for all schools in an area for AMs)
  - [] Sort the condensed summary by percent of goal
    - Maybe get the data and create a hash with it, then just sort the hash and use it to make the rows?
  - [] Split the User#show pages out into different pages for different roles
  - [] Write a Stimulus controller allowing the condensed summary to be sorted by clicking a header

- Near event start features

  - [] Prevent slots closing on weekends, they should close the Friday before instead
    - Possibly hard code the relevant public holidays
  - [] For special days, display the connection option between the morning and afternoon slots (on the daily attendance sheet)
    - Maybe also show if kids are attending both morning and afternoon in that column for regular days
    - Just a different header/values
  - [] Style the print output to be more like the current attendance sheets for slot attendance
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

- Somewhere around the SM training

  - [] Give SMs a 'confirm with email' and 'confirm without email' button
    - [] Add copy button to the invoice show view just for SMs
    - [] Add a 'confirmation email sent' checkbox to the event sheet, same as 'entered'

- Security

  - [] SM can only log in from their school's IP address **requires IP list**

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

- Wiki
  - []
