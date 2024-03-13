# March 2024

## March 1st

- [x] Actually apply the CoursePolicy to requests -__-
- [x] Rename ca/aa/_id/name to admin_approval & curriculum_approval, completely unreadble if you haven't worked on them in a while
- [x] Give Luis a button to actually add new lessons from the index
  - Probably turn the existing dropdown into a partial
  - [x] And make it pretty
- [x] Create the online-specific setsu inquiry email
- [x] Add oddities section to Setsu Calendar, so far just includes the hardcoded order array

#### Sales/OrgAdmin

- Support
  - Display notifications for support messages
  - Generate the resource
    - [x] SupportMessages
  - Create & test models
    - [x] SupportMessage
  - Create & test policy
    - [x] SupportMessagePolicy
      - Unnecessary as if you can see the SupportRequest you can see its messages, and there's no way of viewing them directly
      - Any user can create support messages on a Request they're authorised to view, so not auth needed there
  - Write system spec
    - [x] OrgAdmin creating SupportMessage
  - [x] Create SupportMessage partial
  - [x] Link to the support request index in the nav, and have the form to add a new one at the top of it
  - [x] Tidy up Support related views
  - [x] Reset 'seen_by' on new support messages

#### Teacher Interface

- Match their profile to Louis' wireframe/Alex's designs
  - Navbar
    - [x] Style to match the design
    - [x] Highlight the current link
    - [x] Add subtitle

## March 2nd

- [x] Give AMs a card with links to SM pages in their areas
  - And give them permission to see them

### Setsumeikai Calendar

- [x] Style the desktop view event cards to ensure the full time is always visible
- [x] If an online setsumeikai is selected, only show online as an option in the dropdown
- [x] On the summary, show '自宅からオンラインで参加' for the venue rather than the school name

### Materials

- [x] Define an ATTRIBUTES constant on each lesson type, use it in strong params on controllers/
  - proposed changes controller anywhere else it might be useful
  - up to exercises controller

#### Teacher Interface

- Match their profile to Louis' wireframe/Alex's designs
  - [x] Add the day links
  - [x] Grey out past days
  - [x] Add contextual styles/text to subtitle if not on current day
  - [x] Move current date to the main nav
  - [x] Add contextual link back to current day
    - If in a future week

## March 5th

- [x] Fill in my self-intro slide

### Materials

- [x] Style login page

#### Teacher Interface

- Create Plans linking organisations and courses
  - [x] Create resource
  - [x] Edit & test model/factory
    - [x] Add & test Teacher#day_lessons
  - [x] Add seeds for plans
  - [x] Write a system test for creating one
  - [x] Create & test PlanPolicy
  - [x] Create the controller
  - [x] Create the views
- Show the day's lessons
  - [x] Create unlevelled lesson partial
    - [x] Add vertical separator partial

## March 7th

- [x] Override WP styles on Online School custom text

### Materials

- [x] Change StandShowSpeak script attachment to guide for uniformity
- [x] Add subtypes to Exercise
- [x] Update seeds to generate lessons and a plan showing them on the current day for teachers
  - So I can just run `rails db:reset` to easily get lessons on the teacher profile
- [x] Write a rake task or some kind of script that takes a version label and automatically:
  - Changes the tag on the docker image in dockerrun.aws.json
  - builds a new docker image with that tag
  - uploads the image to dockerhub
  - runs eb deploy
  - with progress output at each step, and aborts on errors

#### Teacher Interface

- Show the day's lessons
  - [x] Create levelled lesson partial
  - [x] Tweak the teacher profile styling for mobile

## March 8th

- [x] Include kindy/ele modifiers in JS invoice calculation
  - And extract the modifier calculation to a helper
  - [x] Use that helper to fix related problems with multiple modifiers not displaying/adding correctly

### Materials

- [x] Add 'short_level' to Application helper to produce readable levels

#### Tests (for students)

- Questions are stored in JSON column, nested by 4 skills then question number and possible score
  - So maybe a hash of arrays?
  - When entering, each row should be a skill, then a colon and comma separated list of max scores for each question
- Loaded by a stimulus controller into a table where teachers can enter results and have percentages live calculate
- So need threshold to move up per test
  - When entering, level and percent needed
