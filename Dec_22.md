# December 2022
## Thurs 1st
### Odin Project - Ruby on Rails - [Rails Final Project](https://www.theodinproject.com/lessons/ruby-on-rails-rails-final-project)

#### What I did
- [] Set up tests and run them continuously using [Guard](https://github.com/guard/guard), like [this](https://www.learnenough.com/ruby-on-rails-4th-edition-tutorial/static_pages#sec-guard)
  - [] Integration tests
    - []
  - [] Unit tests (model associations/controllers)
    - [] Users
    - [] Friendships
    - [] Notifications
    - [] Posts
    - [] Comments
    - [] Likes

- [x] Plan out the db schema
- [x] Install Devise & generate Users resource
  - [] Redirect all to login page if not logged in
  - [] Create friend requests
- [] Create notifications
- [] Create Posts resource
  - [] Create Comments resource
  - [] Create Likes
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
- [] Use Action Cable to have the new posts instantly show up in other User's feeds
- [] Fashion is my profession


#### What I learned
- Realised it's not the post model that needs to be polymorphic, it's the comment and like models. You just have separate models for text and image posts which are both commentable and likeable

- Active Storage creates a bunch of tables that allow it to work, and requires configuration with some kind of cloud storage service
  - you can use it by specifying has_one_attached or has_many_attached on the model you want to have the image, no additional columns needed

- Devise
  - Remember generating a User with Devise only creates the Model, you're still free to generate the Controller/tests yourself
  - To put all the stuff for turbo-compatibility in one place:
    - This goes in turbo_controller.rb
    ```
    class TurboController < ApplicationController
      class Responder < ActionController::Responder
        def to_turbo_stream
          controller.render(options.merge(formats: :html))
        rescue ActionView::MissingTemplate => error
          if get?
            raise error
          elsif has_errors? && default_action
            render rendering_options.merge(formats: :html, status: :unprocessable_entity)
          else
            redirect_to navigation_location
          end
        end
      end

      self.responder = Responder
      respond_to :html, :turbo_stream
    end
    ```
    - This is added to the Devise initializer
    ```
    class TurboFailureApp < Devise::FailureApp
      def respond
        if request_format == :turbo_stream
          redirect
        else
          super
        end
      end

      def skip_format?
        %w(html turbo_stream */*).include? request_format.to_s
      end
    end

    config.parent_controller = 'TurboController'

    config.navigational_formats = ['*/*', :html, :turbo_stream]

    config.warden do |manager|
      manager.failure_app = TurboFailureApp
    end
    ```

- Testing
  - Write tests in a block like (opposite of assert is assert_not)
  ```
  test "the truth" do
    assert true
  end

  ```
  - Tests can make as many assertions as you want
  - They seem to clean up after themselves


### Work Project - [Event Database Prototype](https://github.com/Brett-Tanner/event_db_protoype)
#### What I did
- Planned the visual db schema
  - then wrote it out
- Installed Devise and generated the User model with roles


#### What I learned
- ctrl + shift + v opens a preview of the .md file you're working on
  - learnt this purely because I fat-fingered a button lol

- Devise Roles
  - add an integer column to the User model named role, give it a default value of 0 (your normal User, a parent here)
  - in the User model add "enum role: [:parent, :school_manager, :admin]"
    - the role column from your User model maps to an index in this array
  - also add "after_initialize :set_default_role, :if => :new_record"
    - and the accompanying method
    ```
    def set_default_role
      self.role ||= :user
    end
    ```
  - will need to make sure there's some way of adding Users manually in production, either through seeding an admin role who can add them or accessing the production db through the rails console/directly
    - cos I think you don't want school managers or admins to be able to sign up on the site, that form should always be role: 0 at a controller level, no possibility of changing it


## Fri 2nd
### Work Project - [Event Database Prototype](https://github.com/Brett-Tanner/event_db_protoype)
#### What I did
- Generated User model
  - Seed some parents, SMs and an Admin
  - And REST controller
  - And basic views
- Generated School model
  - Added User association
- Generated Child model
  - Added user association
- Generated Event model
  - Added School association

#### What I learned
- Different views for different roles is fairly easy to do in your controller, per [this SO answer](https://stackoverflow.com/questions/39970314/how-do-i-create-multiple-views-for-different-users-by-role)


## Sat 3rd
### Work Project - [Event Database Prototype](https://github.com/Brett-Tanner/event_db_protoype)
#### What I did

- Generated Event model
  - Added Child association through Registrations
- Generated Event_day model
  - Added associations
- Generated Registration model
  - Added associations
- Generated Emergency_contact model
  - Added child association

#### What I learned
- Decided I actually want to have registrations be on event_days, not events

- Learned why it's important to not make dumb typos in migrations (registration_table_table) and not proofread them before running them