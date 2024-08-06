# August 2024

## August 1st

- [x] Get list of parent emails who've made a booking but didn't pick photo service
  - [x] Enable parents to register for just photo service
  - [x] Fix tests relating to event options
- More new activities
  - [x] Futamatagawa
  - [x] Monzen
  - [x] Shin-urayasu

### LMS

- [x] Use host whitelist for video tutorial uploads
- [x] Remove the image component code from pdf_imageable
  - [x] rework into ImageValidatable concern
  - [x] Update the models that use it
- Add the actual backgrounds
  - [x] DailyActivity
  - [x] Exercise
- [x] Use the new image component in other plans
  - [x] And in the image page component
- [x] Add PDFBackground component
- [x] Switch the Keep Up/Specialist icons
- [x] Drop speaking from tests/results
- [x] Bring the locale toggle back for lesson view

## August 2nd

- More new activities
  - [x] MinamiMachida
  - [x] Kamata
  - [x] Omori
  - [x] Shinkawasaki
- [x] Fix kids being unable to register because of the orphan option check trying to access `registerable` on a hash
- [x] Add Daniel's activity attendance count by school table
  - [x] Haml refactor of activities chart page

### LMS

- [x] Add a 'Regenerate Guides' button for each lesson type (just me for now)
- [x] Add Exercise back to the list of types which skip generating guides for the moment
  - [x] Temporarily remove PDF expectations from tests
- Github issues
  - [x] #64 Writers can't propose changes to at least lesson 354, form just resets with no errors
    - was because it was trying to add phonics resources by an attachment that was already in use on the main lesson
    - solved by making the existing phonics resource attachments nil if a writer
    - [x] Also ensured phonics resources and resources are copied from proposal
    - [x] And extracted a comparable lesson partial
  - [x] #66 test form not in main element

## August 5th

- [x] Diagnose & solve issues caused by mysterious disappearance of Shinjo photo service option
  - [x] Fix the affected invoices so they're registered for the new one
  - [x] Prevent options being deleted if registered for (but only with destroy)
  - [x] Figure out how the heck the option got deleted in the first place
    - If you call #delete(record) on an AR relation, it deletes it from the DB, not the relation
- [x] Add the new photo service icon

### LMS

- [x] Remove ability to edit course_lessons/resources through course form, is insanity
- Github issues
  - #67 scope tests to organisations/courses somehow
    - [x] Modify test scope to go thru course for school staff
      - [x] Update seeds to take it into account
      - Will want to only see current or past tests

## August 6th

### LMS

- Github issues
  - [x] #67 scope tests to organisations/courses somehow
    - [x] Add accepts_nested_attributes to the form/controller/model for Test
- Calendar page
  - [x] Add a `#week_lessons` method to courseable
  - [x] Controller & view scaffold
  - [x] Make the lessons clickable buttons that reveal the lesson modal
  - Styling
    - [x] Columns/headers

## August 7th

- [] Migrate all exercises to 'All levels' before deploying new version
  - [] Check no issues
- [] Need a separate column for food allergy, boolean
  - Talk to leroy about it
  - [] After Summer School, change it so allergy kids can't see the option for lunch
  - [] When merging children the food allergy or not needs to be copied
  - [] When finding by SSID, make them select food allergy or not in addition to first seasonal or not
  - Set by a radio button
  - Parents get a splash on their page & kid's page telling them to update, redirected if they try to register
- [] Try switching on force.ssl for both sites
- [] Look into setting up emails for our new domains
- [] SMs need a test school on event site for training
  - Will need to exclude it from the real scope

### LMS

- Calendar page
  - Styling
    - [] Row headers
    - [] Lesson buttons
  - [] Add the key popover
    - Try popover API
  - [] Create a shared org nav
    - [] Add the org nav to other places it could be used
  - [] Add a way for the calendar buttons to go straight to the requested level
- Notifications
  - From listening to podcasts these can often be different types with STI, if we even need that much complexity
  - I think I want to just store them as JSONB on the User record, delete them once seen if they exceed a certain number
  - [] Manually send notifications to subsets of people
  - [] When lessons haven't been updated in 2 years
  - [] When there are new (relevant) support messages
- [] Add organisation ID to kids
  - [] Form and strong params too
  - [] And migrate the existing ones
- [] Fonts might look weird cos I'm just making them bold, not using the actual bold version
  - A guy on the Syntax podcast mentioned this mattered
- [] Add a UI for viewing/rolling back to previous versions of students
  - [] Remove limit on versions of students stored
- [] Might need to reverse the lesson form/fields relationship at some point, partial locals are an issue
  - Noticed this on phonics class, with the associated phonics resources
- [] Delete the 'LessonUses' controller and move it to CourseLessons#index, since that's what it really is
  - [] See if there's anything stopping me just using a CourseLesson form, rather than `fields_for` in a form
  - [] Add the date fields and CourseLesson update/create actions to enable adding lessons to courses easily
- [] When updating upload progress, decrement failures if sum of all > total

#### Jayson Stuff

- [] Add event lessons
  - [] They're gonna need an attached image to display
  - [] Use the cards for teacher lessons as a template, same basic layout too
  - Can probably be handled by same controller?
  - [] Style to match Alex's mockup
- [] Implement the lesson calendar
  - Probably its own controller
  - [] Needs a link on the teacher nav, using the calendar svg
  - [] Style to match Alex's mockup
- [] Add announcements
  - [] Will need a message, validity period, maybe a link
  - [] Shown conditionally based on User attributes, preferably only attributes w/out joins
- [] Provide a summary of kid's test results per test, like the input view but minimal, maybe sorted by the level they moved to and just showing name/prev level/score
- [] Add a category resource for evening class, resource types are conversation cards and actvities
- Automatically (for kidsUP):
  - [] Create default teacher and class when new schools create
  - [] Add uploaded students to their school's default class
- [] Add reviews to lessons
  - [] Need stars and text
  - [] Text pops up after star rating given
  - [] on the teacher_lesson modal
  - [] Button on the lesson page to mark all reviews acted on, they won't count to the current score
    - Maybe show the score for active reviews and all? And have an index with all of them

### Event Site

- [] Document refactored invoice calculation
- [] Need to add event summary stats to the charts
- Extract PDF generation into a concern
  - [] Generate it in a SQ job when the invoice is modified
    - [] And make it available to download from the invoice partial
  - [] Refactor to use the cost info object
- [] Login isn't showing an error when it fails
- [] Refactor the Event#show page and move it to Invoice#new
- Can do a lot of stuff with cron/background jobs/APIs
  - [] Sync the day's invoices to the new SS in the AM
  - [] Grab a student's test results as JSON to show in the seasonal app

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
  - [Useful article](https://headey.net/rails-assets-active-storage-and-a-cloudfront-cdn)
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

### SS Replacement

- We need an electronic version of the new student application form
  - Maybe prefill behind a PIN
  - Could use the PIN field on event site users for that
  - Have an open, blank one anyone can use
  - Multi-stage? With stage by stage validations
