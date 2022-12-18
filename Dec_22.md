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


## Mon 5th
### Work Project - [Event Database Prototype](https://github.com/Brett-Tanner/event_db_protoype)
#### What I did
- Finalized the tricky associations
- Changed the Devise after_login redirect to point at the current_user's show page
- Create views for:
  - Events (and the required partials)

#### What I learned
- You can change where Devise redirects after a successful login with
```
def after_sign_in_path_for(resource)
  user_path(current_user)
end
```
- You can have partials for models the don't have a controller, and you can call them with render through their relationship to another model

## Tues 6th
### Work Project - [Event Database Prototype](https://github.com/Brett-Tanner/event_db_protoype)
#### What I did
- Finally set up editing registrations per child on the event page
  - Then finished another epic journey to only show registrations for the actual event, rather than all a child's registrations
- Added some basic logic for filtering views to the child list, event list and list of children on the event page
- Applied basic styling to events/show
- Styled the nav_bar

#### What I learned
- form_with a model gets angry if you're missing REST resources like index

- when using fields_for, you can filter the model you use down with the second argument, like "child.registrations.where(event_day_id: event_days)"
  - event_days was an array of the event_days for the current event, cos looking for the actual event was a hassle

## Wed 7th
### Work Project - [Event Database Prototype](https://github.com/Brett-Tanner/event_db_protoype)
#### What I did
- Set it up so you can also change a kid's registration status on their own page
- And on their parent's page
- Filled in the missing parts to create a new event
  - also put a mini-form at the top of the event#index page that lets you generate a new event form with the correct number of event days

#### What I learned
- 


## Thurs 8th
### Work Project - [Event Database Prototype](https://github.com/Brett-Tanner/event_db_protoype)
#### What I did
- Register newly created kids for all events at their school
- Add admin forms for creating new 
  - [x] kids
  - [x] school managers
  - [x] parents
    - [x] with a stimulus controller to add kids

#### What I learned
- 

## Fri 9th
### Work Project - [Event Database Prototype](https://github.com/Brett-Tanner/event_db_protoype)
#### What I did
- [x] Add a school#show view
- Add admin forms for creating new 
  - [x] schools
    - [x] create a school manager at the same time
- [x] Fix the count of kids attending for events/their days
- [x] Record a video explaining how to add fields to a model for Leroy

#### What I learned
- If you want logged in users to create new users, you need to namespace the devise_for routes like "devise_for :users, path: 'u'", otherwise they interfere with your controller
  - since they require the client to not be logged in to register/log in
