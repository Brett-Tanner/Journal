# March 2023

## Mar 1st

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- [] Event_children/time_slot_children rework

  - [] Event children
    - [x] Change overall layout to use a table
    - [x] Get the sticky headers working properly
    - [x] Display all the necessary info
    - [] Add the cost breakdown popup
    - [] Build out the functionality to send a confirmation email from the table
  - [] For time slot children, should just look exactly like the printable one

- Bugfixes/Requested Features
  - [] From Event#index, just put the link to Child#index on the pic for staff rather than the link to Event#show
  - [] Add repeated discount to Invoice#calc_cost (probably as an adjustment?)

## Mar 2nd

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- [x] Event booking rework

  - [x] Use current invoice if it exists/is not closed, otherwise use a new invoice
    - [x] So have an @invoices, not just one. Set the desired invoice through params
    - [x] Grey out slots if registered for in previous invoice
    - [x] Put a link to that invoice on greyed out slots (separate for each child)
  - [x] Make early arrival/departure options mutually exclusive (radio buttons rather than buttons???)
    - [x] Works if already registered for one of the options
    - [x] Works if not already registered for either option

- [] Event_children/time_slot_children rework

  - [] Event children
    - [x] Add the cost breakdown popup
    - [] Build out the functionality to send a confirmation email from the table
  - [x] For time slot children, should just look exactly like the printable one
    - [x] Display the necessary information
    - [x] Style the table and implement sticky headers like on event_children

- Bugfixes/Requested Features
  - [x] From Event#index, just put the link to Child#index on the pic for staff rather than the link to Event#show
  - [] Add repeater discount to Invoice#calc_cost (probably as an adjustment?)
  - [x] Add an 'on time' option with 0 offset and cost since I'm doing radio buttons for arrival/departure times

## Mar 6th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

Was stuck at Mizonokuchi, just laid some groundwork for AWS

#### What I learned

- New, more optimised zip command for uploading source bundles to AWS

```
zip -r db_prototype_v2.zip db_prototype_v2 -x * .[^.]* "db_prototype_v2/storage/*" "db_prototype_v2/tmp/*" "db_prototype_v2/log/*"
```

## Mar 7th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- [] AWS

  - [x] Installed EB CLI
    - Attempted to use it to create the EB, failed because it got stuck on creating the source bundle
  - [x] Updated Ruby to 3.0.5 to match AWS platform version

    - Issue is now pg gem failing to install for some reason

    ```
    An error occurred while installing pg (1.4.5), and Bundler cannot continue.

    In Gemfile:
      pg
    ```

#### What I learned

- AWS EB doesn't like zip files produced on a Mac, so use git archive instead (and probably a prod branch to exclude dev stuff)
  - hence new command to generate a source is this from the project folder
  ```
  git archive -v -o db_prototype_v2.zip --format=zip HEAD
  ```

