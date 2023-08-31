## September 1st

### Odin Project - [Weather App](https://github.com/Brett-Tanner/weather)

- [] Display the info (all in a main element)
  - [] Create containers for the layout elements and do a pulse effect while loading (if no data passed), fill with content once received
  - [] Location info header at top of main
  - [] Current weather card, followed by three days of forecast cards
  - [] Change the border color/shadow of the cards according to weather

### Work Project - [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Features

  - Stats page
    - Adjustments
      - [] Number of each adjustment applied
      - [] Total effect on revenue from each (some will be negative)
        - [] Group any with a magnitude less than a certain amount into a misc data point
    - Edits
      - [] Total edits by staff/customers (subtract the total number of creates from updates)
    - Revenue
      - [] Pie chart of revenue by student category
      - [] Pie chart of revenue by time slot/option/adjustment
    - [] Add tabs/pages for the type of stat
    - [] Add school-specific pages for each of the existing stats
  - [] Add a way of uploading images to the S3 bucket from the site
    - [] Upload to a specific folder based on purpose of image
    - [] Make sure large files work, they didn't the first time
  - [] Event creation
    - [] Event step
      - [] pre-select the existing image in the form
      - [] Extend the 'all' option on event creation to allow specific schools to be selected
    - [] Time Slot step
      - [] Allow slots to be edited individually from the index
        - [] Allow adding an afternoon slot manually if editing a special day
        - [] Allow custom options to be added/edited
        - [] Allow updating time slots with the same name for all events with the same name
      - [] pre-select the existing image in the form
    - [] Remove ability to destroy events from frontend when I'm done testing (no route for it)
    - [] Add a test event with the new flow (on dev env) and go through the whole app to see what needs changing to support having multiple events
      - Probably need some dummy registrations too
  - [] Per-activity costs
    - [] Add internal/external modifier cols to Time Slot
    - [] Add a snack boolean col to Time Slot
    - [] Add code to use them in Invoice#calc_cost
  - [] Figure out what needs to change to stop persisting a blank invoice when there are no unconfirmed invoices available for a child and someone looks at their registration page
  - [] Remove all references to the email template column, then remove the column
    - [] Split the User#show pages out into different pages for different roles
  - [] Have a way to stop sending emails when the event stops
  - [] Look into using our SES account/domain for the school emails to escape their 5000 email limit

- Future Plans

  - [] See if the occasional memory problems are actually something more like [this](https://www.engineyard.com/blog/thats-not-a-memory-leak-its-bloat/)
    - [] Setting up counter_cache for some stuff like registrations on TimeSlots might help with the memory usage
    - [] Also loading all the TimeSlots and Options from the start when calculating Invoice costs
    - [] Install and use Bullet gem
    - [] Also maybe Rack::Bug, or a newer version of something similar since it was last updated in 2015
    - [] Turnout gem to put it in maintenance mode?
    - [] Look at moving to view components rather than partials for (apparently) better performance and easier testing
    - [] Bump Ruby version and others as far as possible
    - [] Forms
      - [] Add useful error messages to all forms
      - [] Add JS validation as well (constraint validation API, see the [Odin Project Lesson](https://www.theodinproject.com/lessons/javascript-form-validation-with-javascript))
    - [] Come up with a better logging system than just dumping them unsorted to S3 (apparently sending them to STDOUT sends them to Cloudwatch?)

### Work Project - [Seasonal Wiki](https://github.com/Brett-Tanner/KU-wiki)

- [] Add 'How to contribute'
  - [] Adding a page
  - [] Adding a section
- [] AWS section
  - [] Pushing a new version
  - [] Services we use and overview of what for
- [] Rails section
  - [] Overview
  - [] Useful Commands
