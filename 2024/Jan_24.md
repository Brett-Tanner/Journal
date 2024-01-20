## January 4th

### Setsumeikai Calendar

- [x] Do the switch

### [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [x] Fix up some mising info on Schools/a missing SM
- [x] Add the 3 course to price lists
  - [x] Change the model
  - [x] Change the forms
  - [x] Push, then add the 3 course
  - [x] Change the code in Invoice#calc_cost

## January 5th

### [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Make other associated modifications to the costs
  - [x] Default lunch & dinner options from 660 > 770
  - [x] Repeater discount is now for 5 or more registrations, not 10
  - [x] There's now a 1 course (officially, price changed as well)
    - Ele and kindy pay same for the new 1 course, so no more pointless price
- Add close_date field to TimeSlot, saves me having to edit the hash every event
  - [x] Add & run the migration, push
  - [x] Add close_at tests
  - TDD kindy/ele modifiers
    - [x] Add the code to use them in calculations

## January 9th

- [x] Finish outline for Leroy
- [x] Alter WP site page slugs to match seasonal school ids
- [x] Edit WP theme templates to produce a URL in the correct format

### [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [x] Add temp exception to repeater discount being 5 till all SMs do their job
- [x] Let SMs delete inquiries since customers seem to like sending multiple
- [x] Fix an error where I was using the sum on every iteration when reducing the extra cost, regardless of whether it applied
- [x] Remove links to setsu/inquiry stuff from SM profiles
- Add close_date field to TimeSlot, saves me having to edit the hash every event
  - TDD kindy/ele modifiers
    - [x] Test their inclusion in the summary
  - [x] Show kindy/ele modifiers where extra cost is shown (as extra cost)
  - [x] Add form fields to actually set the values

#### HAML Refactors

- [x] TimeSlot event form
- [x] TimeSlot#event_slot_fields

## January 10th

### [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [x] Realise I'm missing policy/request tests for charts and write those
- [x] 'All/Area schools' for surveys is broken, individual schools fine
  - Was breaking due to children without parents, couldn't display phone/email for nil
  - Can end up with parentless children when merging, since the responses aren't copied and they prevent the SSIDless child being deleted
  - Added safe navigation, and copied survey responses during child merge
- [x] Bump Puma to 6.4.2 to avoid request smuggling vulnerability
- [x] Add English translations for Stats categories
- [x] And why none have been sent to GAS
  - They are being sent, but GAS isn't updating send_flg. No dupes so fine for now I guess
- [x] Let statistician see setsu/inquiry stats
- [x] When AM/Admin clicks on a school to view Setsu stats for, still shows all schools
  - [x] Add requested graphs (separate for held/created setsu, inquiry category pie chart etc.)
  - [x] Remove null from referrer pie chart
  - [x] Limit inquiries per setsumeikai to setsu inquiries
- [x] List events they apply to under price lists
  - [x] And in the edit view
- [x] Disallow blank survey response submissions

#### HAML Refactors

- [x] Charts#setsumeikais
- [x] PriceList partial
- [x] PriceList#index
- [x] PriceList#edit
- [x] PriceList#new

## January 11th

### [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [x] Adjustments snuck into the middle of the summary, put them back on the left edge
- [x] Figure out why/how there are inquiries for Online
  - It was because I also made them Ikebukero SM for some reason, was getting their inquries as well
  - Also had an issue with the inquiry index erroring because Online isn't a real school, so made default school the managed school
- [x] Do a run through of creating Spring School in dev env, check all the views etc. work with 2 events
- [x] Finish off the time slot edit form that got lost yesterday
- [x] Show multiple events on child/parent pages if available
- [x] Create Spring School
- [x] Manual adjustments to special arvo snacks and arvo close_at

#### HAML Refactors

- [x] TimeSlot#edit

## January 12th

To fix the rubocop linter in nvim using the wrong version, change the lsp setup like this:

```
require("lspconfig").rubocop.setup({
  cmd = { "/home/brett/.rbenv/shims/rubocop --lsp" },
})
```

- [x] Birthday/grade mapping was off because not using April as start of year or taking current date into account
- [x] Auto-scroll to top wasn't happening on Setsu form summary because pathname didn't change
  - So changed the useEffect dependency to the whole location object, which does change because of the hash

### [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [x] Modify auto afternoon creation to use the same close at as the morning, rather than the default
- [x] Sort events by school id within start date on index

##### Testing

- [x] Create copy of Spring school in my (desktop) local dev environment

## January 15th

### [Materials](https://github.com/Brett-Tanner/materials)

#### Documentation

- Create user stories for
  - [x] External teacher
  - [x] External manager
  - [x] KU teacher
  - [x] KU curriculum
  - [x] KU sales
  - [x] KU admin
