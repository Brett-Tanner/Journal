# October 2024

## October 2nd

- [x] Add a redirect to new confirmation page on succesffuly inquiry submission from .biz
- Bumping versions/code scanning
  - [x] Event site webrick & puma
  - [x] Event site solidqueue
  - Mission control for both
    - [x] Event site
    - [x] LMS
- [x] Add button to update first seasonal after each event
- [x] Add whether they have photo service to the event attendance sheet
- [x] Fix missing english translations for lesson types on LMS calendar
- [x] Editing setsumeikai inquiries seems to cause an error (3337, but all seem to do it)
- [x] Add translation for Ueno, Kanamecho
- [x] Try helping Mike troubleshoot the main site going down
  - Was the storage volume filling completely cos of too many assets

## October 3rd

### Jayson Stuff

- [x] Run through changing Options w/Leroy
- [x] Create TimeSlot::SNACK_COST to avoid random 165 values all over
  - [x] Fix ordering bug in new invoiceable
- [x] Add inline_svg to LMS
- [x] Seems to be issue with tutorial category modal, at least with seed data
- [x] in '\_resources_list' partial, we're using @lesson instance var rather than passing as local
- [x] Fix Jayson's tests failing cos he doesn't have poppler to generate PDF previews
- [x] Make jobs visible to plebs on event site
- [x] Add Alex's new Photo Service APNG
- [x] Switch seasonal site to new booking page

# October 9th

- [] Button to download list of photo kids + siblings
  - Copy the query from the event sheet, found a way to do it all in one query there
  - Needs to be a CSV of name, katakana_name, en_name, school name, category and SSID
  - [] For parties, it needs to include the name of the party they attended as well
- [] Add organisation ID to kids
  - [] And migrate the existing ones
  - [] Form and strong params too
  - [] Use in policies
  - [] Make student ID unique within org, not school
  - [] Add automatically when uploading from CSV
  - [] Create default teacher and class when new schools create
  - [] Add uploaded students to their school's default class
  - [] In future will need a way for other orgs to bulk assign students to a class
- [] Add event lessons
  - [] They're gonna need an attached image to display
  - [] Use the cards for teacher lessons as a template, same basic layout too
  - Can probably be handled by same controller?
  - [] Style to match Alex's mockup
- [] Provide a summary of kid's test results per test
  - For curriculum team/admins to look at
  - like the input view but minimal
  - maybe sorted by the level they moved to and just showing name/prev level/score
- [] Add reviews to lessons
  - [] Need stars and text
  - [] Text pops up after star rating given
  - [] on the teacher_lesson modal
  - [] Button on the lesson page to mark all reviews acted on, they won't count to the current score
    - Maybe show the score for active reviews and all? And have an index with all of them
- [] Add a way to upload splash images for LMS through frontend similar to seasonal site and have it automatically displayed,
  - except you'll need a way to mark them active/inactive/have multiple possible images on rotation
  - so probably make it more of a resource wrapping ActiveStorage rather than just automatically grabbing the latest image from a folder

### General

- [] Need a separate boolean column for whether the kid has a food allergy
  - Talk to leroy about it
  - Set by a radio button
  - Parents get a splash on their page & kid's page telling them to update, redirected if they try to register
  - [] After Summer School, change it so allergy kids can't see the option for lunch
  - [] When merging children the food allergy or not needs to be copied
  - [] When finding by SSID, make them select food allergy or not in addition to first seasonal or not

### Expo prep

- Add an API on the LMS to receive form submissions & email Nakagawa san
  - [] Allow it to receive requests without auth/CORS issues

### Leaving prep

- [] Give event site a 'toggle first seasonal' button
  - Gets the name of the latest seasonal with `#seasonal?`, then a list of their ids
  - Get all the children who attended
  - If they're marked first seasonal toggle it to false
  - [] Add to the wiki under 'creating events' cos it needs to be done before each seasonal
- Get Jayson credentials
  - [] AWS
  - [] New company docker
  - [] Company github
  - [] Company cloudflare
- [] Style the photo service button on footer once designed by Alex
  - [] Will need to change the child switcher links to point at new invoice path

### LMS

- Styling
  - Splash pages
    - [] Splash
    - [] Login
  - [] Tests
- [] Add a UI for viewing/rolling back to previous versions of students
  - [] Remove limit on versions of students stored
- [] Delete the 'LessonUses' controller and move it to CourseLessons#index, since that's what it really is
  - [] See if there's anything stopping me just using a CourseLesson form, rather than `fields_for` in a form
  - [] Add the date fields and CourseLesson update/create actions to enable adding lessons to courses easily
- [] When updating upload progress, decrement failures if sum of all > total

### Event Site

- [] Need to add event summary stats to the charts
  - Like the table Admins get at the top when they log in
- Extract PDF generation into a concern
  - [] Generate it in a SQ job when the invoice is modified
    - [] Though this might cause issues with ordering, so will need a new queue to ensure pdf jobs performed first
    - [] And make it available to download from the invoice partial
  - [] Refactor to use the cost info object returned by Invoice#calc_cost

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
  - [] Also maybe Rack::Bug, or a newer version of something similar since it was last updated in 2015
- [] use read/write_attribute or bracket notation in my custom getters/setters
  - Not sure what I'm using now, but probably not those
- [] Use AWS Cloudfront to serve images?
  - [Useful article](https://headey.net/rails-assets-active-storage-and-a-cloudfront-cdn)
- [] Can probably speed up queries for ChartController with pluck
- [] If indexing FK columns which can be null, exclude null from the index

##### Views

- [] Check for missing translations with `i18n-tasks`
- [] Use @layer to section off old BS styles so I can switch to tailwind
  - But both tailwind and BS using !important liberally might make that problematic
- [] Use `current_page` helpers in partials to conditionally render stuff like diff school selection on event partial
- [] Only needs locale param in `number_to_currency` calls, rest are bloat
- [] number_to_phone_number exists
- [] there's also a number_to_percentage helper, but may be more verbose than what I'm doing now
- [] If you wanna show fallback content (like on the invoice index) use `render 'partial' || 'fallback text/content'`
- Extract form error messages into a shared partial
  - This exists now as 'shared/\_form_errors'
  - [] But don't think I made sure it was used everywhere
- [] Use time_tag helper when outputting date or time, generates a `time` element which apparently is a thing
- [] Use number_to_human_size when I add the blob index etc.

### SS Replacement

- We need an electronic version of the new student application form
  - Maybe prefill behind a PIN
  - Could use the PIN field on event site users for that
  - Have an open, blank one anyone can use
  - Multi-stage? With stage by stage validations
- New customer form
  - Add a `MultiInput` for select/radio
    - [] Still some issues with deserializing the custom type
    - [] Add the partial to display it on the submission form
    - [] Add the partial to display the responses on the Submission show page
    - [] Extract the reusable/shared code from Single/MultiInput
  - [] Will need to process the field `name` to ensure downcased and underscored
  - [] Create a test form template that matches the new child registration one
    - [] Seed it
  - [] Create basic models for the courses etc., just so I can run the calculation
  - [] Create a model for Contracts
    - [] If Submission#template_id is 1 or some other dumb condition like that;
      - Give a button to create a contract from it
      - which calculates & stores the adjusted contract from the submission
    - [] Calculates the fees based on form selections
      - [] For courses, first month is least of unit price \* selected days remaining or the regular monthly cost
      - [] Needs to add a bunch of other costs, like snack, textbook
      - [] SMs should be able to manually adjust calculated values
        - But only per item, not the total
    - [] Needs to be printable as a PDF for signing, or some way to electronically sign
