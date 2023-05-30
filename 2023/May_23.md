# May 2023

## May 1st

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- Children

  - [x] Allow staff to set child parent from the parents at their school if they don't have one

- Emails

  - [x] Write a proper application to get out of email sandbox

    - How often we send
      - 3 000 registrations per event, 3 times a year
      - So first time will be at least 6 000 (confirmations for new accounts)
      - May also be more from edits, but hasn't previously been available so unsure of numbers
    - How we manage recipient lists
      - Based on my understanding of recipient lists, we don't use them. Each email goes to only two recipients, the customer who took the action and the SM of their school
    - Details of the app
    - Bounces
      - Will have an SNS notification set up to notify an admin if emails bounce
      - They then notify the SM, who will contact the parent to confirm their email address is correct
    - Complaints
      - Set them as unsubscribed for all email types in the database
    - Unsubscribe requests
      - Link in the email allows them to unsubscribe from emails based on type (e.g. create or update bookings)
      - Backed by table in database for email preferences
    - Examples of the emails we send

      - Confirmation

      ```
      Welcome (user name)-さん,

      以下のリンクからアカウントのメールを確認できます。

      アカウントを確認する(link to confirm account)
      ```

      - After booking is made

      ```
      (Parent name)

      この度はKids UPウィンタースクール2022にお申込みいただき誠にありがとうございます。

      (Student name)様のお申込み内容は下記の通りとなります。

      (Link to view their booking on the site)

      ご参加希望スクール名：KidsUP(school name)

      ご参加希望日・オプション：

      12月26日・月:   午前 | - | - | -


      お申込み金額（内訳）:

      スポット1回（午前・15:00~18:30） x 1: 4216円
      スポット1回（13:30~18:30） x 0: 0円
      スペシャルデー x 0: 0円
      延長 x 0コマ: 0円
      おやつ x 0: 0円
      昼食・夕食 x 0: 0円
      帽子 x 0: 0円
      フォトサービス x 1: 1100円

      計: 5316円


      日程のご変更・その他ご不明点などございましたら、ご参加を希望されるスクールまでお気軽にお問い合わせください。

      ご請求内容につきましては改めてご案内いたします。

      何卒よろしくお願いいたします。

      KidsUP(school name)

      (link to manage email settings/unsubscribe)
      ```

- QOL

  - [] Add filtering to tables
    - [x] Create filter_controller
    - [x] Add to child index
    - [x] Add to customer index
    - [] Add to event sheet
    - [] Add to attendance sheets
    - [] Add to event registration????
    - [] Add to time slots???
  - [] Add sorting to tables

- Security

  - [x] Meeting
    - Qs 5, 6, 16 to Leroy

- Styling

  - [x] Login page (desktop)
  - [x] Forgot password page

- Validations

  - [] Child
    - [] Presence, all except
      - Ele school
      - first seasonal
  - [x] BS validations on all forms
    - [x] Login
    - [x] Sign up
    - [x] Child
    - [x] Event
    - [x] Time Slots
    - [x] Price lists
    - [x] Misc other small ones

## May 2nd

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- Email

  - [x] Configure app for sending email through SES
  - [x] Set up bounce and complaint notifications to go to my personal email (hopefully not a terrible idea)
  - Figure out how to
    - [x] preview emails
    - [x] test emails
      - temporarily set dev email config to be the same as production, export the SES creds as ENV variables **in the same WSL window**
  - [x] Write temp email templates in English
  - [x] Set up emails to be sent
    - [x] When invoice is updated
      - [x] Email SM saying it's been updated with link to the invoice
      - [x] Email parent with details and provisional price
      - [x] If student is at a closed school, send to Leroy instead
    - [x] When user signs up (to the user)
      - Needs DB changes, so I'll do it at night after SMs are done using the app
  - [x] Allow users to unsubscribe from our emails automatically by clicking a link
    - [x] Add the unsubscribe link to our email template
  - [x] Allow them to manually manage their email preferences when signed in

- Bugfixes

  - [x] Alter link from login to sign up so it doesn't shed locale info

#### What I learned

- Devise confirmation emails aren't sent if :reconfirmable is true, so make false and just don't use it

## May 3rd - May 8th

Golden Week

## May 9th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- Email

  - [x] Return to not requiring email confirmation before granting access to the site

