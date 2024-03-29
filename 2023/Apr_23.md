# April 2023

## Apr 3rd

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

Busy with Spring school/new kids' book stickers

- [] Requests/Bugfixes
  - [x] Children now update their names properly when edited through parent as nested attributes
  - [x] Staging branch .gitignore updated to dramatically reduce bundle size

#### What I learned

- Use `git checkout <commit id>`, not git reset if you wanna try out a past version
- Figured out nested attributes weren't the problem since other child attributes could be edited fine
  - It was actually because nested records aren't validated, so the before_validated callback which sets names was never triggered
  - Resolved by adding 'validates_associated :children' to the User model
- To remove files using .gitignore that have already been tracked, you need to `git rm -rf --cached foldername` after editing .gitignore

  - To ignore a folder except for a few files, do something like this

  ```
  /spec
  /app/assets/images/*
  !/app/assets/images/arrow-right.svg
  !/app/assets/images/favicon.svg
  !/app/assets/images/logo.svg
  !/app/assets/images/white_logo.svg
  !/app/assets/images/login_splash.avif
  !/app/assets/images/login_splash.jpg
  !/app/assets/images/sm_login_splash.avif
  !/app/assets/images/sm_login_splash.png
  ```

## Apr 4th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- [] Children

  - [] Editable when SSID is nil, otherwise locked for editing because in SS
  - [x] Highlight in event list if no SSID

- [x] Invoices

  - [x] Need to be able to merge invoices by moving registrations from one to another
    - Should be set to in_ss and just merged, SMs will do it in the SS at the same time
    - Make sure you only get the option for valid merges

- [] Requests/Bugfixes
  - [] Sort out the invoice change formatting on event children so HTML tags are removed but newlines aren't
  - [x] 2nd row of headers for days on event children sticks too far up, it overlaps first header row
  - [x] Options weren't being deleted because I hardcoded the \_destroy value to be 0 on the confirm page
  - [x] I think copy_regs button fails when there isn't an invoice for the kid you're copying to yet, so maybe create one if it doesn't exists as part of the action
    - Was already doing that, problem was it wasn't saving because the total cost was nil
    - Resolved by creating a db default of 0 for that column

## Apr 5th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- CSV

  - [x] Decide on postgres-copy for CSV parsing since it uses PG's own COPY function
    - [] Install and set up the controller actions for import/export

## Apr 6th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- CSV

  - [x] Decide on postgres-copy for CSV parsing since it uses PG's own COPY function
    - [x] Set up the controller action for export
    - [] Set up the controller action for import

- Invoices

  - [] Staff should be able to edit if not in SS
    - [] If in SS, the space where edit should be should instead be filled by a mini form that allows in_ss to be toggled then replaces self with edit button (turboframe)
  - [] Needs to be an error if you try to copy regs to a closed time slot
  - [] Remove invoice numbers from parent view

- Time Slots

  - [] AMs can close time slots
    - still shows but says full
    - no need for automatic closing
  - [] Default registration deadline is 2pm the day before

- Events

  - [x] Remove the registration count from event partial/anywhere else

- Users

  - [x] Change Devise unlock method to time, we just wanna stop brute forcing anyway
  - [] Parents don't need to be associated to a school (I think)
    - Can just get the list of parents for a school through their children (distinct) **Friday**
  - [] User sign up form needs to remember names as well, do the same as you did for the user#edit form

- Requests/Bugfixes
  - [] Sort out the invoice change formatting on event children so HTML tags are removed but newlines aren't
  - [] Change seeds to only create arrival options if morning, afternoon if afternoon
  - [] Arrival only for morning, depart only or afternoon **On live**
  - [] Make options a check box, not a button **Friday**
  - [] Add names of registered time slots to a box on the price bar which expands up and down when clicked
  - [] Add some orphan children with 10 digit SSIDs for friday **On live**
  - [] Images on Events/time slots **On live**
    - [] Include pics of the price lists in the bundle and just direct link them **On live**

#### What I learned