## Mar 8th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- [] AWS

  - [x] Successfully SSH into the EC2 instance!
  - [x] Resolved the issue with pg gem being installed
  - [x] Resolved issues with Bundler and puma versions not matching those on the AWS platform
    - Issue now seems to be puma constantly failing to start due to being able to load some 'indifferent_hash.rb' file
      - Stayed up way too fucking late trying to figure this out, still have no idea.It's 3:20am, what the fuck am I doing
        - Leaving puma out of gemfile produces same error (cos it's the same version by default)
        - Reverting to the original version (5) leads to it terminating as soon as it calls require rather than making it to the folder, which is different at least
        - I hate this, I'm going to sleep

- [] Add Invoices
  - [] Need to be able to merge invoices by moving registrations from one to another
  - [] Need a request change button on the old, paid invoices
  - [] Children are NOT ON THE SAME INVOICE, separate invoices for each child
    - [] Toggle between kids where the invoice toggle is now
      - [] On price bar
      - [] Preserve scroll position
    - [] Button to copy kid's registrations from one kid to to another (separate controller for this)
  - [] No switching between invoices, just display them all at once and have total for all
  - [] Have a confirmation screen before invoice is finalised showing full details
    - Can I do that with Invoice #new? does it create #new regs????

#### What I learned

- The pg gem couldn't be installed because EC2 instances come with a hilariously outdated version of PG installed, and the gem needs a supported version of PG installed

  - In the future will install a newer version of PG through .ebextensions/packages.config during instance initialization [like here](https://stackoverflow.com/questions/61148791/postgresql-on-elastic-beanstalk-amazon-linux-2/63204453#63204453)
  - For now will try to SSH in and install it manually/check what versions are available for the config file in future
  - Shouldn't I be able to just have it connect to the RDS tho???

- Just generate a new keypair for SSH into the instance, it needs to be in your .ssh folder as a .pem

- To get to the app on the EC2 instance, go to the home directory then cd into /var/app/current

  - You don't have write permissions for a whole bunch of stuff though [per this](https://stackoverflow.com/questions/27611608/ec2-user-permissions), so mostly for looking around

- You can use 'tail -f' on a file to view changes as they're made (in shell)
- And cat to read the file

## Mar 9th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- [] AWS

  - Look into alternatives to EB since that's determined to not work
    - [] Manually setting up an EC2/other associated resources
    - [] Deploying with Docker
    - [] Engineyard/other hosting options (will need to be cheaper or clearly better in other ways and same price)

- [] Invoices

  - Children are NOT ON THE SAME INVOICE, separate invoices for each child
    - [] Redo calculation logic with this knowledge
      - [x] Model logic
      - [] JS logic
    - [] Views - [x] Basic layout/contents - [] Submit multiple invoices together - [x] Show all invoices for a child together, cumulative total at the bottom - [x] Toggle between kids where the invoice toggle is now - [] Preserve scroll position
      - [] Don't block the whole day when in SS/on previous invoice, just the stuff that's registered
        - [] When in SS, grey out the individual slot/option and have contact info at top
        - [] Can still add new options/regs tho
      - [] Have a warning for afternoons on regular days with a message saying they're already going
    - [] Button to register your other kid for the same stuff as your first kid (separate controller for this)
  - [] In calculation
    - [] external students who have at least the 10 course and have attended a seasonal event before get 10k discount
    - [] add hat option if they need a hat
  - [] Have a confirmation screen before invoice is finalised showing full details
    - #new creates new nested records as well and they can be used in calcs without saving them
      - So when they're done they click a 'confirm details' button which takes them to the Invoice#new page
        - With the details prefilled as what they selected on the event page (hidden though)
        - And summary/total cost displayed as calculated on the backend
        - They can then submit the hidden details and actually create the invoice/registrations with a 'create registrations' button
        - Takes them to Invoice#show
  - [] Need to be able to merge invoices by moving registrations from one to another

- [] Event children

  - [] Live update or timed refresh so SMs are notified when changes are made even with window open
    - Refresh timer on activity
  - [] Datetime for seen at by SM
    - [] auto set to nil on creation
    - [] button to update to current time when SM has seen it (put this in the change list popup so they actually have to open it)
    - [] separate col in event children table to show changes since last seen
      - should be able to do this using paper trail, no DB change needed
      - get all changes since the seen_at column and show the diffs
  - [] Remove send email and replace with email template (backed by DB col)
  - [] Add arrival and departure times (not just on time slot sheet)
  - [] List billing dates per invoice next to the invoice id
  - [] Put the Kanji/lack thereof to show options
  - [] List the coupons so SM can apply

- [] Time Slot children

  - [] In general should include all info for afternoon slot as well (options, attendance etc.)
  - [] Add columns to show if they're coming in morning/afternoon or both
    - [] Tally for AM/PM attendance like the main attendance col
  - [] Add column to show if photo service is selected for the event
  - [] Change arr/dept time to only display something if option selected, and include the afternoon slot
  - [] If option is not selected/arrival/depart is not changed just leave it blank

- Time Slots

  - Some are priced differently, have a proper think about how to handle those
    - Col with modifiers??
  - [] Render special days first on the event children list with different cols

- [] Emails
  - [] When new invoice is confirmed
    - Email SM saying it's been created with link to the invoice
    - Email parent with details and provisional price
- [] Coupons
  - [] Add somewhere to add a coupon during the invoice creation process
    - SMs will add the adjustment manually
- [] Events
  - [] Need seasonal and single day to be separate types

#### What I learned

- Very long meeting with Leroy which once again will surely result in no more major changes -\_\_-
- You can batch update records using a separate controller + fields_for as described [here](https://stackoverflow.com/questions/41902942/rails-how-to-submit-multiple-forms-to-the-same-table) and [here](https://stackoverflow.com/questions/34557033/rails-submitting-multiple-forms-with-one-submit-button)
  - Can hopefully use that to not have a mess of submit buttons on the price bar

## Mar 10th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- [] Invoices

  - Children are NOT ON THE SAME INVOICE, separate invoices for each child
    - [x] Redo calculation logic with this knowledge
      - [x] JS logic
    - [] Views
      - [] Submit multiple invoices together
        - [] Make sure JS is adding regs to correct invoice
          - If already on invoice, should just add or remove from that one
          - If an invoice is closed, should only be able to add
      - [] Don't block the whole day when in SS/on previous invoice, just the stuff that's registered
        - [] When in SS, grey out the individual slot/option and have contact info at top
        - [] Can still add new options/regs tho
      - [] Have a warning for afternoons on regular days with a message saying they're already going
    - [] Button to register your other kid for the same stuff as your first kid (separate controller for this)
  - [] In calculation
    - [] external students who have at least the 10 course and have attended a seasonal event before get 10k discount
    - [] add hat option if they need a hat
    - [] Add the 184 yen to the JS calculation
  - [] Have a confirmation screen before invoice is finalised showing full details
    - #new creates new nested records as well and they can be used in calcs without saving them
      - So when they're done they click a 'confirm details' button which takes them to the Invoice#new page
        - With the details prefilled as what they selected on the event page (hidden though)
        - And summary/total cost displayed as calculated on the backend
        - They can then submit the hidden details and actually create the invoice/registrations with a 'create registrations' button
        - Takes them to Invoice#show
  - [] Need to be able to merge invoices by moving registrations from one to another

- [] Requests/Bugfixes
  - [] Preserve scroll position on Event#show when switching between children
  - [] Unsure which invoice JS puts the new regs on rn, will need to look into controlling that if it turns out we do need multiple invoices per event

## Mar 11th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- [] Invoices

  - [x] In calculation
    - [x] External students who have at least the 10 course and have attended a seasonal event before get 10k discount
    - [x] Add hat option if they need a hat
    - [x] Add the 184 yen to the JS calculation

- [] Event children

  - [] Datetime for seen at by SM
    - [x] auto set to nil on creation

- [] Time Slot children
  - [x] Add column to show if photo service is selected for the event
  - [x] Change arr/dept time to only display something if option selected
  - [x] Leave options blank unless selected/different from default

## Mar 12th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- [] Event children
  - [x] Remove send email and replace with email template (backed by DB col)
  - [x] List billing dates per invoice next to the invoice id
  - [] Live update or timed refresh so SMs are notified when changes are made even with window open
    - Refresh timer on activity
  - [] Datetime for seen at by SM
    - [] button to update to current time when SM has seen it (put this in the change list popup so they actually have to open it)
    - [] separate col in event children table to show changes since last seen
      - should be able to do this using paper trail, no DB change needed
      - get all changes since the seen_at column and show the diffs
  - [] Add arrival and departure times (not just on time slot sheet)
  - [] Render special days first on the event children list with different cols
  - [] Put the Kanji/lack thereof to show options
  - [] List the coupons so SM can apply

## Mar 13th

- Sick & stuck at Mizonokuchi

## Mar 14th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- [] Invoices

  - Children are NOT ON THE SAME INVOICE, separate invoices for each child
    - [] Views
      - [] Submit multiple invoices together
        - [] Make sure JS is adding regs to correct invoice
          - If already on invoice, should just add or remove from that one
          - If an invoice is closed, should only be able to add
      - [x] Don't block the whole day when in SS/on previous invoice, just the stuff that's registered
        - [x] When in SS, grey out the individual slot/option and have contact info at top
        - [x] Can still add new options/regs tho
      - [] Have a warning for afternoons on regular days with a message saying they're already going
    - [] Button to register your other kid for the same stuff as your first kid (separate controller for this)
  - [] Have a confirmation screen before invoice is finalised showing full details
    - #new creates new nested records as well and they can be used in calcs without saving them
      - So when they're done they click a 'confirm details' button which takes them to the Invoice#new page
        - With the details prefilled as what they selected on the event page (hidden though)
        - And summary/total cost displayed as calculated on the backend
        - They can then submit the hidden details and actually create the invoice/registrations with a 'create registrations' button
        - Takes them to Invoice#show
  - [] Need to be able to merge invoices by moving registrations from one to another

- [] Requests/Bugfixes
  - [x] Make hat and repeater adjustments actual adjustments rather than just part of the calculation for easier manipulation
  - [x] Create an invoice rather than instantiating new one without saving when @all_invoices is empty to make an id available
  - [] Preserve scroll position on Event#show when switching between children
  - [] Unsure which invoice JS puts the new regs on rn, will need to look into controlling that if it turns out we do need multiple invoices per event

## Mar 15th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- [] Requests/Bugfixes
  - [x] 500yen bug in customer event invoices
    - When I moved the repeater and hat adjustments to being actual adjustments I didn't do the same for the JS, so the hat cost was being repeated
  - [] Preserve scroll position on Event#show when switching between children
  - [] Unsure which invoice JS puts the new regs on rn, will need to look into controlling that if it turns out we do need multiple invoices per event

#### What I learned

- Every time I run a db:reset the storage folder gets a whole new set of blobs, so it's been steadily increasing this whole time. Just deleting the folder before doing another reset is fine

## Mar 16th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- [] Invoices

  - [] Views

    - [x] If all invoices are in SS, create a new invoice on Event#show load to add any further registrations
    - [x] Make sure JS is adding regs to correct invoice, and handling calculations for all invoices correctly
    - [] Have a warning for afternoons on regular days with a message saying they're already going
    - [] Button to register your other kid for the same stuff as your first kid (separate controller for this)

  - [] Have a confirmation screen before invoice is finalised showing full details
    - #new creates new nested records as well and they can be used in calcs without saving them
      - So when they're done they click a 'confirm details' button which takes them to the Invoice#new page
        - With the details prefilled as what they selected on the event page (hidden though)
        - And summary/total cost displayed as calculated on the backend
        - They can then submit the hidden details and actually create the invoice/registrations with a 'create registrations' button
        - Takes them to Invoice#show
  - [] Need to be able to merge invoices by moving registrations from one to another

- [] Event children
  - [x] Put the Kanji/lack thereof to show options
  - [x] Add arrival and departure times (not just on time slot sheet)
  - [] Live update or timed refresh so SMs are notified when changes are made even with window open
    - Refresh timer on activity
  - [] Datetime for seen at by SM
    - [] button to update to current time when SM has seen it (put this in the change list popup so they actually have to open it)
    - [] separate col in event children table to show changes since last seen
      - should be able to do this using paper trail, no DB change needed
      - get all changes since the seen_at column and show the diffs
  - [] Render special days first on the event children list with different cols
  - [] List the coupons so SM can apply

## Mar 17th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- [] Invoices

  - [] Views

    - [x] Have a warning for afternoons on regular days with a message saying they're already going
    - [] Button to register your other kid for the same stuff as your first kid (separate controller for this)

## Mar 20th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- [] AWS

  - Look into alternatives to EB since that's determined to not work
    - [] Manually setting up an EC2/other associated resources
      - [YT Walkthrough](https://www.youtube.com/watch?app=desktop&v=E2o2u7Rc0h0)
    - [] Deploying with Docker

- [] Invoices

  - [x] Views

    - [x] Button to register your other kid for the same stuff as your first kid (separate controller for this)

  - [x] Have a confirmation screen before invoice is finalised showing full details
    - #new creates new nested records as well and they can be used in calcs without saving them
      - So when they're done they click a 'confirm details' button which takes them to the Invoice#new page
        - With the details prefilled as what they selected on the event page (hidden though)
        - And summary/total cost displayed as calculated on the backend
        - They can then submit the hidden details and actually create the invoice/registrations with a 'create registrations' button
        - Takes them to Invoice#index
  - [] Need to be able to merge invoices by moving registrations from one to another

## Mar 21st

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- [] Invoices

  - [x] Confirmation page correctly decreases price when registrations are deleted
  - [] Need to be able to merge invoices by moving registrations from one to another

- [] Requests/Bugfixes
  - [] Preserve scroll position on Event#show when switching between children
  - [] Unsure which invoice JS puts the new regs on rn, will need to look into controlling that if it turns out we do need multiple invoices per event
  - [] Make allergies on the add child form a select box between yes/no
  - [x] Need a note on the Invoice#index page that price will likely decrease when merged later

## Mar 22nd

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- [] Event children

  - [] Live update or timed refresh so SMs are notified when changes are made even with window open
    - Refresh timer on activity
  - [x] Datetime for seen at by SM
    - [x] button to update to current time when SM has seen it (put this in the change list popup so they actually have to open it)
    - [x] separate col in event children table to show changes since last seen
  - [x] Render special days first on the event children list with different cols
    - [x] Add categories to time slots
    - [x] Render the special days first
    - [x] Add their unique info
  - [] List the coupons so SM can apply

- [] Requests/Bugfixes
  - [x] Wrote a guide for anyone who ends up translating for the app
    - [] Update to reflect the fact we're using codespaces
    - [] Set up codespaces so translators can run a version of the app with their changes using rails s
      - Create an issue to track the translations, from that issue create a branch
      - Delete the current one and set it up on translation branch
  - [] Sort out the invoice change formatting on event children so HTML tags are removed but newlines aren't
  - [] Also look into the performance impact of making each row a turbo frame (or maybe just the col??) so marking it as seen removes the button
  - [] Preserve scroll position on Event#show when switching between children
  - [] Make allergies on the add child form a select box between yes/no

## Mar 23rd

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- [x] Event children

  - [x] Remove the view changes button once invoice changes are viewed
  - [x] Add blank cells when special not registered
  - [x] Move extension option out of col with lunch and into middle of arrival/dept
  - [x] Timed refresh so SMs are notified when changes are made even with window open
    - [x] Refresh timer on activity
    - [x] Add countdown
  - [x] List the coupons so SM can apply

- [x] Time Slot children

  - [x] Include all info for afternoon slot as well (options, attendance etc.)
  - [x] Add columns to show if they're coming in morning/afternoon or both
    - [x] Tally for AM/PM attendance like the main attendance col

- Time Slots

  - [x] Add a category col for special, seasonal, party time slots so they can be sorted
  - [] AMs can close time slots
    - still shows but says full
    - no need for automatic closing
  - [] Default registration deadline is 2pm the day before

- [] Children

  - [] Add column for grade at school
  - [x] Single name column for kids/adults
    - [] But in forms, get separately then combine with japanese space
  - [] Single columns for allergies
    - [] Allergies are a required field
    - [] Form default is blank, there's a greyed select box which when toggled to no changes the input to なし (user can't alter), toggled to yes makes editable

## Mar 24th

Busy day & tired

## Mar 25th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- [] Requests/Bugfixes
  - [x] Replace ✓ with ◯
  - [x] Display NG if photos_ok false, otherwise blank
  - [x] Figure out why kids are having 12 invoices created by seeds, not 4 (probably making one for each school/event rather than being limited)
  - [x] Time slot children should have katakana name, not kanji
  - [x] Check the option counting on time slot children
    - Seeds was creating two registrations to the same option for each child/invoice because meals were included in the regular scope for options
      - [x] Fix regular scope
      - [] Add a validation to ensure registerable ids are unique per child and registerable type
  - [] Sort out the invoice change formatting on event children so HTML tags are removed but newlines aren't

## Mar 27th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- [] Children

  - [] Add column for grade at school
    - Kindy:
      - 満１歳
      - 満２歳
      - 年々少
      - 年少
      - 年中
      - 年長
    - Ele:
      - 小１
      - 小２
      - 小３
      - 小４
      - 小５
      - 小６
      - 中学１年
      - 中学２年
    - Only the last 3 of kindy and 小 for elementary in form selection boxes
  - [x] Single name column for kids/adults
    - [x] But in forms, get separately then combine with japanese space
    - [x] Katakana name too - [] Single columns for allergies
  - [] Allergies are a required field
  - [] Form default is blank, there's a greyed select box which when toggled to no changes the input to なし (user can't alter), toggled to yes makes editable

- [] Requests/Bugfixes
  - [x] Check the option counting on time slot children
    - Seeds was creating two registrations to the same option for each child/invoice because meals were included in the regular scope for options
      - [x] Add a validation to ensure registerable ids are unique per child and registerable type
  - [] Sort out the invoice change formatting on event children so HTML tags are removed but newlines aren't

#### What I learned

- Once again, lifecycle callbacks are very useful
  - Rather than dealing with strong params in the controller, I just allowed the separate names then used them with attr_accessor to set full name in a before_validation callback

## Mar 28th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- [] Children

  - [x] Add column for grade at school
    - Kindy:
      - 満１歳
      - 満２歳
      - 年々少
      - 年少
      - 年中
      - 年長
    - Ele:
      - 小１
      - 小２
      - 小３
      - 小４
      - 小５
      - 小６
      - 中学１年
      - 中学２年
    - [] Only the last 3 of kindy and 小 for elementary in form selection boxes
  - [x] Single columns for allergies
    - [] Allergies are a required field
    - [] Form default is blank, there's a greyed select box which when toggled to no changes the input to なし (user can't alter), toggled to yes makes editable

- [] Requests/Bugfixes
  - [x] Fix seeds file for the new way to set single name/kana name from combo of first/last
    - [x] Add a conditional to stop errors when manually modifying names
  - [x] Display first and last names in fields when editing a user/child
  - [] Sort out the invoice change formatting on event children so HTML tags are removed but newlines aren't

## Mar 29th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- [] AWS

  - Look into alternatives to EB since that's determined to not work
    - [] Manually setting up an EC2/other associated resources
      - [YT Walkthrough](https://www.youtube.com/watch?app=desktop&v=E2o2u7Rc0h0)
    - [] Deploying with Docker

- [] Invoices

  - [] Need to be able to merge invoices by moving registrations from one to another
    - Should be set to in_ss and just merged, SMs will do it in the SS at the same time
    - Make sure you only get the option for valid merges

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

- [x] Children

  - [x] Add column for grade at school
    - Kindy:
      - 満１歳
      - 満２歳
      - 年々少
      - 年少
      - 年中
      - 年長
    - Ele:
      - 小１
      - 小２
      - 小３
      - 小４
      - 小５
      - 小６
      - 中学１年
      - 中学２年
    - [x] Only the last 3 of kindy and 小 for elementary in form selection boxes
  - [x] Single columns for allergies
    - [x] Form default is blank, there's a greyed text field which when check box toggled to no changes the input to なし (user can't alter), toggled to yes makes editable

- [] Requests/Bugfixes
  - [] Sort out the invoice change formatting on event children so HTML tags are removed but newlines aren't

## Mar 30th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- [] AWS

  - Look into alternatives to EB since that's determined to not work

    - [x] Get the Elastic Beanstalk up and running!!
      - [x] Get the database seeded
      - [] Figure out what's causing the render error when you log in

#### What I learned

- Edit Rails credentials with `EDITOR="code --wait" bin/rails credentials:edit`
  - View them with `Rails.application.credentials`
- View locally saved AWS credentials with `code ~/.aws/credentials`
- Use 'logout', not 'exit' to close eb ssh sessions
- Finally tracked down the issue with mail not being readable, it's a [known issue](https://github.com/mikel/mail/issues/1489) with version 2.8.0
  - Path to the problem folder is '/var/app/current/vendor/bundle/ruby/3.0.0/gems/mail-2.8.0/lib/mail/'
  - Can be (seemingly) fixed by locking 'mail' to 2.7.1 in gemfile
- But now it's trying to load Faker in production for some reason
  - I was loading it in an initializer to set the locale to JA, removed initializer
- This opens the console in an SSH session `RAILS_ENV=production bundle exec rails c`
- `/var/app/containerfiles/logs/production.log` Is the path for puma output
- Currently stuck on this error

```
ActionView::Template::Error (undefined method `persisted?' for nil:NilClass):
    18: <% else %>
    19:
    20:     <div class="event">
    21:         <%= (link_to image_tag(url_for(event.image)), event_path(id: event, child: current_user.children.first.id)) unless event.image.nil? %>
    22:
    23:         <h2><%= link_to event.description, event_path(id: event, child: current_user.children.first.id) %></h2>
    24:

app/views/events/_event.html.erb:21
app/views/users/show.html.erb:53
```

## Mar 31st

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

Busy day @school, also discovered the issue with nested attributes and spent some time looking at that/figuring out what was happening

- [] AWS

  - Look into alternatives to EB since that's determined to not work

    - [x] Get the Elastic Beanstalk up and running!!
      - [x] Get the database seeded
      - [x] Figure out what's causing the render error when you log in
        - Needed to use #blank? for checking image attachments rather than #image.nil?