- There is a [better way](https://github.com/heartcombo/devise/wiki/How-To:-Require-authentication-for-all-pages) of requiring authentication for your whole site
- You can override add to the methods that your associations give you by defining them in the model and using super to give you access to the result of the unaltered method e.g.
```
def events
  super.distinct
end
```

### Odin Project - Ruby on Rails - [Rails Final Project](https://www.theodinproject.com/lessons/ruby-on-rails-rails-final-project)

#### What I did
- Continued learning about/setting up testing from [here](#thurs-1st)

#### What I learned
- Testing
  - use the -b option to provide a full backtrace for any errors
  - ignore errors by using this rather than the standard assert
  ```
  assert_raises(NameError) do
    some_undefined_variable
  end
  ```
  - [Rails comes with these default assertions](https://guides.rubyonrails.org/testing.html#available-assertions)
    - flunk(msg) is my favourite, it just fails the test under all circumstances
    - [Rails also adds some of its own, more complex assertions](https://guides.rubyonrails.org/testing.html#rails-specific-assertions)
    - Enable multi-core parallelization with this in test_helper.rb 
    ```
    class ActiveSupport::TestCase
      parallelize(workers: 2)
    end

    ```


## Sat 10th
### Odin Project - Ruby on Rails - [Rails Final Project](https://www.theodinproject.com/lessons/ruby-on-rails-rails-final-project)
#### What I did
- [x] Generated and tested User model

#### What I learned
- You don't need password_confirmation when you're creating Users in seeds/console/tests
- Can use [ActiveText](https://guides.rubyonrails.org/action_text_overview.html) for text posts 


## Sun 11th
### Work Project - [Event Database Prototype](https://github.com/Brett-Tanner/event_db_protoype)
#### What I did
- [x] Fixed a bug caused by not updating old Child records with the new Category field

#### What I learned
- If you're adding a new field to old tables/records, it seems including a default value in the migration will update all the old records without that value to have the default you set
  - If you're setting a ore complex default that uses a conditional for example, better to use after_initialize though


## Mon 12th
### Odin Project - Ruby on Rails - [Rails Final Project](https://www.theodinproject.com/lessons/ruby-on-rails-rails-final-project)
#### What I did
- [x] Switched to RSpec for testing
- [x] Rewrote User tests for RSpec
- [x] Generated Friendship model
  - [x] Tested basic functionality
  - [x] Added/tested associations to User

#### What I learned
- How to [set up Rspec with Rails](https://medium.com/@amliving/my-rails-rspec-set-up-6451269847f9)
  - but remember it's factory_bot now, not factory_girl
- Faker is not only the GOAT, but a very useful Ruby gem


### Work Project - [Event Database Prototype](https://github.com/Brett-Tanner/event_db_protoype)
#### What I did
- [x] Fixed a bug where children created by creating a new parent wouldn't be registered
- [x] Fixed a typo which was submitting the SM's details as the school's details when creating a new school

#### What I learned
- You define before_save, before_action etc. and the methods they call/code they run on the model, not the controller
  - I wanted after_create, not after_save in this case, as _save is triggered when the record is updated as well


## Tues 13th
### Odin Project - Ruby on Rails - [Rails Final Project](https://www.theodinproject.com/lessons/ruby-on-rails-rails-final-project)
#### What I did
- [] Set up tests and run them continuously using [Guard](https://github.com/guard/guard), like [this](https://www.learnenough.com/ruby-on-rails-4th-edition-tutorial/static_pages#sec-guard)
  - [] Integration tests
    - []
  - [] Unit tests (model associations/controllers)
    - [x] Users
    - [x] Friendships
    - [x] Notifications
    - [] Posts
    - [] Comments
    - [] Likes

- [x] Install Devise & generate Users resource
  - [x] Redirect all to login page if not logged in
  - [x] Create friend requests
- [x] Create notifications
- [] Create Posts resource
  - [] Create Likes
  - [] Create Comments resource
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

#### What I learned
- Rails' route helpers are not available in RSpec by default, this can be problematic
  - There is also a larger problem with seemingly not being able to use the route helpers in your model?? Might need to do it thru controller instead
- Do I really need a separate notification model or can I just show the count of unread thingies on the nav bar?

## Wed 14th
### Odin Project - Ruby on Rails - [Rails Final Project](https://www.theodinproject.com/lessons/ruby-on-rails-rails-final-project)
#### What I did
- [] Set up tests and run them continuously using [Guard](https://github.com/guard/guard), like [this](https://www.learnenough.com/ruby-on-rails-4th-edition-tutorial/static_pages#sec-guard)
  - [] Integration tests
    - []
  - [] Unit tests (models)
    - [x] Users
    - [x] Friendships
    - [x] Notifications
    - [x] Posts
    - [] Comments
    - [] Likes

- [x] Create Posts resource
  - [x] Update Posts test and existing tests to make use of Factory Bot
- [] Create Likes
- [] Create Comments resource
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

#### What I learned
- Action Text doesn't need a content column, you just set it up as an association
  - but you can still use validations like it was a column
- Read about [Factory Bot](https://github.com/thoughtbot/factory_bot/blob/main/GETTING_STARTED.md)
- Regex is annoying
  - But I found a nice test site [specifically for Ruby](https://rubular.com/)
  - And learned you can replace ^ with \A, $ with \z in Ruby to fix security issues


### Work Project - [Event Database Prototype](https://github.com/Brett-Tanner/event_db_protoype)
#### What I did
- [x] Changed the authentication requirement for all routes to be in the routes.rb file, not the application controller as recommended by the Devise wiki
  - [x] Fixed the unnoticed naming collision between Registrations controller and Devise's

#### What I learned
- Naming a controller Registrations when you're using Devise is a problem cos it conflicts
  - But you can namespace it to avoid that, and kinda makes sense to do that with registrations here anyway


## Thurs 15th
### Odin Project - Ruby on Rails - [Rails Final Project](https://www.theodinproject.com/lessons/ruby-on-rails-rails-final-project)
#### What I did
- [] Set up tests and run them continuously using [Guard](https://github.com/guard/guard), like [this](https://www.learnenough.com/ruby-on-rails-4th-edition-tutorial/static_pages#sec-guard)
  - [] Integration tests
    - []
  - [x] Unit tests (models)
    - [x] Comments
    - [x] Likes

- [x] Create Likes
- [x] Create Comments
- [x] Make the Posts index a timeline of all current_user posts and those of their friends
- [] Create Post partial that displays content, author, comments and likes
- [] Create User#show which displays their personal info, posts and a photo
- [] User#index shows all Users and a button to send them a friend request
- [] Use Omniauth so users can sign in with their real FB account
- [] Set up a mailer with
  - [] A welcome email
  - [] Notification emails
- [] Deploy
  - [] Figure out how to send emails without SendGrid/Heroku

#### What I learned
- Factory Bot
  - Can use aliases to allow you to reference an object using associations not named after it
  - Can define transient variables in the factory which won't be set on the object under any circumstances but can be used for logic in creating it
  - You can nest factories to do something like what I wanted with user/friend, you just create another factory inside the first one which has different values not defined in the parent factory
    - Best practice is to start by defining a base factory with only the values required to create the object, then nest factories with any variations on that
  - To put an association in your factory, just include the name of the association with no block passed
    - or if you need to do it explicitly, "association :name" 
    - when you do it that way, you can override attributes on the association object like "association :author, last_name: "Writely""
    - remember you can manually specify the object associated by passing it to build/create like this "post = build(:post, author: eunji)"
      - but I think I still prefer just doing this in the tests manually unless a good reason comes up not to
      - same with [has_many associations](https://github.com/thoughtbot/factory_bot/blob/master/GETTING_STARTED.md#has_many-associations), feels much simpler to just use the Rails syntax in the tests for this
  - To avoid duplicate pkeys, have the id of each object set to {|n| n} so it'll auto-increment with each object created

- Polymorphic associations
  - When you're validating them you have to do each of the _id and _type cols separately
  - but in factory_bot you can just pass an object to likeable, for example

- Security
  - It would probably be best to split names into first, last and title so you don't need to allow spaces or dots, and have the title be a dropdown selection
  - But that's an annoying amount of work with Faker for something that won't matter on this project, good to keep in mind for the event_db though
    - Even though Japanese names maybe don't have spaces between 1st and last?

### Work Project - [Event Database Prototype](https://github.com/Brett-Tanner/event_db_protoype)
#### What I did
- [] 

#### What I learned
- i18n
  - Pretty much perfect for localizing the project so I can read in English in dev/test and just have someone translate for production
  - Stores the translations in something like a hash
  - 2 best ways of deciding which language to use are using a domain like .jp/.en or just passing the language as a param to literally everything
    - 2nd is not as horrendously messy as it sounds, there are ways to hide it in the final URL
  - basically prepend t to anything in the view/controller to translate, or l to localize times
  - uses Simple backend to store the translations in either Ruby or YAML
    - got the impression Ruby is just better, mostly cos it'll throw an error rather than silently fail in some cases
    - relatively ez to use a different backend, might look into if there's one for JP
  - there are user translations for a lot of things/languages, look into that

## Fri 16th

### Work Project - [Event Database Prototype](https://github.com/Brett-Tanner/event_db_protoype)
#### What I did
- [x] Created area_manager role and added event_splash controller/view for the QR code link
- [x] Moved the current app to first_prototype branch so I can start fresh for the prototype I'm presenting

#### What I learned
- You can create a fresh Rails app in an existing directory/repo with "rails new . --database=postgresql --skip-git"
  - Maybe don't do that
  - I had just soooooooooooo much fun with git
    - eventually just checked out the last commit before I messed things up 
    - then committed it to a branch 
    - hard reset main with that branch
    - then force pushed it


## Sun 18th

### Work Project - [Event Database Prototype](https://github.com/Brett-Tanner/event_db_protoype)
#### What I did
- [x] Created a whole new repo so the old one is definitely safe from me messing stuff up with git
- [x] Installed devise
- [x] Required authentication for all pages, though remember you'll need to add each controller as you create it and think about namespacing

#### What I learned
- Don't code while tired, or you'll cd into the wrong folder and delete a perfectly good fresh repo due to an error in an entirely different one


## Mon 19th

### Work Project - [Event Database Prototype](https://github.com/Brett-Tanner/event_db_protoype)
#### What I did
- [x] 

#### What I learned
- 