- Some Bootstrap components need to be initialized on page load.
  - To do this, copy the initializer they provide on the component's page into application.js
  - But within an event listener on turbolinks load, like in my application.js now

## Apr 7th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- Children

  - [] Editable when SSID is nil, otherwise locked for editing because in SS
  - [] If child entered without SSID, staff can enter an SSID and find a child by that to merge
    - Moves the child to the parent
    - Moves all the info from the entered child to the SS imported one
    - Moves all invoices etc. from entered child to SS imported one
    - Needs to be a confirm page showing the kids to be merged cos SMs can't be trusted to enter the right number
  - [x] Photos OK should be an enum
    - [x] Has photos OK, my page ok and none ok
    - [x] Parents can edit photo status
      - [x] But parents can't select the my page ok
  - [x] Put first seasonal option in new child form
    - [x] If that's true and child is external, set needs hat to true
    - Show 1st seasonal if customer, just the hat checkbox if staff
    - Only show first seasonal if it's a new record as well
  - [x] Make allergies a select, not check box

- Users

  - [x] Parents don't need to be associated to a school (I think)
    - Can just get the list of parents for a school through their children (distinct)
  - [] User sign up form needs to remember names as well, do the same as you did for the user#edit form

- Requests/Bugfixes
  - [] Sort out the invoice change view formatting on event children so HTML tags are removed but newlines aren't
  - [x] Change seeds to only create arrival options if morning, afternoon if afternoon
  - [] Arrival only for morning, depart only or afternoon **On live**
  - [] Make options a check box, not a button
  - [] Add names of registered time slots to a box on the price bar which expands up and down when clicked
  - [] Add some orphan children with 10 digit SSIDs for friday **On live**
  - [] Images on Events/time slots **On live**
    - [] Include pics of the price lists in the bundle and just direct link them **On live**

## Apr 8th & 9th

Worked on the project setup instructions for Mike

## Apr 10th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- Events

  - [x] Re-enable event/slot creation by admins with new fields
    - [x] Add image uploads to Event and Time Slot forms
  - [x] Allow afternoon time slots to be created automatically from morning slots
  - [x] Add an option in the School select box to create the event for all schools

- Requests/Bugfixes
  - [x] Fix lack of User school causing issues with Event#index
  - [] Sort out the invoice change view formatting on event children so HTML tags are removed but newlines aren't
  - [] Arrival only for morning, depart only or afternoon **On live**
  - [] Make options a check box, not a button
  - [] Add names of registered time slots to a box on the price bar which expands up and down when clicked
  - [] Add some orphan children with 10 digit SSIDs for friday **On live**
  - [] Images on Events/time slots **On live**
    - [] Include pics of the price lists in the bundle and just direct link them **On live**

## Apr 11th

Too busy.
Did finally get an error for the S3 image upload though! It's the screenshot on my desktop. Successful one was POST, other was PATCH???

## Apr 12th

Too busy again, lunch was just getting info to Mike/Jack. Got file uploads (partially) working by remembering .yml is not a .rb

#### What I learned

- The inability to attach images was being caused by me trying to use ENV variables in a .yml file without declaring them as ruby syntax
  - Attaching images to events seems to work with smaller files, but not large ones
