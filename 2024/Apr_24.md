## April 1st

- [x] Fix parents not being unable to unregister for activities if it dropped them below their previous invoice amount

### Materials

- Add lesson search
  - [x] Write system spec
  - [x] Add views
  - [x] Add controller
  - [x] Figure out how to integrate the DA short levels (mostly just ele) into the search
    - Either duplicate the Ele key somehow
    - Or when mapping the select options, map the integer as the value rather than the downcased key
  - Remove the need for turbo-target top on status toggles
    - [x] refactor 'after_update_url' to be on lesson

## April 2nd

- [x] Fall back to simplest implementation of blank invoice protection; just disable it till they change something

### Event Site

Request will contain an array of event names they want stats for (determined in sheets by the close dates in sheets for those events) and an API key.

Needs to return these values for each event at each school which is ongoing or closed less than a month ago, as a hash keyed by event name and school id.

#### Seasonal

- Number of internal + reservation
- Number of external
- Internal + res revenue
- External revenue
- Goal

#### Parties

- Total revenue
- Goal

- [x] Write a wiki page for the API
- [x] Write a request spec for the API
  - [x] Include it in the auth before action
- [x] Add a route & controller action
- [x] Add the Model methods to get the necessary data

### Materials

- Add lesson search
  - Remove the need for turbo-target top on status toggles
    - [x] Make the visibility badges actually visibility toggles
    - [x] Style the lesson index table to match others
    - [x] submit a hidden 'index' boolean in the toggles that redirects to the index after updating
- [x] Add start/quit date/birthday dates to student
  - [x] Also search by birthday

## April 3rd

### Materials

#### Lessons