- Bugfixes

  - [x] Prevent incorrect counting of afternoon meal options [#28](https://github.com/KUJP-code/db_prototype_v2_official/issues/28)
  - [x] Prevent accidental copying of afternoon registrations for a child's regular days [#29](https://github.com/KUJP-code/db_prototype_v2_official/issues/29)
  - [x] Show detailed info about registered options (#25)(https://github.com/KUJP-code/db_prototype_v2_official/issues/25)
    - Because the record isn't saved on the confirm page, using DB queries to find the relevant info doesn't work
    - Switched away from DB queries to (potentially slower) Ruby methods on the instantiated Invoice object
  - [x] JS calculations got messed up by me putting the children in tables, so had to fix those
  - [x] Fixed opts/slots in SS not correctly displaying as such/made the process of rendering them more efficient

#### What I learned

- Use #reorder to clear orders applied previously to your associations

## May 10th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- Backups

  - [x] Twice a day, rotate after 5 days

- Invoices

  - [x] Figure out why I can't show option details on confirm page
  - [x] Add various links and buttons to make navigating to linked pages easier
  - [x] Hide the merge form unless there's something to merge to
  - [x] Put dates for time slots next to their name in the summary

- Localisation

  - [x] Get screenshots of everything that needs to be translated & send to Leroy
    - [x] And the emails

- Validations

  - [x] Child
    - [x] Presence, all except
      - Ele school
      - first seasonal
    - [x] Katakana name is only katakana
    - [x] Birthday is between 1 and 15 years ago
    - [x] SSID is unique
    - [x] Grade, category and photos are only the values allowed in the enum

- Bugfixes/Misc Features

  - [x] Change 'Mark in SS' to 'Confirm Invoice'
  - [x] Fix navbar remaining invisible after printing attendance sheet
  - [x] Fix issues with photo service opt count being inaccurate due to added complexity from sibling registrations counting
  - [x] Fix 200yen not being applied on confirm screen due to the calculation using things which aren't saved yet
    - [x] Also refactored the calculation to dramatically increase performance
  - [x] Fixed adjustments not being included in the post-merge calculation when on the invoice being merged from
  - [x] Make site display in English if you're logged in as an admin
  - [x] Find the memory leak
    - Based on what I saw while the MG SM was looking around, something can potentially cause the site logo to be repeatedly loaded?
    - Looking at top very shortly after reveals basically 0 memory usage, while Elastic Beanstalk still says 92%
    - Seems there's some kind of lag on the EB measurement, maybe not as much of an issue as I thought if it's cleared that quickly?
    - Ah, the zero mem usage is only for the list of processes. In the summary at the top it does actually have 90%ish used
    - Using htop now, seems Puma processes might be the culprit for high memory usage
    - Tentatively seems it can be fixed with MALLOC_ARENA_MAX env variable, as per [here](https://www.speedshop.co/2017/12/04/malloc-doubles-ruby-memory.html)
    - Also possible Ruby just uses a lot of memory, might need to go to a 2GB instance rather than 1GB

#### What I learned

- Use #reorder to clear orders applied previously to your associations
- Using &.method means the method won't be called if the thing you're calling it on is nil
  - This is super super helpful, I know there were a lot of times using this would've made my code way simpler haha

## May 11th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- Children

  - [x] Change photo permission options back to OK/NG

- Hosting

  - [x] Create the production environment
    - [x] bump the versions of bundler and ruby to match the new platform version I was forced into

- Invoices

  - [x] Apply coupon button on confirm page that reveals a dropdown
    - Coupons are WELBOX/すくすくえいど

- Performance

  - [x] Clean up unused turbo frames

- SM Suggestions

  - [x] Sort student/parent indexes by name
  - [x] Change the total price on Invoices to 合計（税込）and remove the standalone 税込
  - [x] Make 'Confirm Booking' a toggle, so SMs can unconfirm and make changes
  - [x] Add regular placeholders to the first/last name/kana name fields on forms so they know which is which
    - Family name first
    - [x] Store them in the db this way too, so change the callback that sets the names

- Styling

  - [x] Change password screen

- Users

  - [x] Users can edit their personal info
  - [x] Show a badge asking them to verify email
    - [x] They can resend a confirmation email from there

- Validations

  - [x] Adjustments
    - Presence on change and reason
  - [x] Price Lists
    - Cost positive integer, presence
    - Name presence
  - [x] User
    - Presence of name, kana name, address stuff, phone

#### What I learned

- Maybe bump the platform version first, then upload the new app version.
  - Other way round caused some problems, not entirely sure how I fixed them other than restarting the app server and spam deploying the version bumped version
  - Because I tried to deploy new version on old platform it failed, but seems the new version was actually installed
  - So I had a version mismatch error, and couldn't redeploy the bumped version I wanted on there
- Should probably manually attach single images to multiple slots when seeding the real data so I don't have a million copies
  - Or figure out a way to do it in seeds, like creating the blob in AS then attaching it to all the slots
  - [Something like this maybe](https://stackoverflow.com/questions/72137882/attach-one-active-storage-blob-to-multiple-files)
- Shift + tab to collapse leading whitespace

## May 12th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- Database

  - [x] Re-write seeds file for new validations
  - [x] And to not create a million copies of each image
  - [x] And to put images into a folder in S3 based on environment and what they're an image for
  - [x] See what happens when you try to import a record that already exists with PG_COPY
    - It just tries to create a new one, that's not gonna work
  - [x] Create a second, slower way of importing CSVs that can update records
    - [x] For children
    - [x] For their schedules

- Emails

  - [x] Send customer a confirmation email when SM clicks 'Confirm Booking' on their invoice

- Forms

  - [x] Added a yen kanji to the change field on the adjustment form for clarity
  - [x] Made the selects on the Child form auto-derived from enums so I don't have to keep changing them if the values change

- Invoices

  - [x] Make it more obvious the invoice is confirmed, they have to click close on something
    - Nice big green box at the top of the page with a long, detailed message.

- Localisation

  - []

- Performance

  - [] Optimise AR queries for
  - [] Optimise view rendering for

- QOL

  - [] Add filtering to tables
    - [] Add to event sheet
    - [] Add to attendance sheets
    - [] Add to event registration????
    - [] Add to time slots???
  - [] Add sorting to tables

- Security

  - [] SM can only log in from their school's IP address **requires IP list**
  - [x] Run Brakeman and check what it finds
    - [x] Whitelist unsafe params

- SM Suggestions

  - [x] Snacks
    - [x] Frontend
    - [x] Backend
    - This is auto-applied to every child who is attending an afternoon and it's not their regular day
    - Since they can't apply for afternoons on their regular days, it's safe to add the option to every afternoon slot they register for
    - Leroy says its fine to just show them all in the summary, but let's try to do it for individual days as well if possible

- Styling

  - []

- Time Slots

  - [] Index for admins needs pagination for performance/not loading 10 billion images

- List of people who tried the site from logs

#### What I learned

- You can specify the path for ActiveStorage attachments like so `user.avatar.attach(key: "avatars/#{user.id}.jpg", io: io, content_type: "image/jpeg", filename: "avatar.jpg")`

## May 13th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- QOL

  - [x] Add filtering to tables
    - [x] Add to event sheet
    - [x] Add to attendance sheets
  - [x] Scaffold daily attendance summary on SM homepage

- Security

  - [x] Remove ability to change User roles from frontend

## May 14th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- Production setup

  - [x] Alter the CSVs controller for new data format
  - [x] Alter various pages to handle kids not having a school, or names

## May 15th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- Hosting

  - [x] Seed real child data to the production DB

- Performance

  - [x] Remove unnecessary helpers/routes
  - [x] Paginate indexes
    - [x] Children
    - [x] Users
  - [] Optimise AR queries for
    - [x] Child#index
    - [x] User#index
    - [x] Event sheet
      - [x] Event_child partial (this was a huge one, takes a third of the time to render the page now)

- QOL

  - [x] Add character counter to password/SSID fields

- Styling

  - [x] Daily attendance summary on SM homepage
    - [x] And make it printable

- Bugfixes

  - [x] Added a separate type to the JS price calc to avoid check boxes triggering the radio button function and adding/removing unexpected registrations
  - [x] Added a type filter to the check if an \_add_slot is registered to avoid false positives on option registrations

## May 16th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- Events

  - [x] Add the outdoor category to relevant time slots

- Invoices

  - [x] Hat adjustment is now only applied if child hasn't received hat and they're registered for an outdoor activity
  - [x] Create first time registration adjustment now it's different from hat

- Performance

  - [] Optimise AR queries for
    - [x] Slot children index
      - [x] Slot child partial (remove the depart/arrive time methods from time slot model after this)
    - [x] Use #select to only fetch relevant fields for User#index

- Production setup

  - [x] Cleaned out our S3 bucket now that I know how to not generate a billion junk files every reset
  - [x] Rebuilt the staging environment and reseeded it to test that I actually know how to not generate junk files
    - [x] Rewrote seeds files to do it even more efficiently
    - [x] Rename all the images to the japanese names of the time slots
    - [x] Discovered AWS/Ruby do NOT like Kanji/they use different encodings so a bunch of slots won't get associated with their images
      - [x] Write a translation hash to fix that and rename all the images to english
      - [x] It only works for 20, end up doing the other 11 by hand

## May 17th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- Children

  - [x] If children are missing required fields, populate them with a default value
    - Search like this `problems = Child.where(name: nil).or(Child.where(katakana_name: nil).or(Child.where(en_name: nil).or(Child.where(allergies: nil))))`
    - Then select (not where, it'll modify the records then not save) records with nil for a required value and loop over applying the default value
    - Then loop over saving all, printing the name of the record being modified for debugging
  - [x] Make blank default for kid photo permission
  - [x] When adding a new child from index, need to make the check boxes first seasonal rather than needs/received hat
    - [x] Also when claiming a child, they need to say if they've attended a seasonal or not - [] Use needs hat for first seasonal boolean
    - Lots of comments to explain why that is
    - Either automatically toggle when they register for their second seasonal or I do it manually to all after each event

- Localisation

  - [x] Add translation for copy-regs under the button to do so on event#show

- Performance

  - [] Optimise AR queries for
    - [x] Paginate TimeSlot#index
      - Page per event
      - use the event's school name as the key of the nav bar

- Styling

  - [x] Forgot password & password reset pages
    - [] No you didn't not responsive for mobile

- Bugfixes

  - [x] Stop showing the PIN popup on child page to users, they should just be able to see

## May 18th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- Children

  - [x] Merge children is broken, child has no parent??
    - Was using the SS child to get the list of kids to merge from, but they'll not be associated to a parent by definition
    - Instead used a parent param in the initial search by SSID to set the parent instance variable and get the list of mergeable kids from that
  - [x] Import the regular schedules on prod
    - [x] Test on staging/dev
    - [x] Fix some of the very weird logic I had in the upload method
  - [x] Link to the morning slot for both special days from event sheet, it has all the info

- Events

  - [x] Copy-regs fails because no en_days method on regular schedule
    - The method is there, but some kids don't have a regular schedule
    - Added logic to return a blank hash if no regular schedule, meaning no registrations will be skipped due to being regular days

- Localisation

  - [x] Authentication pages
  - [x] User profile
  - [x] Child/User forms
  - [x] SM sheets/lists
  - [x] SM invoice stuff
  - [x] Change my pass translation is missing
  - [x] Generic adjustments in invoice need English removed
  - [x] Merge child translations
  - [x] Toast translations

- Invoices

  - [x] First time reg needs to be based on the first seasonal (needs_hat) boolean
    - [x] Repeater discount should also use this boolean rather than looking for previous events

- Styling

  - [x] More clarity on Invoice summary
  - [x] Improve time slot partial layout
  - [x] Make links orange by default, grey on hover
  - [x] Reconfirm email page
  - [x] Forgot password & password reset pages
  - [x] Remove the negative margin on login page
  - [x] Different sizes for images on event#show?
  - [x] Coupon collapse makes the buttons look hilarious on mobile
  - [x] Summary popup on event sheet is off center

- Time Slots

  - [x] Time slot index links don't work on live
    - Was trying to access school 1, which doesn't exist anymore
    - Added a check to prevent that
  - [x] Completely redesigned pagination for TimeSlot#index to use my own method

- Users

  - [x] Add randomly generated password field, not editable, to create customer form
    - [x] Allow users to change their password by editing themselves
    - [x] Allow SMs to edit users without changing/needing their password
  - [x] AM should have a summary for their area on their homepage
  - [x] Admin should have a summary for the whole company

- Bugfixes

  - [x] Blank is still not default for photos on add child form
    - DB default for photos was NG, so I manually set it in controller when creating a new child
  - [x] Find child didn't add to leroy
    - Was caused by required values not being present on child records, resolved by adding defaults when importing children
  - [x] Some forms had the old first/last name order
  - [x] Got the different schools mixed up with the regular ones
    - American hot dogs is the normal one
    - [x] Change their event images
    - [x] Change their slots and images
    - [x] Add their options back
  - [x] On SM profile table, photo sales should only be the kids who paid for
  - [x] Print not working for attendance sheet, is for daily attendance on SM profile
  - [x] When we import children for update, I'll need to handle nil values in the import data for required fields
  - [x] Fix option radio button behaviour when already selected on load
    - selecting something else then reselecting the original option would lead to the FE price calculation showing the option as free
    - list of optCostTargets decreases when original option is selected (it should though, the temp opt is removed)
    - the registered class should also be removed from the hidden field when deselected, but it's not added back when reselected like it should be

## May 19th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- Adjustments

  - [x] Allow deletion of adjustments

- Children

  - [] Create 100 test children and add them to the online school

- Emails

  - [x] Change the devise mailer templates to reflect the translated versions
  - [x] Add a message saying when the SM updated the booking
  - [x] Create a layout with the signature and image
    - [x] Create a similar one just for Devise emails
  - [x] Change the booking related mailer templates to reflect translated versions
  - [] Add copy button to the email template

- Events

  - [x] Header disappears when you search the event sheet cos they have classes now
  - [x] Only show instructions for copying regs if more than one child

- Invoices

  - [x] Make the tax number smaller and after the final price
  - [x] Left align all the summary text
  - [] Have a total of all invoices costs on the event show page, invoice index (for both parent and children)
  - [x] have different success messages for parents and SM when updated
    - [x] have a different one for confirmed

- Localization

  - [x] Copy regs popup is in english
  - [x] Edit child on Child page (in the card and in the child summary at the top)
  - [x] When adding a new child on the parent page, the toast is missing a translation
  - [x] Coupon heading on the confirm page is in English
  - [x] Summer school needs to be in Japanese (Kids UP サマースクール 2023)
  - [x] Error messages on form submission are mostly fine but the name of the field is in english

- Performance

  - [] Optimise AR queries for
    - [] Event#show page
      - Try lazy loading closed accordion contents?
    - [] SM profile page
    - [] AM profile page
  - [] Optimise view rendering for

- Security

  - [] SM can only log in from their school's IP address **requires IP list**

- Time Slots

  - [x] Add the ability to close afternoon slots
  - [x] Add translations
  - [x] Make the index page more user friendly
  - [x] Update Yakisoba activity with new image and name
    - [x] Add the missing slot image on Den-en-chofu
  - [x] KidsUP 南町田グランベリーパーク has no morning extension
  - [x] 新浦安 has no 8:30 morning. Earliest they can start is 9:00
  - [x] Den-en-chofu is missing a time slot image
  - [x] Extension option missing from special day

- Users

  - [x] Added areas to the AMs

#### What I learned

- Can override the default layout for Devise emails like [this](https://stackoverflow.com/questions/72305122/after-upgrading-rails-from-6-1-1-to-7-0-3-my-devise-mailers-cant-be-initialized/72308475#72308475)

## May 20th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- Children

  - [x] Create 100 test children (and parents) and add them to the online school
  - [x] Investigated Leroy saying the update function doesn't work on children
    - On prod, around 4000 were updated in some way when he did it, but no idea if correctly
    - Tested updating name on dev, staging and prod, all worked
    - Will go over the exact fields he tried to update and check it out on Monday

## May 21st

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- Emails

  - [x] Make the email template Japanese
  - [x] Add copy button to the email template

- Invoices

  - [x] Have a total of all invoices costs on the
    - [x] event show page
    - [x] invoice index (for both parent and children)

## May 22nd

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- Children

  - [x] Go over the update function with Leroy
    - [x] Fix katakana missing default being hiragana

- Invoices

  - [x] Update the event cost translation and add the explanatory message

- Translations

  - [x] Changed some invoice related translations, and categories on event page

### Odin Project - [Rails Conclusion](https://www.theodinproject.com/lessons/ruby-on-rails-conclusion)

I submitted my work project for the final project rather than building a Facebook clone, since it let me get way more experience with the stuff I learned in Odin's Rails path and a whole lot more experience with stuff that wasn't covered/was skimmed over. I feel like building a Facebook clone with the requirements Odin sets would be kinda boring revision at this point, and I'll be keeping my Rails skills fresh by maintaining/adding features to the work project going forward. On to Advanced HTML and CSS! (by skimming the headings looks like I learnt most of the CSS stuff myself for the work project haha). But first time to set up my personal wiki in this repo.

## May 23rd

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- Localization

  - [x] Added a different message/subject to the booking update email depending on whether an SM or user caused the update
  - [x] Translated the site title

### Personal Project - Wiki

Start a wiki in this Journal repo to organise the stuff I learned more efficiently, and host on Github Pages

- [Setting up Github Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site)

#### What I learned

- Jekyll (a Ruby gem!) is used to build Github Pages
  - [Guide to setting up Jekyll](https://jekyllrb.com/docs/step-by-step/01-setup/)
  - Jekyll does not like tabs in its config file, use spaces
  - `bundle exec jekyll serve --livereload` to test locally
    - port is 4000, not 3000
  - You can set [defaults for front matter](https://jekyllrb.com/docs/configuration/front-matter-defaults/) in \_config.yml
- Frontmatter
  - two lines of --- with some yml in between
  - can be used to set objects, config for the page
- Liquid
  - [Objects](https://jekyllrb.com/docs/variables/)
    - Enclosed in double curlies like `{{ page.title }}`
  - [Tags](https://jekyllrb.com/docs/liquid/tags/)
    ```
    {% if page.show_sidebar %}
      <div class="sidebar">
        sidebar content
      </div>
    {% endif %}
    ```
    - For control flow
  - [Filters](https://jekyllrb.com/docs/liquid/filters/)
    - Change the output of an object, using a '|'
    - For example `{{ "hi" | capitalize }}`
- Includes
  - Kinda like partials, they go in the \_includes folder
  - Called in your page like `{% include navigation.html %}`
- Data Files
  - .yml files in \_data directory
  - they act as a kind of database, can be accessed like `site.data.????`
  - accept JSON, YAML and CSV

## May 24th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Bugfixes

  - [x] Personal info on user form actually says bank info
  - [x] Add a dash to the regex for katakana (and japanese space)
  - [x] Add some missing adjustment related translations to the registration page
  - [x] From customer list, creating a new customer asks you for password
    - because the auto generated passwords are missing??
    - editing doesn't
    - conditional was showing the temp passwords to users, not staff
  - [x] Check if copy_regs copies photo service registrations
    - it doesn't, but it also doesn't show the copied registrations on the summary despite copying them
  - [x] Hat adjustment can be added twice??
    - on minnie mouse on leroy's test profile, the confirmed one
    - it's because I'm manually calling save after update in the update controller action? some kind of timing issue?
    - that's being done because otherwise deleted adjustments are still (visually) on the booking after deletion, so maybe move the save into a callback after adjustment deletion
    - nope, no more callbacks for now thanks. Just added a check of the invoice's own adjustments, which includes pending ones
  - [x] Don't add adjustments if no slot regs??
    - comes down to whether we care about adding surprise adjustments or having leftover invoice costs more. I care more about surprise adjustments
  - These are both 'fixed', but the underlying problem is still there. I now just calculate and save the invoice every time its show page loads, which covers all the summary not updating issues we found. Doesn't create new versions of the invoice or add too much time to the page load. But need to refactor the calculation to not have this issue.
    - [x] You can register for options on a slot you're not attending **Temp resolution through show bandaid**
      - there is a callback on registration model, but doesn't seem to work (it actually does work, but not reflected in the summary)
      - triggers when booking is calculated again, so must be an issue with it calculating before the registrations for the time slot are deleted
      - if a slot is in ignore slots, add any registrations for its options to ignore opts?
      - adding invoice.calc_cost to the callback didn't change anything
    - [x] Show copied registrations on the invoice after copying them **Temp resolution through show bandaid**
      - seemingly only an issue when copying to a child who didn't previously have a booking for that event
      - the registrations etc. are copied correctly, but the summary text isn't updated

### Personal Project - Wiki

- Setup a basic, autogenerated list of topics

## May 25th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Bugfixes

  - [x] Handle attempted bookings for orphans by redirecting to child page and showing a warning asking to add a parent
  - [x] Change the afternoon name for special days to the actual name of the afternoon activity on that day
  - [x] Middle extension cost for special days needs to be 3 x the 30min extension cost for that level
    - [x] Seed k_extensions to production env
    - There's a different cost for kindy and elementary

- Localization

  - [x] Change all instances of booking to application
    - [x] And the more adjustments
  - [x] 3 回 not 3 コマ on invoice summary

- Performance

  - [x] Stats summary takes wayyyy too long to load at large numbers of registrations
    - Added eager loading for the big stuff, should do for now
  - [] Optimise AR queries for
    - [] Event#show page
      - Try lazy loading closed accordion contents?
    - [] SM profile page
    - [] AM profile page
  - [] Optimise view rendering for

- Security

  - [] SM can only log in from their school's IP address **requires IP list**

### Personal Project - Wiki

- Create separate collections for topics and link to them from the topics index
- Set up projects to have their own nav links
- Try and fail to set up each topic to have its own nav links because I can't get the correct layout to apply from frontmatter defaults

## May 26th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Bugfixes

  - [x] Handle cases where the customer selects options for a day, then deselects the day without deselecting options
  - [x] Special days should automatically add a 1500 yen adjustment when registered for (maybe count number registered in calc cost and have that many)
    - [x] also need to delete that adjustment when unregistered
    - [x] will need to update the FE calculation somehow too, probably by tagging special days and adding/subtracting 1500 yen per (can I do it the same way as snack?)
  - [x] A million other things I was too busy to write down as I did them
  - [x] Remove online course from offered schools
  - [x] And from the per-school event stats
  - [x] Hide empty areas in per-school stats for the big boss

- DB Changes

  - [x] Gave AMs their new areas

- Performance

  - [] **Stats summary takes wayyyy too long to load at large numbers of registrations**
  - [] Optimise AR queries for
    - [] Event#show page
      - Try lazy loading closed accordion contents?
    - [] SM profile page
    - [] AM profile page
  - [] Optimise view rendering for

- Security

  - [] SM can only log in from their school's IP address **requires IP list**

## May 27th-28th

Izu Roadtrip

## May 29th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Bugfixes

  - [x] Stats summary partial, and maybe the per school ones??? are broken
    - was showing regs for each category of kid that added up to more than the number of total regs
    - we believe total regs was right, based on adding up the totals from each school
    - maybe the < 3000 filter? (that was an issue, but smaller)
    - maybe because online was excluded from the list of events, but not when joining children with invoices
  - [x] Big boss sees the summary 3 times, but the stats are for all their areas combined?
    - made them actually per area
  - [x] Stop SS updates setting every parent id to nil
    - [x] and needs hat, and received hat

- Performance

  - [] Optimise AR queries for
    - [] Event#show page
      - Try lazy loading closed accordion contents?
    - [] SM profile page
    - [] AM profile page
  - [] Optimise view rendering for

- Security

  - [] SM can only log in from their school's IP address **requires IP list**

### Personal Project - Wiki

- Got per-topic layouts working, albeit by manually adding them to the topic pages rather than in the front-matter defaults

## May 30th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Bugfixes

  - [x] Fix the lambda being applied to the child/invoice association preventing anyone registering for anything
    - Filter meant the registration page never showed an invoice for kids to register on
    - because newly created invoices are always less than 3000, they weren't included in all invoices or active
    - also, a new one was still created each time
    - so some had 10+ invoices
    - added a separate, 'real invoices' association, which I should have done in the first place
  - [x] Saw someone repeatedly try to find a child by only their birthday, and made birthday/SSID fields required
  - [x] Saw a lot of people just leave after reaching the confirm page, so got a more explicit translation about needing to hit confirm
    - And put it in a yellow warning box

- Features

  - [] Add a search to the indexes (mainly for admins, there are too many pages and we don't know the order)
  - [] Possibly bring the recalculate button back, e.g. for children whose category in the SS changed since their booking was made

- Performance

  - Optimise AR queries for
    - [x] SM profile page
    - [x] AM profile page

- Security

  - [] SM can only log in from their school's IP address **requires IP list**

### Personal Project - Wiki

- Add instructions to the Jekyll section for creating new topics

## May 31st

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Bugfixes

  - []

- Features

  - [] Add a search to the indexes (mainly for admins, there are too many pages and we don't know the order)
  - [] Possibly bring the recalculate button back, e.g. for children whose category in the SS changed since their booking was made

- Security

  - [] SM can only log in from their school's IP address **requires IP list**

### Personal Project - Wiki

-

### Odin Project - [Transforms](https://www.theodinproject.com/lessons/advanced-html-and-css-transforms)