- Image ideas
  - Use [ListObjects](https://docs.aws.amazon.com/AmazonS3/latest/API/API_ListObjectsV2.html) to attach images from the S3 bucket manually in rails c
  - Search for images I upload with the app using the same logic I do when seeding locally (with active storage)
  - Image tag pointing at the S3 image [like this](https://stackoverflow.com/questions/7933458/how-to-format-a-url-to-get-a-file-from-amazon-s3)
  - Just have an image tag linking to the image in the assets folder, path generated from event/slot name
  - Read through the logs till you figure out why larger images fail silently

## Apr 13th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- Styling

  - [x] Login
  - [x] Signup
  - [x] Profile (user)
  - [x] Profile (child)
  - [x] Event index
  - [x] Child list for event
  - [x] Child list for time slot

- Requests/Bugfixes
  - [] Sort out the invoice change view formatting on event children so HTML tags are removed but newlines aren't
  - [x] Arrival only for morning, depart only or afternoon **On live**
  - [] Make options a check box, not a button
  - [] Add names of registered time slots to a box on the price bar which expands up and down when clicked
  - [x] Add some orphan children with 10 digit SSIDs for friday **On live**
  - [x] Images on Events/time slots **On live**
    - [x] Include pics of the price lists in the bundle and just direct link them **On live**
  - [x] Claim child tries to add parent's school, but that doesn't exist **Friday**
  - [] Staff shouldn't see option to add/claim child

#### What I learned

- 90% memory usage seems to be from when I SSH and mess around in the console, needs to hold a lot in memory when I do that
- Rather than using nested hashes, it's actually possible to set attributes in Rails helpers with 'aria-label': 'stuff' for example
- Add classes to the devise forms using html: { class: 'something' }

- Bootstrap

  - General

    - Rules after Bootstrap is imported in application.scss will override BS rules (because the BS ones are set with the default! flag)
    - To modify default CSS variables, set them like `$bg-color: white;`
      - Theme colors from maps can also be called as standalone variables
      - SASS variables need to be set outside a rule to be global, if inside a rule will only be accessible to that rule
      - If you wanna overwrite a SASS variable put it before the import, if you wanna overwrite a CSS variable put it after the import
    - Can add to map (groups of css values) by creating your own and merging it like

    ```
    // Create your own map
    $custom-colors: (
      "custom-color": #900
    );

    // Merge the maps
    $theme-colors: map-merge($theme-colors, $custom-colors);
    ```

    - Use tint-color(color, weight) to lighten, shade-color to darken
    - There's a color-contrast(color) function which returns a color which has at least the minimum contrast to the passed color
    - Use add() and subtract() rather than calc to avoid weird errors
    - Their components inherit from a base class and add modifiers as appropriate, try to stick to this when adding your own
    - BS variables are by default prefixed with bs- to differentiate from mine

  - Forms
    - You can add the 'disabled' attribute to a fieldset and it'll disable all the fields inside it, and style them appropriately
      - Similar for readonly, can add '.form-control-plaintext' to make them just display as plaintext without the input
    - Add text under inputs with the '.form-text' class on a div
      - Use 'aria-labelledby' or 'aria-describedby' on the input to link it to the text (using an id on the text div)
      - If you want the text in line, use a span etc.

- SASS
  - Lets you nest pseudo-selectors like
  ```
  .btn-ku {
    background: $ku-orange;
    color: $near-white;
    &:hover {
      background: $near-white;
      color: $ku-orange;
      border: 1px inset $ku-orange;
    }
  }
  ```

## Apr 16th

Set up the EB CLI on my home computer.

## Apr 17th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- AWS

  - [x] Terminated and re-created the staging environment
    - DO NOT delete the current version of the app from the S3 bucket -\_\_-

- CSV

  - [x] Set up the controller action for import

- Styling

  - [x] Styled the Child form (still overridden by the in place edit styling on the user page tho)

#### What I learned

- For some reason when applying a class to the select form helper, it needs to be in a hash and must be the 4th option passed

  - You can make it the 4th by making an empty hash the 3rd

- Don't delete any vaguely recent app versions from the S3 bucket, they might still be needed for rollback
  - Yeah really don't do this, it requires you to terminate the environment and just start again

## Apr 18th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- Children

  - [x] Editable when SSID is nil, otherwise locked for editing because in SS
  - [x] Should be able to print a list of kids attending from the page showing them
  - [x] If child entered without SSID, staff can enter an SSID and find a child by that to merge
    - [x] Also needs to update the child_id for each registration
    - Moves the ssid child to the parent
    - Moves all invoices etc. from entered child to SS imported one
    - Needs to be a confirm page showing the kids to be merged cos SMs can't be trusted to enter the right number
  - [x] Links to all time slots at the top of event children list
  - [x] Link to an index of the daily attendance sheets
    - [x] Style those
    - [x] Figure out how to only print the table the print button is associated with
  - [] Hide ele school from all, staff can enter pin to view sensitive info

- Styling

  - [x] User#form partial

- Tests

  - [x] Rewrite for new reality
    - [x] Child
    - [x] Invoice
    - [x] Misc changes caused by removing school from parents

- Users

  - [x] User sign up form needs to remember names as well, do the same as you did for the user#edit form
  - [] Hide address info and phone number once entered to sign up, staff can see by entering PIN
    - [x] Add a PIN column on the user table, we set for them
  - [] Redirect to P-up privacy policy and require acceptance before accessing app
  - [] SM can only log in from their school's IP address
    - Implement through an 'AllowedIPs' table
      - Name and IP fields on this table
    - Probably with a through table???
  - [] Timeout admin users after a while
  - [] On SM/AM profile
    - Show table for each event
      - Internal , reservations, external and total kids
      - Number of photobook sales
      - Total revenue from internal & reservation (sum of invoices)
      - Total revenue from external Ss
      - Total revenue for event
      - Goal revenue

- Requests/Bugfixes
  - [x] Stop displaying unnecessary afternoon info for special days
  - [x] Staff shouldn't see option to add/claim child
  - [] Parent children are not updated after redirect from merge child
  - [] Sort out the invoice change view formatting on event children so HTML tags are removed but newlines aren't (probably just open the full versions view in a new tab)
  - [] Stop printing the weird extra info on attendance sheets

#### What I learned

- Registrations need to belong to a child so I can validate that a child hasn't registered for the same thing twice

## Apr 19th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- Children

  - [x] Hide ele school from all, staff can enter pin to view

- Coupons

  - [x] Add somewhere to add a coupon during the invoice creation process
    - SMs will add the adjustment manually

- Events

  - [x] Make registrations a check box, not a button
    - [] Automatically uncheck all options for a time slot when that time slot is unchecked on the registration page (easy enough to do but more difficult to do in a way that updates the price)
  - [x] Add names of registered time slots to a box on the price bar
    - [x] Whose visibility can be toggled
  - [] Staff need a way to see/edit the same event show view customers do
    - Probably an 'Edit Invoice' button on invoices
  - [] Events need a revenue goal

- JS

  - [x] Modify conditional controller to by used for PIN reveal of sensitive info
  - [x] Rewrite large chunks of the price calculation logic to work with checkboxes

- Users

  - [x] Hide address info and phone number once entered to sign up, staff can see by entering PIN
  - [] Redirect to P-up privacy policy and require acceptance before accessing app
  - [] SM can only log in from their school's IP address
    - Implement through an 'AllowedIPs' table
      - Name and IP fields on this table
    - Probably with a through table???
  - [] Timeout admin users after a while
  - [] On SM/AM profile
    - Show table for each event
      - Internal , reservations, external and total kids
      - Number of photobook sales
      - Total revenue from internal & reservation (sum of invoices)
      - Total revenue from external Ss
      - Total revenue for event
      - Goal revenue

- Requests/Bugfixes
  - [] Parent children are not updated after redirect from merge child
  - [] Sort out the invoice change view formatting on event children so HTML tags are removed but newlines aren't (probably just open the full versions view in a new tab)
  - [] Stop printing the weird extra info on attendance sheets

#### What I learned

- Seems the leftover require tree comments in application.css cause some problems with asset compilation

  - Might just have been because my CSS used the login splash JPG and I hadn't retained it in the bundle through .gitignore
  - Removing the comment at the start of the file resulted in a successful deploy
  - Very possible the issues were all caused by me not updating the stuff I copy/paste into .gitignore to include the SVGs
    - They were in the CSS so tried to be bundled, but could't cos I left the PNG versions in, not SVG

- If you make a change that requires database changes, you'll need to rebuild the environment
  - Best to do that with an upload of a full, images included deploy so seeding is easier

## Apr 20th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- Events

  - [x] Make registrations a check box, not a button
    - [] Automatically uncheck all options for a time slot when that time slot is unchecked on the registration page (easy enough to do but more difficult to do in a way that updates the price)
    - Probably an 'Edit Registrations' button on invoices
  - [x] Events need a revenue goal

- Invoices

  - [x] Remove invoice numbers from summary
  - [x] Only apply hat adj if never applied before, not per event
  - [x] Group invoices by child, event in index
  - [x] Staff should be able to edit (same view as customers) if not in SS
    - [x] Replace with in_ss message if in SS, and disable merging from Invoices in SS
  - [x] Add previous versions to the #show view
    - [x] Allow resurrection of those versions
  - [x] Streamline logic for skipping slots already registered for in #copy_regs
  - [] Skip closed time slots (and their options) when copying registrations **DB change**

- Styling

  - [x] Basic Invoice styles
    - [x] Divs for each block of text, w/BS styles
    - [x] Switch partial to card class and tidy up from
    - [x] Redo heading sizes with knowledge they're not gonna be primary headings on page
    - [x] Make various small things I noticed readable
      - [x] Children index
      - [x] Customers index
      - [x] Schools index

- Users

  - [x] Show P-UP privacy policy in a modal on sign up page
  - [x] Require accepting P-UP privacy policy before accessing app
  - [] SM can only log in from their school's IP address **DB change**
    - Implement through an 'AllowedIPs' table
      - Name and IP fields on this table
    - Probably with a through table???
  - [x] Timeout admins/AMs after an hour
  - [x] Show event stats for each event at each school they manage. Cols are:
    - Internal , reservations, external and total kids
    - Number of photobook sales
    - Total revenue from internal & reservation (sum of invoices)
    - Total revenue from external Ss
    - Total revenue for event
    - [x] Goal revenue **DB change**
  - [x] Make the school list for AM/SMs actually readable

## Apr 21st

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- Authorisation

  - [x] Choose between Pundit and cancancan
    - Pundit, I like the way they organise their files more

- Children

  - [x] Katakana name must be present and katakana
  - [x] Allergies read only by default
  - [x] Photos select defaults to blank
  - [x] Have a link to their invoices on show page

- Events

  - [x] Make registrations a check box, not a button
    - [] Automatically uncheck all options for a time slot when that time slot is unchecked on the registration page (easy enough to do but more difficult to do in a way that updates the price)
  - [x] Partial links to sheet if in index, to child's regs if on child#show
  - Registered slots popup
    - [x] add AM/PM or date
    - [x] add total num of options registered
    - [x] sort alphabetically

- Invoices

  - [x] Skip closed time slots (and their options) when copying registrations
  - SM/AMs can
    - [x] add adjustments to invoices
    - [x] edit adjustments on invoices
  - [x] Change visible name to 'Bookings'
  - [x] prevent multiple siblings being registered for same event option in Invoice#calc_cost (just destroy it if siblings registered)
  - [x] Show tax in Invoice#summary
  - [x] Needs the weird number thing from the example Leroy had
  - [] Re-enable resurrection with the ability to restore registrations and adjustments for that version

- Options

  - Photo service is only necessary once per parent
    - [x] count them as registered if any sibling is on time slot attendance sheet
      - on event sheet
      - on time slot sheet

- Time Slots

  - [x] Create index
  - [x] Create partial
  - [x] Create show
  - [x] AMs (not SMs) can close time slots
    - [x] still shows but says full

- Users

  - [x] Katakana name must be present and katakana
  - [] SM can only log in from their school's IP address
    - [x] Implement through column on User table

- Requests/Bugfixes
  - [x] Start generating test data in JA again
  - [x] Stop showing children without relevant invoices on invoice#index

## Apr 22nd

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- Security

  - [x] Install Pundit
  - [] Set up authorisation for all controllers
    - [x] Adjustments
    - [x] Children
    - [x] CSVs
    - [x] Events
    - [x] Invoices
  - [] Remove model scopes/methods that aren't needed anymore now I have policy scopes

- Requests/Bugfixes

  - [] Invoice#index is empty for some users despite having invoices
  - [] Parent children are not updated after redirect from merge child
  - [] Sort out the invoice change view formatting on event children so HTML tags are removed but newlines aren't (probably just open the full versions view in a new tab)
  - [] Stop printing the weird extra info on attendance sheets
  - [] Resume printing table borders on attendance sheets

## Apr 23rd

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- Requests/Bugfixes

  - [x] Invoice#index is empty for some users despite having invoices
    - Event association was defined thru regs, not invoices

## Apr 24th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- Emails

  - [] When new invoice is confirmed **Requires domain**
    - [] Email SM saying it's been created with link to the invoice
    - [] Email parent with details and provisional price

- Price Lists

  - [x] Create controller
  - [x] Set up views for admins to manage price lists
    - [x] Index/partial
    - [x] Edit/new/form

- Security

  - [x] Set up authorisation for all controllers
    - [x] Options
    - [x] Price Lists
    - [x] TimeSlots
    - [x] User
  - [x] Remove unnecessary routes

## Apr 25th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

2-3 hour meeting w/Leroy

- Child

  - [x] Only show needs hat/received hat
  - [x] Allow SMs to edit on child#show if no SSID
  - [x] Allow staff to create children from index
  - [] Check for registrations on child being merged to and don't copy dups
    - [] Limit select for non ssid kid to kids with no ssid
    - [] Click no ssid (in event sheet) to go to merge page for that child
  - [] Make sure SSID link on index doesn't default to the path

- Events

  - [x] First toggle doesn't change price

- Invoices

  - [x] Add whodunnit to the past invoice versions
  - [x] Set the info to be displayed for each Invoice partial context
  - [x] Convert all my popups to BS modals
    - [x] Invoice summary and template
    - [x] Invoice changes
  - [] Back button on confirm page
  - [] See if you can show options on the confirm page
  - [] Event partial at the top of invoice index (show the pic)
  - [] Copy_regs is checking if options are closed again, stop it doing that
  - [] Add a button to partial to mark as in_ss

- Seeds

  - [x] New price lists
  - [x] Real schools
    - [x] SM accounts for each school
    - [x] 10 parents for each school
    - [x] 2 kids for each parent, registered for 10 random slots and 5 random options each at their school's event
    - [x] An unclaimed child for each school
      - [] Put in a spreadsheet we can show during the presentation (probably the one Leroy sent me w/emails)
  - [x] Seed the staging database
  - [] Use find_each with batch_size: 100 for seeds with a large number of records to maybe help RAM usage

- Users

  - [x] Allow staff to create customers from index
  - [] SM can only log in from their school's IP address **requires IP list**
  - [] When adding child there should be a back/close button for the TF
  - [] Only show time slot index for staff

- Requests/Bugfixes

  - [x] First registration added after navigating to event page doesn't register
  - [x] Sort out the invoice change view formatting on event children so HTML tags are removed but newlines aren't (probably just open the full versions view in a new tab)
  - [x] Stop printing the weird extra info on attendance sheets (this is an option on the browser print dialog)

## Apr 26th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- Child

  - [x] Make sure SSID link on index doesn't default to the path
  - [x] Add catch-all to enums for all the extra SS categories
  - [x] Reject kindy time options on attendance sheet

- Events

  - [x] Only show kindy times for kindy and ele times for ele
  - [x] Update JS to have 200yen dumb increase instead of 184yen
    - [x] And not apply to single regs

- Hosting

  - [x] Validate SES as email service
  - [x] Get AWS to issue an SSL cert for our domain

- Invoices

  - [x] Back button on confirm page
  - [x] Add invoices in SS to confirm page for context
  - [x] Event partial at the top of invoice index (show the pic)
  - [x] Add a button to invoice partial to mark as in_ss

- Options

  - [x] Timing options should default to なし if there isn't one registered
  - [x] Timing options need separate costs for kindy and elementary

- Seeds

  - [x] Real schools
    - [x] An unclaimed child for each school
      - [x] Put in a spreadsheet we can show during the presentation (probably the one Leroy sent me w/emails)

- Time Slots

  - [x] Don't need the show view, remove all links to it

- Users

  - [x] Merge Child
    - [x] Fix
      - [x] For in_ss kids with no registrations
      - [x] For in_ss kids with registrations
    - [x] No SSID on event sheet links to the merge child div for that child's parent, or their #show page if no parent
    - [x] Check for registrations on child being merged to and don't copy dups (use copy_regs?)
      - [x] Limit select for non ssid kid to kids with no ssid
    - [x] PIN to delete children, since I can't do that or invoices in the merge action
  - [x] When finding child there should be a back/close button for the TF
  - [x] Only show time slot index for staff

- Bugfixes

  - [x] Find child not working
    - Authorisation issue
  - [x] Copy regs not working
    - Was checking if options are closed. They can't be.
  - [x] Long-running registration error w/multiple invoices
    - Regs were being added to a random invoice (sometimes the in_ss one) as there were multiple opt/slot targets
    - This led to those regs not being passed to the confirm page, or update action, as invoices in SS aren't updated
    - Stopped rendering the targets on invoices in the SS

#### What I learned

- You can link back with a link_to that's passed :back as the url
- And link to an anchor (by its id) on another page by passing the anchor: param to a url helper

## Apr 27th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- Styling

  - [x] The damn flash message
    - Using BS toasts now
  - [x] Responsive navbar
  - [x] Event sheet
  - [x] Slot attendance sheet
  - [x] Login fixes for mobile
  - [x] Customer profile
  - [x] Child profile
  - [] Event#show
    - [x] Migrate basic layout to BS to avoid conflicts
    - [x] Header section
    - [x] More info
    - [x] Accordion
    - [x] Registered/Unregistered slots
    - [x] Price bar
      - Probably have a collapse that toggles everything except the price, like a view details button before they register
      - Could also show the register button, but have the collapse toggle the coupon field as well
  - [] Login page (desktop)

- Seeds

  - [x] Use find_each with batch_size: 100 for seeds with a large number of records to maybe help RAM usage
  - [x] Re-seed the test DB with new option names

- Bugfixes

  - [x] Event child needs active invoice to exist
    - Added a check that such an invoice does exist before rendering the changes cell, if it doesn't just renders an empty cell
  - [x] Child deletion logic
    - Legacy button for admins on parent page was using legacy code that was unnecessary and not be authorised properly
    - Cleaned up so kids can only be deleted by staff if no SSID, from their own page

## Apr 28th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- Hosting

  - [x] Troubleshoot domain not working
    - spent an ungodly amount of time on this, literal hours of just reading docs/thinking of ways to approach it
    - seems .app forces SSL, and I'm not set up for that yet
    - test.kids-up is now getting incorrect cert errors, which is an improvement
      - will try explicitly adding to new cert
    - but the main domain just times out over and over, it should be working
    - tried a whole bunch of things I didn't document cos too tired/frustrated, but eventually worked my way through to the ports on the load balancer
    - figured out I needed it earlier in the day, but had left instance port on default, same as incoming for HTTPs
    - it needed to be port 80 on the instance, and using HTTP
  - [x] Set up for SSL
    - Created a load balancer listening on port 443 for HTTPS requests, using our certificate
      - 1st time forgot the wildcard
      - 2nd time wildcard didn't work
  - [] Write a proper application to get out of email sandbox
  - [] Set up dev environment

- Localisation

  - [x] Login
  - [x] Signup
  - [x] User profile
  - [x] Child form
  - [x] Event#show
  - [x] Invoice partial
  - [x] Child profile
  - [x] Attendance sheets
  - [x] Misc Yuna changes later in the day

- Styling

  - [x] Accordion on event attendance sheet
  - [] Login page (desktop)

## Apr 29th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- Children

  - [x] Added toggle buttons for staff to set if a child has their hat or changes their photo permission

- Invoices

  - [x] Handle lack of invoice when going back thru confirm page more gracefully