- [x] Only show toggle to release if the lesson is approved (or it's a course)
- [x] Allow writers to update proposals without creating a new one
- [x] Extract lesson attributes to a common partial rather than one per lesson type
- Proposed change rework - Make them just a state of Lesson
  - [x] Delete proposed change table
  - [x] Refactor ProposedChange tests to match proposals being a state of Lesson
  - [x] Write shared factory validity tests of proposals for each lesson type
  - [x] Add new proposal trait to base Lesson factory
  - Add columns to Lesson to duplicate the functionality
    - [x] Add an enum column to Lesson to indicate its proposal status
      - Accepted
      - Changes Needed
      - Proposed
      - Rejected
    - [x] Add an optional belongs_to ChangedLesson and has_many ProposedChanges on Lesson
  - [x] Refactor references to ProposedChange to match them being a state of Lesson
  - Need to be able to compare proposed change and current version side by side
    - [x] Create ProposalsController to handle the changes
    - [x] Create ProposalsController#show
    - [x] Update links where applicable to point at ProposalsController#show rather than LessonType#show
    - [x] Basic styling for ProposalsController#show

## April 4th

### Materials

#### Lessons

- [x] Add status to Lesson search
- [x] Remove proposing changes condition on attach guide to close issue 12
- [x] Add status to visibility toggles
- Proposed change rework - Make them just a state of Lesson
  - [x] Write tests for and create ProposalPolicy
  - Create ProposalsController#update, which
    - [x] Improve system spec expectations
    - [x] Updates proposal with new status/comments if not accepted
    - [x] deletes a Lesson and replaces it with the Proposal if proposal is accepted
      - [x] Add a class method to Lesson which handles the replacement
      - [x] Fix original lesson not being deleted due to destroy: option on associations
    - [x] otherwise does a normal update (only accepting status and internal comments as params)
  - [x] Write a model spec for accepting a proposed change and having it replace the existing one
  - [x] Have proposals table use the proposal form
  - [x] Remove changed_lesson_id field from proposal form as we can just get it from the proposal

## April 5th

### Materials

- Add site themes by
  - [x] Renaming all the `ku-purple` etc to more generic stuff like `color-primary`
  - [x] Add 'tailwind-theme-switcher' tailwind plugin and some demo themes
  - [x] Add dropdown component from [tailwindcss-stimulus-components](https://github.com/excid3/tailwindcss-stimulus-components)
  - [x] Create Stimulus theme switcher for admins
  - [x] Allow the theme to be set for an organisation
    - Add a helper which retrieves the theme based on a user's org id
    - Needs to fall back to the default if org doesn't have a theme
    - Name the theme like `org-n`
- [x] Write a wiki entry for the theme setup

## April 8th

### Materials

- [x] Review Jayson's PR
  - Doesn't work for non-admin users
  - Requested he add a highlight for tests when on test result page
- [x] Add an auto-expanding text area helper with StimulusComponents
  - Integrate it automatically into every text area by making a custom form builder and setting it as default
- Add scrolling to a given skill in the test results input
  - [x] Create stimulus controller
  - [x] Create the nav component
- Add slideover component for main nav on mobile
  - [x] Add stimulus controller
  - [x] Style

## April 9th

- [x] Help Leroy with some kids whose parents registered them for events at online
  - This took a really long time, and ended with two invoices being off by 1000yen combined -\_\_-
- [x] Send invoice change emails to all SMs, like we do for inquiries

### Materials

- [x] Require authorization on ProposalsController
- Add slideover component for main nav on mobile
  - [x] Keep signout link on far right for desktop, put in slideover for mobile
  - Reduce nav links to minimum necessary
    - [x] Admin

## April 10th

- If a kid is an online student, don't show the online event as their default.
  - [x] Render a highlighted message telling them they have to choose another school in place of the calendar/link
    - 参加希望のスクールをお選びください。
  - [x] Keep the image, but without a link or event name
  - [x] Show the expanded 'choose another school' option
  - [x] Add Event#with_sibling_events and an attr_reader to simplify getting & accessing sibling events in controller

### Materials

- [x] Add organisations#show
  - Plan
  - List of schools & school student counts
  - List of OrgAdmins
  - Student count
- [x] Style schools table header
- [x] Add list of classes & teachers to schools#show
- Reduce nav links to minimum necessary
  - [x] Writer
  - [x] Sales
  - [x] OrgAdmin
  - [x] SchoolManager
  - [x] Teacher
  - [x] Parent
- [x] Modify org theme helper to support use with no user/org params

## April 11th

### Materials

#### Auth

- [x] Remove Admins from visible types for Admin
- [x] Attempt 2 at merging Jayson's PR
  - [x] Restore the hover effect
- [x] Move theme selector out of role links, next to the lang toggle
  - [x] And find an icon for it
- [x] Give a link to sign up per-org with hidden field for the org id
  - [x] And a global sign up form with a select box for org
  - [x] Show the org signup link on OrgAdmin & SM homepages, as well as the Org#show page
  - [x] Add clipboard stimulus controller
- Add Alex's icons
  - [x] Teacher profile
  - [x] Lesson pages
  - [x] Course page, for the sections

## April 12th

### Materials

- [x] Address some issues Luis added to the repo, and help him/Jayson clarify tutorials requirements
- [x] Add support requests & messages to seeds
- [x] Fix the purple box around tutorials not reaching the top
- [x] Wrap activities on teacher page for large numbers of activities
- [x] Add extra emails jsonb column to users
  - They can add emails but not delete
    - [x] Write tests
    - [x] Write code
    - [x] Modify views/controllers
      - [x] And add a check for email validity
- [x] Add requester name to support requests
- [x] Style support requests

### Event Site

- [x] Create a page/scaffold for the downtime plan

## April 13th

### Materials

- [x] Respond to GH issues

### Event Site

- [x] Long meeting with leroy to plan out next year
- Update seeds to make testing easier, let other people actually set up a dev environment
  - [x] Test accounts, areas, schools, users & children
  - [x] Price Lists, Events & Time Slots
    - [x] Suppress STDOUT while adding images cos libvips has pointless errors
  - [x] Invoices
- Modify PriceList to use store_accessor for courses
  - [x] No point I think, you can't use numbers as keys

## April 14th

### Materials

#### CSV Upload

- [x] Write JS enabled system spec to lay it all out
  - Deliberately trigger some errors like not uploading a file, poorly formatted CSV
  - Check kids are shown as uploaded on current page once done
  - Check for successful upload by going to the index page
- [x] Scaffold Controller with new, update & create actions
- [x] Scaffold new view

## April 15th

### Materials

- Handle daily attendance in the LMS?

#### CSV Upload

- [x] Write tests for StudentUploadPolicy
  - [x] Create & enforce StudentUploadPolicy
- [x] Use PapaParse to parse CSV into student objects

## April 18th

### Materials

- Handle daily attendance in the LMS?

#### CSV Upload

- [x] Use Typescript for the Stimulus controller
- [x] Create a student table
- [x] Create rows for each student parsed from the CSV
- [x] Set their ID from the array index
- [x] Add an optional param for row creation which sets the status. Default is pending

## April 19th

### Materials

- Handle daily attendance in the LMS?

#### CSV Upload

- Add an optional param for row creation which sets the status. Default is pending
  - [] Make this an enumerated type with pending, uploading, done
- [] Use [@rails/request.js](https://github.com/rails/request.js) to get turbo-stream responses
- [] Should check is row is a valid child
  - Need some way of getting the idea of a 'valid child' from backend to frontend
  - Maybe values?
- [] Displays status as sticky heading at top, moves between checking, uploading, done
  - [] Also track pending, failures, successes
- Flesh out controller
  - [] New is form with a file field for the initial upload
  - [] When you click upload, a Stimulus controller intercepts the request and parses the CSV
- [] Populates list with children as they're processed, given 'pending' status
- [] Once a child is processed, push it to queue and start uploading
  - Have max concurrent uploads, maybe 2 or 3
  - Moves to done once all are processed and uploaded
  - If there's a network error (or timeout), give an option to retry
- [] Once the child is uploaded, controller sends back either

  - JSON indicating success which a stimulus controller uses to modify the child row
  - A turbo-stream to replace the child row with a success version

- [] Add staff uploads as well

- Address GH issues

### Event Site

- Write up the downtime plan
  - [] Dockerize, upgrade to Ruby 3.3
  - [] Backup the DB in every way possible
  - [] Spin up a new version with the (shared) DB backup on the PUP account and get it working
  - [] Switch the domain registrar to Cloudflare
  - [] Point the domain at the new EB
  - [] IP lock SM accounts
  - Extras if I have time
    - [] Maybe install SolidQueue and use it for emails
    - [] Maybe finish the invoice calc rewrite if I have extra time
    - [] Refactor the Event#show page and move it to Invoice#new

##### Testing

- Write tests for Invoice#calc_cost to prepare for the rewrite
  - Summary
    - [] Test that event options are removed from blank invoices
      - They're currently shown, and the registration remains on the invoice, but not charged for
      - Did not end up doing this because the logic is too entangled
      - Obvious solution is to mark them for destruction in orphan option check, but that's also used with hashes, not just models
      - So can't call #mark_for_destruction, #destroy or set the \_destroy flag
  - [] PDF creation (or at least that one is created)
- Rewrite Invoice#calc_cost as separate classes for cost calculation, summary generation and PDF creation
  - Can test it separately with unit tests till ready, then swap it in when done
- [] Refactor request specs to use rails path helpers
- [] Test emails with [email_spec](https://github.com/email-spec/email-spec) gem
- [] Create `rails predeploy` task to run all the tests and brakeman prior to deployments

#### Future Plans

- [] Add a table showing a summary of inquiries per month and type, as well as total per month [like this](https://docs.google.com/spreadsheets/d/1fcCN4togDFfhgDeuver5Ts-Javrq_s-RI0b_qRcJc3k/edit#gid=1456240236)
- [] Allow for varying price list courses by automatically determining max/intervals in invoice calc
- [] Overwrite the sign in path properly as well
  - Can use `stored__location_for` to redirect to originally requested page
- [] Uncomment `config.force_ssl` in production, we're already redirecting to HTTPS and the other stuff is good
- [] Investigate what happens if you upload a new asset with the same key as an existing one
- [] When importing the historical setsu/inquiries, try insert/upsert_all with record_timestamps: false to set our own created at
- [] In August 2022, RDS certificate [expires](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/UsingWithRDS.SSL-certificate-rotation.html#UsingWithRDS.SSL-certificate-rotation-updating). Will need to rotate to avoid connectivity issues.
- [] Move control of the domain from Onamae to Cloudflare
- Platform Upgrades
  - TEST ALL ON STAGING FIRST
  - [] Bump AWS platform version
    - [] And enable YJIT
  - [] Try bumping Ruby version to latest stable (can maybe install manually with a pre-deploy hook)
- [] Add button to generate photo service armband PDF for parties
  - Printable template with kids' names and a color which shows their photo status

##### ActiveRecord

- Look into [delegated types](https://api.rubyonrails.org/classes/ActiveRecord/DelegatedType.html)
  - [] especially for splitting the mess of user logic into more manageable chunks
- Maybe use [#store](https://api.rubyonrails.org/classes/ActiveRecord/Store.html) on models with JSON, seems to give a nicer API
  - [] price lists
  - [] surveys
  - [] maybe email preferences
- Can use has_one on a has_many to single out a specific important record
  - [] Next event
  - [] Active invoice
- Rather than manually setting `_destroy`, use `#mark_for_destruction`
  - [] Will be used by invoice calculations, maybe in the confirm controller too?
- You can define methods on associations either by nesting them within a block for that association or defining a class method on the model like `self.my_method`
  - Lets me pass parameters to an operation on an association
  - But I think this is basically just scopes no?
  - Apparently can define a scope on children like `scope :event_invoices, ->(name) { where(event_name: name) }`
- More specific to what I've needed before, you can pass params to scopes by just putting brackets with the params after the '->'
  - Can also put these in modules for re-use, could be handy for stuff like dates that are on everything
  - [] Definitely useful somewhere in the Charts/Stats section of the site
- validates_acceptance_of creates a virtual attribute which must be true for the record to be saved
  - [] add to User for backend validation of privacy policy
- You can chain a list of validations on a single column, like `validates presence: true, uniqueness: true ... etc.`
- Use SQL strings, or maybe the active_record_import gem to update children

##### Optimisation

- [] Nest the confirm_invoice view inside the new route so it's confirm_new_invoice_path

```
resources :invoices do
  new do
    post :confirm
  end
end
```

- [] Similarly, I could do school filtering by nesting those resources inside the school resource.
- [] Use #fetch and #dig in the controller rather than conditionals about the existence of a param, since they can have a default value if not found
- See if the occasional memory problems are actually something more like [this](https://www.engineyard.com/blog/thats-not-a-memory-leak-its-bloat/)
  - [] Also loading all the TimeSlots and Options from the start when calculating Invoice costs
  - [] Also maybe Rack::Bug, or a newer version of something similar since it was last updated in 2015
- Simplify/modularize invoice code
  - [] Split out PDF functionality
  - [] Preload all the stuff I need for calc_cost at the start and pass it explicitly
  - [] Create columns for each type of cost?
- [] use read/write_attribute or bracked notation in my custom getters/setters
  - Not sure what I'm using now, but probably not those
- [] Use AWS Cloudfront to serve images?
- [] Can probably speed up queries for ChartController with pluck
- [] If indexing FK columns which can be null, exclude null from the index

##### Views

- [] Extract conditonal info display into its own partial
  - Already done for the child one, just make more general for parents & move to shared folder
- [] Remember you can use partials in turbo-stream responses, I'm sure there's some stuff to clean up there
- [] Move set_shared_vars in the mailer to a before_action, is fine to apply to all mailers I think
- [] Use @layer to section off old BS styles so I can switch to tailwind
  - But both tailwind and BS using !important liberally might make that problematic
- [] Use `current_page` helpers in partials to conditionally render stuff like diff school selection on event partial
- [] Add a photo_for helper to encapsulate nil checks for associated images and return empty string if missing
- [] Check for missing translations with `i18n-tasks`
- [] Remove locale param from number_to_currency calls, shouldn't need it
- [] number_to_phone_number exists
- [] there's also a number_to_percentage helper, but may be more verbose than what I'm doing now
- [] Change the current event#show to be Invoice#new, since that's what it really is
  - [] Rework the current add_slot partials into a container, morning and afternoon
    - They can likely use fieldsets (with a form attribute matching the invoice form's id) to be submitted with the form directly
    - reduces the JS I need on that page [MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset)
- [] If you wanna show fallback content (like on the invoice index) use `render 'partial' || 'fallback text/content'`
- [] Extract form error messages into a shared partial
- [] Potentially also extract fields shared between multiple models into a partial (e.g. names for kids/parents)
  - Or just partials for each type of form group? As a fieldset
- [] Apparently there are undocumented ControllerHelper methods I can use to generate the ID for for main elements
- [] Use time_tag helper when outputting date or time, generates a `time` element which apparently is a thing
- [] Use number_to_human_size when I add the blob index etc.
