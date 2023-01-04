# December 2022
## Jan 3rd

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)
#### What I did
- [] Tested registration associations
    - [x] To events
    - [x] To children
    - [] To time slots


## Jan 4th

### Work Project - [Event Database Prototype v2](https://github.com/Brett-Tanner/db_prototype_v2.git)
#### What I did
- [x] Tested registration associations
    - [x] To time slots
    - [x] To everything else
- [] Completely reworked the Area/School/Manager relationships to be has_many :through
    - [x] Tested Area
    - [] Tested School
    - [] Tested User
    - [] Tested everything else

#### What I learned
- Has_one/belongs_to were going to cause problems down the line one way or another, whether it was the original inability the change managers or a future need to have multiple managers/managers to have multiple schools/areas
    - Moved to has_many :through instead to avoid these issues and create more room for added features