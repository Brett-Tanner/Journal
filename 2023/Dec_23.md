# December 2023

## December 1st

### [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Write tests for Invoice#calc_cost to prepare for the rewrite
  - [x] Automatic adjustments
  - [x] Manual adjustments
  - [x] Basic registrations tests (including dup protection)
  - Option price calculation
    - [x] Slot options

## December 4th

### [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Write tests for Invoice#calc_cost to prepare for the rewrite
  - [x] Output full test details by default
  - Option price calculation
    - [x] event options
    - [x] calc_cost itself and its arguments/guards
    - [x] callbacks like auto-calc on save and auto moving registrations to a new child
    - [x] price lists

## December 5th

### [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Remember debug() is a helper in views, formats and YML and displays in pre tags

- [x] Why couldn't Leroy delete the auto-created options for that Saturday he made
  - Was the empty fields for the afternoon slot; they were trying to create a new one and obviously the validation failed
  - Added a reject_if: :name_blank? to the options
  - :all_blank wasn't working cos I had default values like `morning: false` set which the form was submitting
- [x] Move form errors into a haml partial
- Can use has_one on a has_many to single out a specific important record
  - [x] Managed school - doesn't work for this, can't use it on :through tables. My existing instance method is fine.

## December 6th

### [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- [x] Fix the logic error in the event partial which directed parents to the attendance sheet
  - [x] Also switch Invoice#index to haml
  - [x] Extract child/parent partials from Invoice#index
- [x] Check Pundit policies inherit from ApplicationPolicy, which is all false by default
- [x] Check I included Pundit in ApplicationController
- [x] Check whether I handled redirect to profile by overriding `after_sign_in_path` in Devise
  - I did for `after_sign_out_path`, not for sign in though
- [x] Figure out why Pundit didn't stop parents following the attendance link anyway
  - There was a scope on the main index action, but not the attendance associations
  - They had been using authorize, but I removed that

##### Pundit

- Enforce pundit on all controllers one by one with `after_action :verify_authorized` and `after_action :verify_policy_scoped`
  - [x] Children
- Fix any weird authorization logic I find
  - Children
    - [x] Make child_policy scope actually return children, not schools
    - [x] Authorize ChildrenController#event_attendance & #slot_attendance with Event & Slot policies respectively
    - [x] Clean up unnecessary params, user and record are available implicitly to every method
- Write tests for every Pundit policy (should now be every action on every controller)
  - Unit tests for policies
    - [x] Children
  - Unit tests for policy scopes
    - [x] Children

## December 7th

### Setsumeikai Calendar

- [] Add margins (but only on school list component) to align root with the images below
- [] Add margin to top of root for separation from page text
- [] Use flex-start on the school list
- [] Change referrer options to match those in this [pdf](https://drive.google.com/file/d/1zD98bm_XZo0jNP4DQu5FJT9BDR0y5i_B/view)

### [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Remember debug() is a helper in views, formats and YML and displays in pre tags

- [] Overwrite the sign in path properly as well
  - Can use `stored__location_for` to redirect to originally requested page
- [] Uncomment `config.force_ssl` in production, we're already redirecting to HTTPS and the other stuff is good
- [] SMs should be able to edit their school's data
  - [] JSON validations from Rails Way
  - [] Pundit permissions
- [] Add button to generate photo service armband PDF for parties
  - Printable template with kids' names and a color which shows their photo status

#### Future Plans

- [] Investigate what happens if you upload a new asset with the same key as an existing one
- [] When importing the historical setsu/inquiries, try insert/upsert_all with record_timestamps: false to set our own created at
- [] In August 2022, RDS certificate [expires](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/UsingWithRDS.SSL-certificate-rotation.html#UsingWithRDS.SSL-certificate-rotation-updating). Will need to rotate to avoid connectivity issues.
- [] Move control of the domain from that Japanese site to Cloudflare
- Platform Upgrades
  - TEST ALL ON STAGING FIRST
  - [] Bump AWS platform version
  - [] Try bumping Ruby version to latest stable (can maybe install manually with a pre-deploy hook)

##### ActiveRecord

- Maybe use [#store](https://api.rubyonrails.org/classes/ActiveRecord/Store.html) on models with JSON, seems to give a nicer API
  - [] schools
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
- [] Look into using [query logs](https://api.rubyonrails.org/classes/ActiveRecord/QueryLogs.html) for a better idea of where slow SQL is coming from
- validates_acceptance_of creates a virtual attribute which must be true for the record to be saved
  - [] add to User for backend validation of privacy policy
- You can chain a list of validations on a single column, like `validates presence: true, uniqueness: true ... etc.`
- Look into [delegated types](https://api.rubyonrails.org/classes/ActiveRecord/DelegatedType.html)
  - [] especially for splitting the mess of user logic into more manageable chunks
- Use SQL strings, or maybe hte active_record_import gem to update children

##### Pundit

- [] Enforce pundit on all controllers one by one with `after_action :verify_authorized` and `after_action :verify_policy_scoped`
  - [] Adjustments
- Fix any weird authorization logic I find
  - Children
- Write tests for every Pundit policy (should now be every action on every controller)
  - Unit tests for policies
    - [] Adjustments
  - Unit tests for policy scopes
    - [] Adjustments
  - Request tests for controllers (to check for 401's when not authorized)
    - [] Children
    - [] Adjustments
  - [] If I can figure out a way, shared example that checks authorize called on every non-index action and policy_scope called on index
    - Maybe doable by just testing each route responds with something since we're using `after_action :verify_authorized`
- Pundit can do [strong params based on role](https://github.com/varvet/pundit#strong-parameters), which I definitely wanted for some stuff

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

##### Testing

- Devise gives you handy helpers `sign_in` and `sign_out` which take an instance of user
- Write tests for Invoice#calc_cost to prepare for the rewrite
  - [] Snack price calculation
  - [] Extra cost price calculation
  - [] PDF creation (or at least that one is created)
  - [] Summary
    - Maybe just add some of these to the other, more specific tests to take advantage of the setup in those files
- [] Create `rails predeploy` task to run all the tests and brakeman prior to deployments

##### Views

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

### [KU-Wiki](https://github.com/Brett-Tanner/KU-wiki)

- [] Add 'How to contribute'
  - [] Adding a page
  - [] Adding a section
- [] AWS section
  - [] Pushing a new version
  - [] Services we use and overview of what for
- [] Rails section
  - [] Overview
  - [] Useful Commands

### Work Project - [Games Site]()

- [] Avatars
  - Can customise with points earned from games
- [] Matching game
  - Toggle numbers on the cards
  - Show heat gauge/points earned on right
  - Play audio of the word when clicked? (Audio file size might be an issue)
