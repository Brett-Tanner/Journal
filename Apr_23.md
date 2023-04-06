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

- CSV

  - [] Set up the controller action for import

- Children

  - [] Editable when SSID is nil, otherwise locked for editing because in SS
  - [] If child entered without SSID, staff can enter an SSID and find a child by that to merge
    - Moves the child to the parent
    - Moves all the info from the entered child to the SS imported one
    - Moves all invoices etc. from entered child to SS imported one
    - Needs to be a confirm page showing the kids to be merged cos SMs can't be trusted to enter the right number
  - [] Photos OK should be an enum **Friday**
    - [] Parents can edit photo status **Friday**
    - Has photos OK, my page ok and none ok
    - But parents can't select the my page ok
  - [] Put first seasonal option in new child form **Friday**
    - If that's true and child is external, set needs hat to true **Friday**

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

- Emails

  - [] When new invoice is confirmed
    - Email SM saying it's been created with link to the invoice
    - Email parent with details and provisional price

- Coupons

  - [] Add somewhere to add a coupon during the invoice creation process
    - SMs will add the adjustment manually

- Options

  - [] Photo service is only necessary once per parent
    - Need to somehow register all other children for it, maybe do so then apply an adjustment to their invoices reducing the cost by photo service cost
    - And reverse on delete
    - Probably a callback when that type of option is created/destroyed?

- Users

  - [] Parents don't need to be associated to a school (I think) **On this one rn, fixing seeds for no parent school**
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

-
