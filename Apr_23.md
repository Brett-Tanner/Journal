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
  /app/assets/images/*
  !/app/assets/images/favicon.png
  !/app/assets/images/logo.png
  !/app/assets/images/white_logo.png
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

## Apr 14th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- CSV

  - [] Set up the controller action for import

- Children

  - [] Editable when SSID is nil, otherwise locked for editing because in SS
  - [] If child entered without SSID, staff can enter an SSID and find a child by that to merge
    - Moves the child to the parent
    - Moves all the info from the entered child to the SS imported one
    - Moves all invoices etc. from entered child to SS imported one
    - Needs to be a confirm page showing the kids to be merged cos SMs can't be trusted to enter the right number
  - [] Should be able to print a list of kids attending from the page showing them

- Coupons

  - [] Add somewhere to add a coupon during the invoice creation process
    - SMs will add the adjustment manually

- Emails

  - [] When new invoice is confirmed
    - Email SM saying it's been created with link to the invoice
    - Email parent with details and provisional price

- Invoices

  - [] Staff should be able to edit if not in SS
    - [] If in SS, the space where edit should be should instead be filled by a mini form that allows in_ss to be toggled then replaces self with edit button (turboframe)
  - [] Needs to be an error if you try to copy regs to a closed time slot
  - [] Remove invoice numbers from parent view

- Options

  - [] Photo service is only necessary once per parent
    - Need to somehow register all other children for it, maybe do so then apply an adjustment to their invoices reducing the cost by photo service cost
    - And reverse on delete
    - Probably a callback when that type of option is created/destroyed?

- Time Slots

  - [] AMs can close time slots
    - still shows but says full
    - no need for automatic closing
  - [] Default registration deadline is 2pm the day before

- Users

  - [] User sign up form needs to remember names as well, do the same as you did for the user#edit form

- Requests/Bugfixes
  - [] Sort out the invoice change view formatting on event children so HTML tags are removed but newlines aren't
  - [] Make options a check box, not a button
  - [] Add names of registered time slots to a box on the price bar which expands up and down when clicked
  - [] Staff shouldn't see option to add/claim child

#### What I learned

-
