# June 2023

## June 1st

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Bugfixes

  - [x] Had one less column on the event sheet than needed because I was subtracting both special days from the number of columns, despite them only taking one

- Features

  - [x] Give big boss AM an overall summary for the company too

### Personal Project - Wiki

- [] Style the navs for each topic
  - [x] Ruby
  - [x] Rails
  - [x] Jekyll
  - [x] Git

### What I learned

- You can always just set the base height/width of an img in HTML properties, especially useful when a BS .img-fluid has gigantism
- Jekyll layouts can be nested, just use the parent layout as the layout of the child layout

## June 2nd

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Bugfixes

  - [x] Stopped a new child/schedule version being created each time they're updated due to manually setting created and updated at
  - [x] Set backup retention back to 14 days after it somehow got set to 2

## June 3rd

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Bugfixes

  - [x] Photo service is bugged, it's impossible to register for right now. Works in JS but is not present on confirm page or confirmed invoice
    - Was being caught by the orphan option check as event options never have an associated slot
    - Added a guard clause to except event options from said check

## June 5th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Bugfixes

  - [x] Two schools were in the wrong areas (Ikegami and Toyocho) so I switched them
    - Actually, they had their ids switched. The correct ids were in the correct areas, but those ids were associated to the wrong school/name
    - Means:
      - Anyone who signed up without associating their kid to an SSID is fine, they manually chose the school which reflects the order of the schools in the database
      - But any kid imported from the SS is at the wrong school, because it's mapped wrong.
        - So to fix, maybe we just change the mapping in the SS imports?
          - Nah change the names to avoid confusion on future. Name/id mapping is same everywhere
        - Then for both of those schools, check if any of their students have an invoice for an event at the other school, switch to the correct event if so
  - [x] Renamed the schools to match the SS mapping, then made sure all associated children/invoices/events/managers were associated with the right one

### Personal Project - Wiki

- [x] Style the navs for each topic
  - [x] HTML

## June 6th

### Personal Project - Wiki

- [x] Added a table of contents to the css/animations page, will re-use on others

### Odin Project

- [x] [Transforms](https://www.theodinproject.com/lessons/advanced-html-and-css-transforms)
- [x] [Transitions](https://www.theodinproject.com/lessons/advanced-html-and-css-transitions)

## June 7th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

- Bugfixes

  - []

- Features

  - [] All AMs want the all schools summary, so remove special code for big boss and maybe condense admin/AM conditionals a bit
  - [] Add an instructional PDF to the login page/make the sign up button more obvious
  - [] For special days, display the connection option between the morning and afternoon slots (on the daily attendance sheet)
    - Maybe also show if kids are attending both morning and afternoon in that column for regular days
    - Just a different header/values
  - [] Prevent slots closing on weekends, they should close the Friday before instead
    - Possibly hard code the relevant public holidays
  - [] Add a search to the indexes (mainly for admins, there are too many pages and we don't know the order)
  - [] Possibly bring the recalculate button back, e.g. for children whose category in the SS changed since their booking was made
  - [] When generating invoice details, just skip if the option name is 'なし'
  - [] Look into using our SES account/domain for the school emails to escape their 5000 email limit

- Security

  - [] SM can only log in from their school's IP address **requires IP list**

### Odin Project

- [] [Keyframes](https://www.theodinproject.com/lessons/advanced-html-and-css-transforms)
