# May 2023

## May 1st

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- Emails **Requires being let out of sandbox**

  - [] Write a proper application to get out of email sandbox

    - As much detail as possible
    - How often we send
    - How we manage recipient lists
    - Details of the app
    - Bounces
    - Complaints
    - Unsubscribe requests
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
      ```

  - [] When new invoice is confirmed or invoice is updated
    - [] Email SM saying it's been created with link to the invoice
    - [] Email parent with details and provisional price
    - [] If student is at a closed school, send to Leroy instead
  - [] When user signs up (to the user)

- Hosting

  - [] Set up dev environment

- Invoices

  - [] Figure out why I can't show option details on confirm page

- Localisation

  - []

- QOL

  - [] Add filtering to tables
  - [] Add sorting to tables

- Styling

  - [] Login page (desktop)

- Time Slots

  - [] Index for admins needs pagination for performance/not loading 10 billion images

- Users

  - [] SM can only log in from their school's IP address **requires IP list**

- Validations

  - [] Child
    - [] Presence, all except
      - Ele school
      - first seasonal

- Bugfixes

  - []

#### What I learned

-