- Add tests & results
  - Add resource
    - [x] Test
  - Edit & test model/factory
    - [x] Test
      - [x] Test questions parsing
      - [x] Test thresholds parsing
  - Add seeds
    - [x] Test
  - Write a system spec for creating one
    - [x] Test
  - Create & test Policies
    - [x] Test
  - Create the controller
    - [x] Test
  - Create the views
    - [x] Test

## March 11th

### Materials

#### Tests (for students)

- Add tests & results
  - Add resource
    - [x] TestResult
      - [x] Add an 'answers' jsonb column to store their actual scores for each question
  - Edit & test model/factory
    - [x] TestResult
      - [x] Figure out that you need the :prefix or :suffix options to have enums with the same values
  - Add seeds
    - [x] TestResult
  - Write a system spec for creating one
    - [x] Write a JS-enabled system spec for calculating scores on Tests#index
  - Create & test Policies
    - [x] TestResult
  - Create result input table
    - [x] For each skill, fields are autogenerated for each question & max score displayed in header
      - [x] The inputs have min set to 0, max set to the max score
    - [x] Add autogenerated fields for answers to match questions on the test

## March 12th

### Materials

- [x] Review & merge Jayson's lang switcher PR
- [x] Make some changes to integrate it into the site
  - [x] Retain locale between pages by adding it to links as a default URL option
  - [x] Fix the locale breaking a bunch of system tests
    - Needed to set the locale in rails_helper since it's in the URLs by default now
  - [x] Infer locale if not provided
- [x] Remove vestigal files controller

#### Tests (for students)

- [x] Check answers are stored correctly when input
- [x] Display existing answers in form when they exist
- [x] Pass the JS enabled system spec for creating TestResults
  - [x] Entering all the scores for a skill displays the percentage for that section
  - [x] Entering all scores for a test shows the overall percentage and selects the suggested level from the select box
  - [x] Handle empty strings so NaN isn't displayed, set value to 0 if NaN

## March 13th

- [x] Updating time slots isn't working
  - Only on live
  - Lots of 'invalid form control is not focusable' errors in console when submitted
  - Other timeslots work fine
  - Pretty sure the problem is [that slot](https://kids-up.app/en/time_slots/3963/edit) is a special slot with no afternoon slot
     - So every time you try to edit it, the blank afternoon slot form is submitted and errors because it has blank required fields
     - It's a browser error becuase they're hidden and required
     - So maybe expand the afternoon slot by default if it doesn't exist?
     - And improve the blank filter on the accepts_nested_attributes_for
     - Also check errors for the afternoon slot are displayed at the top of the morning form, just to be sure
- [x] Merge child is also [not working](https://kids-up.app/en/users/4532)
  - This one gets a 406 response, so it's probably an issue with the respond_to block
  - It was actually a conditional in the controller which lead to nothing being explicitly rendered if there was no child found
  - which meant the action tried to render a default 'find_child' template, which didn't exist
  - thus the 406 response

### Materials

- [x] Add the actual language switcher SVG
- Shouldn't I just be using policy_scope to decide if a record can be accessed in pundit?

#### Tests (for students)

- [x] Create a validity controller to attach to each input which limits values to a valid range
  - Use the form validation API and attributes on the field to make it reusable for all form validations
- [x] Update student level when level check updates
- [x] Make results table header sticky

### Setsumeikai Calendar

- [x] Add prefecture filters under the search bar
- [x] Group schools by prefecture in the select box
  - Abandoned because Safari only added support for groupBy a few days ago

### [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [x] Add a 'prefecture' column to the schools table
- [x] Then start sending it to the Setsumeikai API and add it to the forms

#### HAML Refactors

- [x] merge children partial
- [x] add child partial

## March 14th

### Materials

- Shouldn't I just be using policy_scope to decide if a record can be accessed in pundit?

#### Tests (for students)

- [] Allow filtering results table by level
  - [] Also, in the controller, only fetch Ss who are currently in the level of the test
- Create results page/student profile
  - Should be able to print as a PDF

### Seasonal Site

### API

- Number of internal + reservation
- Number of external
- Internal + res revenue
- External revenue
- For parties just the total revenue

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
