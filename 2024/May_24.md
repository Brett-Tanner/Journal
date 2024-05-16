# May 2024

## May 8th

- [x] Sort out new AM areas
- [x] Manually get summary stats for last 2 events

### Materials

- Handle daily attendance in the LMS?

#### CSV Upload

- Displays overall status as sticky heading at top, moves between checking, uploading, done
  - [x] Also track totals for pending, failures, successes
    - Use a separate Stimulus controller on the turbo response whose connect action updates the count appropriately

## May 9th

### Documentation

- Lessons
  - [x] Inheritance
  - [x] Guide generation
  - [x] Form construction

### Lessons

- Tweaks to warning box on DA PDF
  - [x] Round box border
  - [x] Add padding
- [x] Use correct ShingMGo
- [x] Remove unused `includes` from PDF generation
- [x] Update PDF generation tests to be less specific
- [x] Actually use S3 for file storage
- Sort out permissions for the app to upload files
  - [x] Worked with Yamamoto-san to rule out IAM permissions issue
  - [x] Roll back to using local storage so Luis can actually test stuff
- [x] Try setting up swap space again
  - [This one](https://repost.aws/knowledge-center/ec2-memory-swap-file) works fine while the instance is running, unsure if works when restarted though
  - [x] Try seeing if it persists after modifying dockerrun to use a swap file and deploying
    - It does, not 100% sure the container is using it but the swap file is there after a new deploy
- Research possible solutions to Aws::S3::Errors::AccessDenied (Access Denied)

## May 10th

- [x] Attempt to add new version of the dumb tracking thing
  - Script they gave me does nothing
  - Might create a script tag loaded from their servers that does something?
  - But I want an explanation at least before running arbitrary code from someone else's server

### Materials

#### CSV Upload

- [x] Modify system spec setup to pass
- Write response templates
  - [x] Update
  - [x] Make the error forms submit to the correct endpoints for them to function
  - [x] Get a form in a table row to work correctly
    - Had to put it in a cell and reference the form with the `form` attribute on inputs
  - [x] Troubleshoot possible incorrect 'student already taken' error
- [x] Add a dropdown to the nav that lets you select the type of upload
- Teachers
  - [x] Write system spec

## May 13th

- [x] Set up production summary API for Paolo

### Materials

#### CSV Upload

- [x] Troubleshoot flaky upload tests when running multiple together
  - It was because I had `#create_csv` defined for each, so they were overwriting each other in non-deterministic ways
  - Causing the test CSVs to not be created, or the wrong one to be created at the wrong time
  - [x] Refactor the CSV creation code to just be part of `#create_{}_csv`
- [x] Fix tests not running the request JS, so full flow can be tested
  - Was because the test was generating a CSV with a bunch of fields not used by the controller, was messing something up either with the data being sent or in the controller
- [x] Teachers
  - [x] Refactor system spec to not interfere with other upload tests
  - [x] Test & write TeacherPolicySpec
  - [x] Create controller/views
  - [x] Create Stimulus controllers for teacher upload
  - [x] Fix a bug caused by relying on potentially blank fields for tubro dom ids
  - [x] Fix a bug caused by sending the (JS) index of the upload as an attribute of the record being uploaded
- Parents
  - [x] Write system spec
  - [x] Test & write ParentUploadPolicySpec

## May 14th

### Materials

- [x] Bump Ruby version to 3.3.1
- [x] Include `csv` in Gemfile since it's out of stdlib from 3.4.0

#### CSV Upload

- [x] Parents
  - [x] Create controller/views
  - [x] Refactor Stimulus controllers
- [x] Seems there's actually an issue with student uploads, chase that down
  - Might be why it's the only one whose tests don't pass the whole way through
    - Wasn't, that's still a problem
  - Was a typo, using 'hidden_field' rather than 'hidden_field_tag'

### Event Site

- Dockerize
  - [x] upgrade to Ruby 3.3.1
  - [x] Customize Dockerfile to build successfully

## May 15th

### Materials

#### CSV Upload

- [x] Add school creation link to Org page & make title of the table a link to the full school index

### Event Site

- Dockerize
  - [x] Customise docker-compose.yml to run the whole app successfully
    - Up to the S3 SDK causing issues with docker-compose
  - [x] customise .dockerignore
  - [x] take a look at the entrypoint, and config/dockerfile.yml
- Add wiki notes on getting docker-compose working locally
  - [x] .env files and contents
  - [x] DB setup required & how to do it
    - e.g. creating the DB, migrating, adding a user to log in with
- Add wiki notes on transferring domain
- [x] Try getting dockerized app running on KU account
  - IT WORKED FIRST TRY! Just remember to add an S3 bucket name or it'll crash
- [x] Backup the DB in every way possible
  - Copied latest snapshot, figured out how to share, will export to S3 tomorrow morning
- [x] Switch the domain registrar to Cloudflare

## May 16th

- [x] In setsu calendar, auto select the school they're attending the setsu at as the default one they're interested in on form

### Event Site

#### In-office tasks

- [x] Resize swap space because there's not room to pull docker images lol
- IT WORKED FIRST TRY! Just remember to add an S3 bucket name or rails server will crash
- [x] Try creating an S3 bucket specifically for each app
- [x] Share the latest RDS snapshot with the P-UP account
- [x] Spin up a new version with the shared snapshot on the PUP account and get it working
  - [x] Verify accounts still exist and are accessible
- [x] Set up eb CLI for new server
- [x] Reinstate Leroy as online SM

## May 17th

### Materials

- [] 500 error on org page is caused by not having a plan, so when you try to call name on nil it crashes

#### CSV Upload

- [] Include correcting an invalid record in upload system specs

### Event Site

#### In-office tasks

- [] Figure out why the temp URL won't work with the setsu calendar on live but will in dev
- [] Figure out the S3 permissions issue, then:
  - [] Once it's working, point the setsumeikai calendar at the new version temp URL
  - [] Also change the GAS sheets URLs to point at the new version temp URL
  - [] May need to reupload all the images that were on S3
- [] Point the domain at the new URL with a CNAME record
- [] IP lock SM accounts
- Extras if I have time
  - [] Maybe install SolidQueue and use it for emails
  - [] Maybe finish the invoice calc rewrite if I have extra time
  - [] Refactor the Event#show page and move it to Invoice#new
- [] Need to add event summary stats to the charts
- [] Login isn't showing an error when it fails

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
