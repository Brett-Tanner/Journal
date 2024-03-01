# March 2024

## March 1st

- [x] Actually apply the CoursePolicy to requests -__-
- [x] Rename ca/aa/_id/name to admin_approval & curriculum_approval, completely unreadble if you haven't worked on them in a while
- [x] Give Luis a button to actually add new lessons from the index
  - Probably turn the existing dropdown into a partial
  - [x] And make it pretty
- [x] Create the online-specific setsu inquiry email
- [x] Add oddities section to Setsu Calendar, so far just includes the hardcoded order array
- [] Define an ATTRIBUTES constant on each lesson type, use it in strong params on controllers/proposed changes controller anywhere else it might be useful
  - Handy for tracking the attributes each lesson uses in the actual code rather than a lucidchart embedded in the wiki
- [] Write a rake task or some kind of script that takes a version label and automatically:
  - Changes the tag on the docker image in dockerrun.aws.json
  - builds a new docker image with that tag
  - uploads the image to dockerhub
  - runs eb deploy
  - with progress output at each step, and aborts on errors
- [] Look into the Normalize API for data that needs massaging

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
  - [] Both can have the user association nullified, so handle that possiblity in the views

#### Teacher Interface

- Match their profile to Louis' wireframe/Alex's designs
  - Navbar
    - [x] Style to match the design
    - [x] Highlight the current link
    - [x] Add subtitle

## March 2nd

- [] Define an ATTRIBUTES constant on each lesson type, use it in strong params on controllers/proposed changes controller anywhere else it might be useful
  - Handy for tracking the attributes each lesson uses in the actual code rather than a lucidchart embedded in the wiki
- [] Write a rake task or some kind of script that takes a version label and automatically:
  - Changes the tag on the docker image in dockerrun.aws.json
  - builds a new docker image with that tag
  - uploads the image to dockerhub
  - runs eb deploy
  - with progress output at each step, and aborts on errors
- [] Look into the Normalize API for data that needs massaging

#### Sales/OrgAdmin

  - [] Both can have the user association nullified, so handle that possiblity in the views

#### Teacher Interface

- Match their profile to Louis' wireframe/Alex's designs

#### Courses

- Course price is per student, so need an easy way to calculate that
- Needs to have a week from on the plan so they can't see stuff from before the week they started paying
- [] Only show a month in advance of lessons by default as its paid by month
  - Probably need a field for months paid on the plan

#### Students

- Update student level when level check updates
- Student limit on the plan as we're charging by student
  - They can only add students up to the limit

### [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [] Redirect or bounce emails to the automated email address

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
