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

- [] Event booking rework
    - [] Use current invoice if it exists/is not closed, otherwise use a new invoice
        - So have an @invoices, not just one. Set the desired invoice through params
        - [] Grey out slots if registered for in previous invoice
            - Have a list of all registrations from @invoices or from just the event's time slots
        - [] Put a link to that invoice on greyed out slots (separate for each child)
            - Using the list of all registrations

- [] Add Invoices
    - [] Need to be able to merge invoices by moving registrations from one to another
    - [] Need a request change button on the old, paid invoices

- [] Event_children/time_slot_children rework
    - [] Event children
        - [] Add the cost breakdown popup
        - [] Build out the functionality to send a confirmation email from the table
    - [] For time slot children, should just look exactly like the printable one

- [] Implement notifications
    - [] Automatically created on certain actions
        - 

- [] Hosting
    - [] 

- Bugfixes/Requested Features
    - [] From Event#index, just put the link to Child#index on the pic for staff rather than the link to Event#show
    - [] Add repeated discount to Invoice#calc_cost (probably as an adjustment?)


#### What I learned
- 