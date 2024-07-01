# July 2024

## July 1st

- [x] Wildcard Futamatagawa SM and schedule time to fix tomorrow
- [x] Identify & fix missing snack for special day afternoon
- [x] Change some kid's name for Kamata SM
- [x] Add document submission form to the event site
  - [x] Create controller/routes
    - Email sent to SM on submission
      - [x] Create DocumentUpload mailer
        - [x] And spec
        - [x] And preview
      - [x] Basically just says 'a {category} document has been submitted' with a link to the index
  - [x] Create views
    - [x] Create policy, scope & tests for index
    - [x] Index is table with all the details accessible by SM of school submitted to, AMs
      - [x] Create or re-use the nav to filter by school
    - [x] Figure out a way to show the signed in nav bar on index rather than signed out
      - Split into unathenticated layout explicitly used in controller
    - [x] Add KU logo to new form like for new sign ups
    - [x] Give admins/SMs/AMs a button to access the index
    - [x] Translations for index & form/new
- Need some way of doing the early bird discounts for parties
  - They could be different per school
  - Some schools (new ones) can do free events
    - Just add a separate 0 cost price list for that event
- [] Try switching on force.ssl for both sites
- [] Look into setting up emails for our new domains

## LMS

- [x] Add temp drawing SVG
- [x] KindyPhonic has lesson plans, the button is highlighted but no link to download
  - Since I'm rendering both PhonicsClass & KindyPhonic in that col, it was overlapping and preventing the link from being clicked
- [x] On category resources, the table headings are just the category now rather than the resource type
- [x] Try sorting kids on test result page with Ruby since AR doesn't want to help
- [x] Missing English translations for user roles in the support messages
- [x] Find where I haven't translated school names & add the translation call
  - Also correct 'Ikebukuro'
  - I'll do most of this as I see missing translations I think
- [x] Move some stuff out of the admin nav into an 'Admin tasks' card
  - [x] Tidy up plans index/show since we actually link to it now
- [x] Deleting a newly added phonics resource in the form stops you submitting the form
  - Probably something going wrong with the fields controller cleanup
  - Was checking if the lesson was a new resource, not the PhonicsResource
  - Led to the wrong cleanup logic being used

## July 2nd

- Identify & fix missing snack for special day afternoon
  - [] Get a list of all the affected students
  - [] recalculate their invoices
  - [] Send the lists of affected students to the SMs
- Need some way of doing the early bird discounts for parties
  - They could be different per school
  - Some schools (new ones) can do free events
    - Just add a separate 0 cost price list for that event
- [] Try switching on force.ssl for both sites
- [] Look into setting up emails for our new domains

## LMS

- Add a CSVExportsController to dump the data from various tables for export
  - Will need to check what gem I used for the event site, that one's fast
  - [] Create policy & tests
  - [] Controller & views
- [] Monthly list of materials by lesson
  - Just a list of lesson titles and the materials they need for now
  - Later on think about automatically generating the full list for a month
  - Monthly materials controller
- [] Add kana names to students
- [] In Safari, exporting the lesson plan to PDFViewer downloads the login page instead
- Attempt to reproduce Luis' issue with EnglishClass topics not saving #56
  - Couldn't reproduce, waiting on a video from Luis
- [] Allow organisations to have multiple courses again
  - [] Only show teachers the ones that've started
- [] Add a weekly/monthly calendar view of missing lessons
  - Probably a method on the course that grabs all the course lessons and checks for missing based on weeks/days
  - Might also want to check for dups
  - [] Notify if upcoming missing lessons from a cron job
- [] Automatically:
  - [] Create default teacher and class when new schools create
  - [] Add uploaded students to their school's default class
- [] Add a UI for viewing/rolling back to previous versions of students
- [] Might need to reverse the lesson form/fields relationship at some point, partial locals are an issue
  - Noticed this on phonics class, with the associated phonics resources
- [] Provide a list of kids who could move up for each test
- [] Delete the 'LessonUses' controller and move it to CourseLessons#index, since that's what it really is
  - [] See if there's anything stopping me just using a CourseLesson form, rather than `fields_for` in a form
  - [] Add the date fields and CourseLesson update/create actions to enable adding lessons to courses easily
- [] When updating upload progress, decrement failures if sum of all > total
- [] Refactor the PDF generation
  - The endless 'draw\_\_\_\_' methods seem like they could be extracted
  - Probably different versions for plaintext, lists and links
- [] Replace icons for aerobics, dance and jumping exercise subtypes when I get them
- [] Add a 'quit_chance' enum to students, next to the comments section
  - Revisit after SS meeting to decide what the enum values will be
- Implement notifications
  - [] When lessons haven't been updated in 2 years
  - [] When there are new (relevant) support messages
  - [] Manually send notifications to subsets of people
- [] Use Flipper for feature flags

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
