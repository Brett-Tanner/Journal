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

- [] AWS
    - [x] Installed EB CLI
        - Attempted to use it to create the EB, failed because it got stuck on creating the source bundle
    - [x] Updated Ruby to 3.0.5 to match AWS platform version
        - Issue is now pg gem failing to install for some reason
        ```
        An error occurred while installing pg (1.4.5), and Bundler cannot continue.

        In Gemfile:
          pg
        ```

#### What I learned
- AWS EB doesn't like zip files produced on a Mac, so use git archive instead (and probably a prod branch to exclude dev stuff)
    - hence new command to generate a source is this from the project folder
    ```
    git archive -v -o db_prototype_v2.zip --format=zip HEAD
    ```




## Mar 8th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- [] AWS
    - [x] Successfully SSH into the EC2 instance!
    - [x] Resolved the issue with pg gem being installed
    - [x] Resolved issues with Bundler and puma versions not matching those on the AWS platform
        - Issue now seems to be puma constantly failing to start due to being able to load some 'indifferent_hash.rb' file
            - Stayed up way too fucking late trying to figure this out, still have no idea.It's 3:20am, what the fuck am I doing
                - Leaving puma out of gemfile produces same error (cos it's the same version by default)
                - Reverting to the original version (5) leads to it terminating as soon as it calls require rather than making it to the folder, which is different at least
                - I hate this, I'm going to sleep

- [] Add Invoices
    - [] Need to be able to merge invoices by moving registrations from one to another
    - [] Need a request change button on the old, paid invoices
    - [] Children are NOT ON THE SAME INVOICE, separate invoices for each child
        - [] Toggle between kids where the invoice toggle is now
            - [] On price bar
            - [] Preserve scroll position
        - [] Button to copy kid's registrations from one kid to to another (separate controller for this)
    - [] No switching between invoices, just display them all at once and have total for all
    - [] Have a confirmation screen before invoice is finalised showing full details
        - Can I do that with Invoice #new? does it create #new regs???? 


#### What I learned
- The pg gem couldn't be installed because EC2 instances come with a hilariously outdated version of PG installed, and the gem needs a supported version of PG installed
    - In the future will install a newer version of PG through .ebextensions/packages.config during instance initialization [like here](https://stackoverflow.com/questions/61148791/postgresql-on-elastic-beanstalk-amazon-linux-2/63204453#63204453)
    - For now will try to SSH in and install it manually/check what versions are available for the config file in future
    - Shouldn't I be able to just have it connect to the RDS tho???

- Just generate a new keypair for SSH into the instance, it needs to be in your .ssh folder as a .pem

- To get to the app on the EC2 instance, go to the home directory then cd into /var/app/current
    - You don't have write permissions for a whole bunch of stuff though [per this](https://stackoverflow.com/questions/27611608/ec2-user-permissions), so mostly for looking around

- You can use 'tail -f' on a file to view changes as they're made (in shell)
- And cat to read the file


## Mar 9th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)

#### What I did

- [] AWS

- [] Add Invoices
    - [] Need to be able to merge invoices by moving registrations from one to another
    - [] Need a request change button on the old, paid invoices
    - [] Children are NOT ON THE SAME INVOICE, separate invoices for each child
        - [] Toggle between kids where the invoice toggle is now
            - [] On price bar
            - [] Preserve scroll position
        - [] Button to copy kid's registrations from one kid to to another (separate controller for this)
    - [] No switching between invoices, just display them all at once and have total for all
    - [] Have a confirmation screen before invoice is finalised showing full details
        - Can I do that with Invoice #new? does it create #new regs???? 


#### What I learned
- 