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

- [] Children

  - [] Editable when SSID is nil, otherwise locked for editing because in SS

- Time Slots

  - [] AMs can close time slots
    - still shows but says full
    - no need for automatic closing
  - [] Default registration deadline is 2pm the day before

- [] Emails

  - [] When new invoice is confirmed
    - Email SM saying it's been created with link to the invoice
    - Email parent with details and provisional price

- [] Coupons

  - [] Add somewhere to add a coupon during the invoice creation process
    - SMs will add the adjustment manually

- [] Options

  - [] Photo service is only necessary once per parent
    - Need to somehow register all other children for it, maybe do so then apply an adjustment to their invoices reducing the cost by photo service cost
    - And reverse on delete
    - Probably a callback when that type of option is created/destroyed?

- [] Requests/Bugfixes
  - [] Sort out the invoice change formatting on event children so HTML tags are removed but newlines aren't

#### What I learned

-
