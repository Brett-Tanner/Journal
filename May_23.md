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

## May 3rd - May 7th

Golden Week

## May 8th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- Backups

  - [] Twice a day, rotate after 5 days

- Hosting

  - [] Uploaded Email update and reset the database to facilitate all the changes
  - [] Set up dev environment

- Invoices

  - [] Figure out why I can't show option details on confirm page
  - [] Put dates for time slots next to their name in the summary

- Localisation

  - []

- QOL

  - [] Add filtering to tables
    - [] Add to event sheet
    - [] Add to attendance sheets
    - [] Add to event registration????
    - [] Add to time slots???
  - [] Add sorting to tables

- Security

  - [] SM can only log in from their school's IP address **requires IP list**

- Styling

  - []

- Time Slots

  - [] Index for admins needs pagination for performance/not loading 10 billion images

- Validations

  - [] Child
    - [] Presence, all except
      - Ele school
      - first seasonal

- Bugfixes

  - []

#### What I learned

-
