# March 2023
## Mar 1st

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- [] Event_children/time_slot_children rework
    - [] Event children
        - [x] Change overall layout to use a table
        - [x] Get the sticky headers working properly
        - [x] Display all the necessary info
        - [] Add the cost breakdown popup
        - [] Build out the functionality to send a confirmation email from the table
    - [] For time slot children, should just look exactly like the printable one 

- Bugfixes/Requested Features
    - [] From Event#index, just put the link to Child#index on the pic for staff rather than the link to Event#show
    - [] Add repeated discount to Invoice#calc_cost (probably as an adjustment?)


## Mar 2nd

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- [x] Event booking rework
    - [x] Use current invoice if it exists/is not closed, otherwise use a new invoice
        - [x] So have an @invoices, not just one. Set the desired invoice through params
        - [x] Grey out slots if registered for in previous invoice
        - [x] Put a link to that invoice on greyed out slots (separate for each child)
    - [x] Make early arrival/departure options mutually exclusive (radio buttons rather than buttons???)
        - [x] Works if already registered for one of the options
        - [x] Works if not already registered for either option

- [] Event_children/time_slot_children rework
    - [] Event children
        - [x] Add the cost breakdown popup
        - [] Build out the functionality to send a confirmation email from the table
    - [x] For time slot children, should just look exactly like the printable one
        - [x] Display the necessary information
        - [x] Style the table and implement sticky headers like on event_children

- Bugfixes/Requested Features
    - [x] From Event#index, just put the link to Child#index on the pic for staff rather than the link to Event#show
    - [] Add repeater discount to Invoice#calc_cost (probably as an adjustment?)
    - [x] Add an 'on time' option with 0 offset and cost since I'm doing radio buttons for arrival/departure times


## Mar 6th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

Was stuck at Mizonokuchi, just laid some groundwork for AWS

#### What I learned
- New, more optimised zip command for uploading source bundles to AWS
```
zip -r db_prototype_v2.zip db_prototype_v2 -x * .[^.]* "db_prototype_v2/storage/*" "db_prototype_v2/tmp/*" "db_prototype_v2/log/*"
```


## Mar 7th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- [] Add Invoices
    - [] Need to be able to merge invoices by moving registrations from one to another
    - [] Need a request change button on the old, paid invoices

- [] Event_children/time_slot_children rework
    - [] Event children
        - [] Build out the functionality to send a confirmation email from the table


- [] Implement notifications
    - [] Automatically created on certain actions
        - 

- [] Hosting
    - [] 

- Bugfixes/Requested Features
    - [] Add repeater discount to Invoice#calc_cost (probably as an adjustment?)

#### What I learned
- 