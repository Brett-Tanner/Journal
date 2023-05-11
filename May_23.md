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

- Emails

  - [] Send customer a confirmation email when SM clicks 'Confirm Booking' on their invoice

- Invoices

  - [] Make it more obvious the invoice is confirmed, they have to click close on something

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
  - [] Run Brakeman and check what it finds

- SM Suggestions

  - [] Snacks
    - This is auto-applied to every child who is attending an afternoon and it's not their regular day
    - Since they can't apply for afternoons on their regular days, it's safe to add the option to every afternoon slot they register for
    - Leroy says its fine to just show them all in the summary, but let's try to do it for individual days as well if possible

- Styling

  - []

- Time Slots

  - [] Index for admins needs pagination for performance/not loading 10 billion images

- List of people who tried the site from logs

#### What I learned

-
