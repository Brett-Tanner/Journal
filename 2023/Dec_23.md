# December 2023

## December 1st

### [Seasonal Registration Site](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Write tests for Invoice#calc_cost to prepare for the rewrite
  - [] Test adjustments
  - [] Test options
  - [] Test PDF creation (or at least that one is created)
  - [] Test the summary
- [] Add button to generate photo service armband PDF for parties
  - Printable template with kids' names and a color which shows their photo status

#### Future Plans

- [] In August 2022, RDS certificate [expires](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/UsingWithRDS.SSL-certificate-rotation.html#UsingWithRDS.SSL-certificate-rotation-updating). Will need to rotate to avoid connectivity issues.
- [] Move control of the domain from that Japanese site to Cloudflare
- Platform Upgrades
  - TEST ALL ON STAGING FIRST
  - [] Bump AWS platform version
  - [] Try bumping Ruby version to latest stable (can maybe install manually with a pre-deploy hook)

#### Views

- [] Look into HAML for templating rather than ERB, as well as the other options like phlex or components
  - [] Do a moderately complex view in each of them and benchmark it
- [] Move all formatting-related code into helpers
  - [] Can still use in controller using `helpers.method`
- [] Change the current event#show to be Invoice#new, since that's what it really is
  - [] Rework the current add_slot partials into a container, morning and afternoon
    - They can likely use fieldsets (with a form attribute matching the invoice form's id) to be submitted with the form directly
    - reduces the JS I need on that page [MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset)
- [] If you wanna show fallback content (like on the invoice index) use `render 'partial' || 'fallback text/content'`
- [] Extract form error messages into a shared partial
- [] Potentially also extract fields shared between multiple models into a partial (e.g. names for kids/parents)
  - Or just partials for each type of form group? As a fieldset

#### Optimisation

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
