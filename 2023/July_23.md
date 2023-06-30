## July 1st

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Changes

  - [] Move invoice list next to total cost and change the heading for total cost to the new translation
    - [] Migrate the DB column first, then make changes

- Features

  - [] Look into [this](https://github.com/westonganger/paper_trail-association_tracking) to see if I can add a restore invoice button
    - In the show action, have an or to assign @invoice or @last version
    - actually, just change the dependent option to nil so the invoice can be restored and still have all its stuff
    - [] List all deleted invoices on SMs page if there are any
  - [] Add a count of students registered for each time slot, for all schools (or for all schools in an area for AMs)
  - [] Sort the condensed summary by percent of goal
    - Maybe get the data and create a hash with it, then just sort the hash and use it to make the rows?
  - [] Split the User#show pages out into different pages for different roles

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

### Work Project - WordPress Reservation Plugin

### Odin Project - [Portfolio](https://www.theodinproject.com/lessons/advanced-html-and-css-personal-portfolio)

- [] Fill in each section

  - [] About
    - [] Write a dev CV
  - [] Projects
    - [] Expanding view transition between projects and their page

- Styling
  - [] Use [this site](https://realtimecolors.com/palettes/?colors=1e0f1f-eeddee-a151a4-e1c5e2-ad5eb0#generator) to get accent colors for stuff like the ring around the theme toggle
  - [] use CQI units for text scaling
