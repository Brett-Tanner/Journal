## Mar 1st

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
    - [] For time slot children, should just look exactly like the printable one

- [] Implement notifications
    - [] Automatically created on certain actions
        - 

- [] Hosting
    - [] 

- Bugfixes/Requested Features
    - 

#### What I learned
- 