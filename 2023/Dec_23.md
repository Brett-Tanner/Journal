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
- [] Why couldn't Leroy delete the auto-created options for that Saturday he made
- [] Invesigate what happens if you upload a new asset with the same key as an existing one
- [] Check for missing translations with `i18n-tasks`
- Write tests for Invoice#calc_cost to prepare for the rewrite
  - [] Snack price calculation
  - [] Extra cost price calculation
  - [] PDF creation (or at least that one is created)
  - [] Summary
    - Maybe just add some of these to the other, more specific tests to take advantage of the setup in those files
- [] Add button to generate photo service armband PDF for parties
  - Printable template with kids' names and a color which shows their photo status

#### Future Plans

- [] When importing the historical setsu/inquiries, try insert/upsert_all with record_timestamps: false to set our own created at
- [] In August 2022, RDS certificate [expires](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/UsingWithRDS.SSL-certificate-rotation.html#UsingWithRDS.SSL-certificate-rotation-updating). Will need to rotate to avoid connectivity issues.
- [] Move control of the domain from that Japanese site to Cloudflare
- Platform Upgrades
  - TEST ALL ON STAGING FIRST
  - [] Bump AWS platform version
  - [] Try bumping Ruby version to latest stable (can maybe install manually with a pre-deploy hook)

##### ActiveRecord

- Can use has_one on a has_many to single out a specific important record
  - [] Managed school
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
- Maybe use [#store](https://api.rubyonrails.org/classes/ActiveRecord/Store.html) on models with JSON, seems to give a nicer API
  - [] price lists
  - [] surveys
  - [] maybe email preferences
- Use SQL strings, or maybe hte active_record_import gem to update children

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

##### Views

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

### Personal Project - [Budgeting Site](https://github.com/Brett-Tanner/budgeting-site)

- Features

- [] wire the upload form up to submit to
- [] an endpoint to create DB records
- [] Auto-categorize based on rules
  - [] Add rules table
- [] If transactions are uploaded for last day already in the DB and they have the same amount, ask if duplicates
  - [] If uploaded for any time prior to the last day in the database, just ignore them

### Work Project - [Games Site]()

- [] Avatars
  - Can customise with points earned from games
- [] Matching game
  - Toggle numbers on the cards
  - Show heat gauge/points earned on right
  - Play audio of the word when clicked? (Audio file size might be an issue)
