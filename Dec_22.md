# December 2022
## Thurs 1st
### Odin Project - Ruby on Rails - [Rails Final Project](https://www.theodinproject.com/lessons/ruby-on-rails-rails-final-project)

#### What I did
- [] Plan out the db schema
- [] Set up tests and run them continuously using [Guard](https://github.com/guard/guard), like [this](https://www.learnenough.com/ruby-on-rails-4th-edition-tutorial/static_pages#sec-guard)
  - [] Integration to make sure pages load correctly
  - [] Unit to make sure model associations work correctly
- [] Install Devise & generate Users resource
  - [] Redirect all to login page if not logged in
- [] Implement friend requests
- [] Implement notifications
- [] Create Posts resource
  - [] Create Comments resource
  - [] Create Likes join table??
  - [] Create Post partial that displays content, author, comments and likes
- [] Make the Posts index a timeline of all current_user posts and those of their friends
- [] Create User#show which displays their personal info, posts and a photo
- [] User#index shows all Users and a button to send them a friend request
- [] Use Omniauth so users can sign in with their real FB account
- [] Set up a mailer with
  - [] A welcome email
  - [] Notification emails
- [] Deploy
  - [] Figure out how to send emails without SendGrid/Heroku

##### Extra Credit
- [] Allow posts to have uploaded images
- [] Use ActiveStorage to allow Users to upload more than just a profile pic
- [] Use polymorphic associations to make Posts text OR photos
- [] Fashion is my profession


#### What I learned