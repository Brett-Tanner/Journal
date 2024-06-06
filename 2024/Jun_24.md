# June 2024

## June 3rd

- [x] Start cron job article on wiki
  - Set one up to sweep SQ jobs older than a week
    - [x] For LMS
    - [x] For event site
  - [x] One to get PGHero stats
    - Requires messing with RDS settings so skipping this one
- [x] Copy docker_entrypoint from event site
  - Tried but failed, I think an issue with the file extension? It looked different without a \* but adding one failed the deploy
  - Just trying it without the extension this time

## LMS

- [x] Bump propshaft to 0.9
- [x] Make the test result entry table at least readable with new styles
- Add level SVGs where appropriate
  - [x] Organise assets/icons into folders without breaking anything
  - [x] On teacher profile
- [x] Improve levelled lesson styling & add KeepUp/Specialist
- [x] Add a level_icon helper for lessons
  - [x] And refactor the icon_filename method out into a helper as well
- [x] Only allow PDF uploads for lesson guides
- Address Github issues
  - [x] Add separate columns for en names
  - [x] Add kindy row to levelled lessons

## June 4th

- [x] Only show the "don't select regular days" message to internal students
  - [x] Extract child switcher to a HAML partial
  - [x] Chase down potential 'copy_regs' issue
    - Was just because all the slots were closed on test event
- [x] Add a 'wildcard' carveout to the SM IP check so we can make sure we always have the ability to give them access
- [x] Add GTM to main layout and remove the page-specific tags
  - [x] Remove the Clarity tags
  - [x] And fix BS validations not applying on turboload
- [x] Chase phantom 'Allergy not entered' issue on event site
  - Can't reproduce

## LMS

- [x] Test new filepath helpers
- Change Exercise to not generate guides
  - [x] Add to list of skipped classes in Pdfable
  - [x] Cut down form fields to guide/resources/basic stuff required

## June 5th

#### In-office tasks

- [x] Try new docker_entrypoint
  - Failed again, with a permissions error
  - Tried changing the permissions, failed for a different reason
  - Gave up again for now and will just migrate manually
- [x] Manually fix the PPT guide uploads for lessons 48 & 49
  - [x] Discover and fix edge case with short name for keep up having space in it, leading to icon path breaking
- [x] Test whether the event site is correctly receiving IPs from the docker container
  - Certainly seems to be from the logging, will need to do some real-time testing with the affected SMs

## LMS

- [x] point 'materials' subdomain of 'kids-up.app' at the LMS
- [x] Make resource dropdowns absolutely positioned in a relative container so they don't shift the layout
- [x] Grey them out when there aren't any attached resources
- [x] Sort searchable resources by most recent, only show the last 10
  - But still show unlimited results for searches
- [x] Show kindy phonics on teacher page
- [x] Extract the logic for checking guides are uploaded to PdfUploadable concern
- [x] Fix resources details element having higher z-index than summaries that drop down from them
- Address Github issues
  - [x] Add KindyPhonics
    - [x] Write a system test for creating one
    - [x] Create model, factory and unit tests
      - [x] Alias 'example sentences' as 'blending words'
      - [x] Should automatically set level as kindy
      - [x] Exclude from guide generation
    - [x] Create and controller & views
  - [x] Add 'Special' (blank) lessons
    - [x] Write a system test for creating one
    - [x] Create model, factory and unit tests
      - [x] Exclude from guide generation, only resources and title
    - [x] Create views and controller
      - [x] Hide the guide partial
      - [x] Show them to teachers
- [x] Get a download SVG and add it where appropriate
  - [x] Resource dropdowns (internal)
- [x] Also add separator to the resource dropdown

## June 6th

- [x] Get constantly interrupted by fixing SM's IP addresses in the event site
- [x] Figure out why confirmation emails are failing
  - Was calling `calc_course_cost` directly, but not passing the new slots arg that's required
  - Also relied on the existence of @data
  - passed a list of slots, and removed reliance on @data (partially, probably a better solution than initializing it blank if not present)
  - [x] Wrote mailer tests to make sure it doesn't happen again
- Write tests for all the other mailers
  - [x] InvoiceMailer.updated_notif
  - [x] InvoiceMailer.sm_updated_notif
  - [x] InquiryMailer.inquiry
  - [x] InquiryMailer.setsu_inquiry

## LMS

- [x] Add missing control svg (temp)
- [x] Create PhonicsLesson template
  - [x] Add background image
  - [x] Header section
    - Level, title, goal
  - [x] Image
  - [x] Materials
  - [x] Instructions
  - [x] Adding difficulty
  - [x] Extra fun
  - [x] Notes
  - [x] Links
  - [x] Footer level

## June 7th

- [] Fix the preview when you paste it into a chat

## LMS

- [] Update DailyActivity template with new bg image
- [] Refactor the PDF generation
  - The endless 'draw\_\_\_\_' methods seem like they could be extracted
  - Probably different versions for plaintext, lists and links
- Address Github issues
  - [] Mask the corners of uploaded images to make them rounded
  - [] Add Keep Up/Specialist
    - [] Write a system test for creating one
    - [] Create model, factory and unit tests
      - [] Exclude from guide generation
      - [] Custom levels enum with only specialist and keep up
    - [] Create views and controller
    - [] Add a separate tab for KeepUp/Specialist
  - [] Ensure Lessons have unique title within level and subtype
- Get a download SVG and add it where appropriate
  - [] Guide buttons
- [] Replace icons for aerobics, dance and jumping exercise subtypes when I get them
- [] Add date fields to the table so you can add lessons to other courses
  - In turboframes
- [] Teacher logins need to be locked to their school's IP
  - But only for KidsUP
- [] When updating upload progress, decrement failures if sum of all > total
- [] Add delay between uploads
- [] Try storing user type as a string enum rather then the current frozen array constant
  - Could make some translations etc. easier
- Implement notifications
  - [] When lessons haven't been updated in 2 years
  - [] When there are new (relevant) support messages

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