- [x] Make & embed a quick outline of the DB schema

### [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [x] Filter inquiries by setsumeikai/general
- [x] Add auto-unsubscribe button to emails to meet gmail/yahoo requirements

## January 16th

### [Materials](https://github.com/Brett-Tanner/materials)

#### Views

- Scaffold course views

  - [x] Index
  - [x] Course table partial
  - [x] New/Edit
  - [x] Form partial
  - [x] Show

#### Files

- [x] Add basic uploads
- [x] Add basic downloads
- [x] Add breadcrumbs
- [x] Add ability to make new folders
- [x] Implement uploads to current folder
- [x] Add navigation back to previous folder
- [x] Add navigation forward to nested folders

## January 17th

- Set Jayson up with an AWS account for his Elastic Beanstalk
  - [x] Invite his personal account
  - [x] Then cancel that, bad idea
  - [x] Make him get a new account just for work
- Add a search to the school index on main site
  - [x] Write basic JS to hide/show results
  - [x] Basic HTML for the form
- [x] Endless meetings
- [x] Talk out a basic structure for lessons with Daniel, took pictures of the sketches

### [Materials](https://github.com/Brett-Tanner/materials)

- [x] Bump to Rails 7.1.3

### [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [x] Add the event_summary table to one of the charts views

## January 18th

### [Materials](https://github.com/Brett-Tanner/materials)

- Files controller is now just a file explorer rather than primary method of access/storage, so decouple from courses
  - [x] Add index action that lists all course folders
  - [x] Decouple all the partials from reliance on course_id
  - [x] General cleanup of code quality in those views/controllers

#### Lessons

- Model for each category, all inheriting from a base class
  - Base class has title, summary, category, week, day, references a course and has attached materials (attached files)
  - Start with daily activity & exercise
    - Links and steps for both as array column
    - Each have different subcategory enums
- Has to be backed by a single database table so it can be referenced from other tables
- Each model can generate a PDF plan from a template

- [x] Create & test base Lesson model
- [x] Add a basic main nav
- [x] Write a system test for creating a DailyActivity lesson
- Pass that test by:
  - [x] Adding the role enum to User
  - [x] Creating a migration/model/factory for Organisations so Users can be associated with them
  - [x] Adding steps and links columns to Lesson
  - [x] Creating the DailyActivity model & testing its validity
  - [x] Fiddle with rails_helper for a while to get system tests running with Rack::Test, not selenium
  - [x] Correctly subclass DailyActivity from Lesson, and reorganise folders to match
  - [x] Add an 'Add lesson' dropdown to Course#show
  - [x] Create controller actions for DailyActivity creation
  - [x] Make day an enum on Lesson so we have human readable days mapped
  - [x] Create views for DailyActivity creation

## January 19th

### [Materials](https://github.com/Brett-Tanner/materials)

- [x] Long meeting to get Jayson set up with organisation AWS account
- [x] Set up an SCP so he can only access EB
- [x] Stop pretending the 1 course is spot use on invoices
- Main site tweaks
  - [x] Limit month range to next 2 months
    - [x] Write tests
    - Can do with validRange prop to calendar component
    - Takes start and end arguments in form 'YYYY-MM-DD'
  - [x] Add month title/navigation to footer as well as header
  - [x] Scroll to top of calendar when month changes
- Realise Rails has built in STI support and try using that
  - [x] Rename category enums to a 'type' string column
  - [x] And subcategory to subtype
  - [x] Add inclusion validations to compensate for the removal of enums
  - [x] Update tests if needed
  - Had quite a few issues compared to using the enum I had set up already
  - Will need to look into it properly and weigh pros/cons

## January 20th

### [Materials](https://github.com/Brett-Tanner/materials)

- [x] Switch to Rails' built-in STI
- [x] Add #split_on_capitals to Applicationhelper
- [x] Split shared lesson form fields into their own partial
- [x] Create Exercise model/form

## January 22nd

- [] Finish off the search functionality for the main site school index

### [Materials](https://github.com/Brett-Tanner/materials)

#### Lessons

- Write a system test for creating a DailyActivity lesson
- Pass that test by:
  - [] Creating Lesson#show action/view and daily_activity partial

#### Files

- [] Can use the 'accept' attribute of file fields to limit filetypes which can be uploaded
  - Maybe set automatically with constants on the relevant model

### [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

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

#### HAML Refactors

- []

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

### [Setsumeikai Calendar](https://github.com/Brett-Tanner/setsumeikai_calendar)

- Add online trial lessons to setsu registration form
  - [] Make it possible to edit Online's school info
  - [] Add the necessary info
  - [] Send that info in API responses
  - [] Add SM accounts (if necessary) for Online
