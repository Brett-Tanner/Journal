# September 2022

## Fri 2nd

- Decided to start keeping a journal

### Odin Project - Ruby Foundations
- Spent even more time debugging the load function for my chess project
    - Tests were failing due to a YAML.load_file call returning nil despite the file existing and containing valid YAML
    - Tests passed when the files were present prior to the test being run
    - The issue appears to be with my test setup rather than the code not working as intended
        - I thought deleting was the issue, but it also seems to be an issue when I write to the file before trying to load it
        - removing all the unless statements in the before block causes an otherwise passing test to fail
        - So perhaps you can't load a file which has been written to in this session/instance???
        - obvious solution is to move the logic creating the files outside the context, but then what about when the first test deletes a file? And would that even work or would it still count as the same "instance"
        - maybe something to do with the cursor position thing in C I learnt about in CS50, Ruby is based on C. But no manual file close/move cursor option in Ruby that I can find
    - Seems like there are issues with creating a file and reading from it in the same function/instance????
    - Tried searching the psych docs for Ruby's YAML support and Ruby's docs for the File class, but couldn't find any info to support
    - I think I'll leave it for now and move on, haven't made real progress in two days and if I'm right about the cause it's unlikely to affect the actual functionality of the game
    - Will come back with a fresh perspective to fix it though, as being unable to delete saves is not ideal

## Sat 3rd
### Odin Project - Ruby Foundations
- Finally fixed the tests for Game#from_yaml
    - It was something to do with creating a file and reading it in the same test
    - So I added the actual file I wanted to read to a new test directory, and prevented it from being deleted with an unless? check on the File.delete
    - Then still created two dummy files so it still printed the expected list of files, but didn't read them since that seemed to be the problem
    - In future, either have a separate directory for test files so they won't show in normal use and don't need to be created/read during the test
    - Or just figure out why being created/read in the same test is a problem at some point
- Started building the possible move constants for each piece
    - For Knight, just copied it from Knight's Travails project
    - But did also learn you can't call a class' function to initialize a constant of that class if the constant is defined before the function
    - You are, helpfully, free to put constants at the end of the class and make them private. Otherwise I'd need to do a lot of scrolling to get past the list of possible moves
    - I decided to hardcode the list after figuring out how to generate it as that seemed like it would perform better than generating it once per instance for 32 pieces, especially the same one 16 times just for the pawns. 
        - May or may not be best practice though, maybe you're supposed to put it in a separate file and require it? 
        - But that kinda feels like it defeats the purpose of making it perform better, and makes the code less readable
        - On a related note having the list there is much more readable than a bunch of generating functions which never actually print it anywhere

## Sun 4th
### Odin Project - Ruby Foundations
- Realised my knight move list was for an 8x8 array, and now I'm using a 9x9 hash. Adjusted the generating methods to match by just making the array it uses to generate 9x9, then going next whenever there's a 0 in the order then compacting the resulting hash of moves
- Created move lists for
    - Bishop: Fairly straight(diagonally)forward
    - King: Also straightforward once I remembered it moves horizontally and vertically as well as diagonally
    - Pawn: Have to make sure Piece#legal? is the last check before a move, otherwise Pawns could prune their move list before they actually move. 
        - Did not actually finish making the logic for it

## Mon 5th
### Odin Project - Ruby Foundations
- Wrote tests for then drafted my first version of Pawn#legal?, since it won't really rely on a Possible_moves like the others. 
    - Checking possible moves of a pawn seems better suited to a bunch of true/false tests than an adjacency matrix since there are a bunch of different scenarios but very few possible moves
    - Remembered you can have two different subjects, rather than manually setting the subject to a white or black pawn each time
    - I finished all the pawn tests except those which need to check if there's a piece to take on the diagonal
        - For some reason my doubles don't seem to have a color attribute, despite me definitely defining one. I finished work too late to start debugging such an unintuitive problem so I'll finish writing the tests tomorrow

## Tues 6th
### Odin Project - Ruby Foundations
- Finished the tests for Pawn#legal
    - Realised in hindsight I should have just generated the board double the same way I do for the actual board to make it more intuitive, after about 10min carefully flipping the board in my head because it's an array rather than a hash
- Created move lists for
    - Queen
    - Rook
- Tomorrow is testing and writing the #legal? method for the Piece parent class
    - Write in Piece parent class, then test each individual piece to make sure the move list I generated is correct
    - Remember this is not checking if the piece is blocked or anything like that, checking for blocks will likely need to be a separate method
        - When I do write the #blocked? method, probably put it on Piece parent class then just overwrite it on Knight to always just return false
        - Can I even do that with the move_list? Probably, I did it for Knight's Travails. 
        - Just need to remember that I'm not looking for shortest path, I'm checking if there's an unblocked path of one move
    - Thinking of pathing makes me wonder if I should make the CPU player randomly select a piece to move, then have it figure out the shortest path to the enemy king and make the first move from that
        - Might be more interesting that just random valid moves, but also might just be a waste of time for no benefit

## Wed 7th
### Odin Project - Ruby Foundations
- Testing Piece#legal? turned out to be very straightforward, honestly might be pointless but still good to check I didn't miss anything
- Lots of writing tests, no big issues

## Thurs 8th
### Odin Project - Ruby Foundations
- Started work on Piece#clear_path?
    - Realised the possible_moves lists aren't actually useful for checking a path, since they don't give any info on the path between start and destination
    - But that's fine since Knights can't be blocked, and everything else moves in a straight line
    - So just find the difference, then increment through and check each space by looking at its class
- Honestly I got distracted by a bunch of stuff today/the last few days, need to focus back up and actually get this done

## Fri 9th
### Odin Project - Ruby Foundations
- Continued work on Piece#clear_path?
    - Wrote the special case for Pawn#clear_path cos he just has to be special
        - insta-true if it's a diagonal move (#legal? should stop diagonal moves to empty spaces anyway)
        - gets the move length, then returns true unless either square it would move forward through is occupied
    - Got it working using nested if statements to deal with down and backward movement on the x and y axes, feel like there should be a more elegant way to do it but maybe I'll revisit once I've got everything else working
- Tidied up State a bit since I have't looked at it in ages
- Started planning out State#check?
    - Right now it seems unnecessarily long and complex, I'm doing a lot of searching through the whole board
    - Remembered that Ruby does shallow copies, meaning my copy of the board I used to test if the change caused check was actually changing the original board, causing an infinite loop
    - Finally found the King after remembering that #class does not return a string, it returns the actual class
    - Finally realized that my very early decision to have different capitalization for the colors in different places was stupid
    - I think I've got it working now, at least for when the King isn't in check. Tomorrow I'll write the tests that make sure it knows when the King is actually in check
- Testing State#move with all the new checks it has to pass broke my old tests, but that's ok cos I know a lot more about doubles and mocking and also when not to do those things now, so I should re-write the old tests anyway

## Sat 10th
### Odin Project - Ruby Foundations
- Test State#check?
- Refactor State tests to work now that all the move checks are actually made
- Modularized some parts of State#move
- Scaffolded and tested State#checkmate?, no issues other than a few typos and variable naming mistakes which were quickly solved
- In my breaks tomorrow I'll work on State#promote, and once that's done the game should be ready to actually play! Assuming I didn't forget any features. 
    - This'll be my first time trying to run a completed program after only TDDing it, I've never actually run the Game file and seen what happens. 
    - So hopefully it all goes perfectly or nearly so and TDD as an approach is validated, because there were a lot of great things about automated testing
    - Ofc even if it fails that probably just means I didn't write my tests well or didn't test enough/the right stuff

## Sun 11th
### Odin Project - Ruby Foundations
- Tested and implemented State#promote
    - Only issue was me not thinking about order of operations, which lead to me promoting the enemy piece then moving my pawn over the top of it
- Now we try playing it and see if all the testing worked!
- It almost worked perfectly! 
    - There was an errant error message displaying from the State#check? method being called from valid_move? in checkmate, I removed it from #valid_move? and called it separately in move, as it's not necessary to check for check when already checking for checkmate
    - I quickly realised I'd never actually added a way to trigger State#save, so I did that
- Also, by finished I mean the core functionality. I still need to give the computer players the ability to make random moves, and add a replay feature if I still feel like doing that
- For now though, pretty thrilled! Only two things got through my testing, one which is kinda hard to notice in a test since I receive all #puts by default and one which was just kinda a silly thing I forgot to do. Pretty fantastic for my first big, complex project!
- Ok turned out there were some issues with loading saves that my testing didn't catch cos I didn't save an actual State
    - You need to explicitly allow non-standard classes be loaded with the permitted_classes: option
    - There's some compatibility thing involving aliases which is solved by toggling aliases: true
- I've decided I'll come back and add Computer players and the replay function when I'm tired of reading stuff in the next course and want to code something. For now, onward!

### Odin Project - Intermediate HTML & CSS
- Looked through the different kinds of HTML elements and a CSS cheatsheet, saved both to the appropriate folders in Useful Ref
- Emmet! I remember discovering this existed from a YT video or something and learning a few shortcuts, it seems incredibly useful
    - But I'm tired so I'll read it tomorrow
    - Actually I stayed up to watch LEC
        - Wrap with abbreviation is bound to "cmd+e"
        - Remove tag is bound to "cmd+r"

## Mon 12th
### Odin Project - Intermediate HTML & CSS
- Read about SVGs
    - They scale like a vector, because they're mathematically defined rather than using pixels
    - Very good for simple, geometric designs or visualising data, not so much for photo-realism or busy designs
    - Usually smaller than an equivalent JPG, and file size doesn't increase with image size 
    - Have a series of properties which can directly be altered/created in HTML and CSS
    - They can be embedded inline to be made interactive, but that will slow down your load times
    - Or linked like a regular image, which still lets them scale but you can't interact with their contents
- Got some useful sites for free icons and saved them in my Resources folder
- Read about HTML table elements
    - You can manually set each cell in the table to take up a certain number of rows/columns using the row/colspan attributes
    - You can style whole columns using col and colgroups
        - col goes inside colgroup just below the opening table tag
        - create a self-closing col element for each column, it styles the corresponding column
        - Remember to include empty cols (at least before the one you want to style) or it'll just style the first one
        - If you wanna apply the style to a certain number of cols from the start, use the span attribute
        - thead, tfoot and tbody are used for formatting, e.g. when you want a table header and footer to stick to the top and bottom of the screen while the body scrolls past
            - tfoot can be included at the start just below thead but will still be rendered at the end
            - tbody wraps everything else in the table (added implicitly even if you don't use it)
- Started working on the assessment for the table section, but its late and more complicated than expected/I don't remember that much from isolated bits of reading scattered throughout the day

## Tue 13th
### Odin Project - Intermediate HTML & CSS
- Finished off the table assessment, was actually easy. Key takeaways:
    - th exists
    - If you want a header to span multiple rows, you need to actually create the rows
- Read about default styles (applied by the browser)
    - You can use a file called a 'CSS Reset' to remove the default styles for your project
    - The main two options are the Meyer Reset, which completely removes default styles applied by browsers and normalize.css, which keeps the useful defaults and makes the the same across browsers
    - I went with normalize.css, as I don't always want to have to manually style everything. I'm not a graphic designer
- Read "CSS units"
    - Only use px for absolute units, in and cm are only for printing
    - em and rem relate to font size, though they're used to size other things too
        - em is the font size of the element (or its parent if parent sets font size)
            - This means you can chain 1.3em for example to make list items progressively larger
            - em is mostly used for media queries
        - rem is preferred as it is the same but with the font size of the root element (:root or html)
            - set :root font-size to **6.25%** to make it base 10 in relation to pixels
            - e.g. 20px would be equivalent to 2rem, 1px would be 0.1rem
    - Also have viewport units, vh and vw, which are each 1% of the relevant dimension of your viewport
        - vmin and vmax use the smaller or larger of the viewport dimensions
        - for text, you usually don't want to use plain vh or vw because the scaling can be extreme
            - instead use calc(base size + vh or vw scaling)
    - Can use % for a percentage of the container instead
- Read "More text styles"
    - Added links to online font sources to my resources folder
- Read "More CSS properties"
    - Just bookmarked it after reading in Useful Ref, I've seen them all before
- Read "Advanced selectors"
    - Again just bookmarked after reading, it's either review or I ended up already finding it anyway

### Odin Project - Ruby Foundations
- Went back and added replay functionality, went exceptionally smoothly.
    - Probably cos I had a long walk to the shops to think about it
- However, upon trying to show Viktoria the replay function by replaying a game where I lost as fast as possible, I didn't lose
    - Got a "well, that was unexpected, which I traced to Piece#find_path 
        - I remember thinking I didn't need an else there, good thing I ignored that feeling
    - Fixed that by making the row_diff and col_diff values absolute values for their comparison, which allowed me to catch previously uncaught cases of a positive row diff and negative col diff or vice versa
    - However the game now insists the black queen is blocked, when it clearly isn't
        - I printed the path found by find_path, and it turns out the queen is going down left rather than than right in the path?????
        - Because I'm only using row diff to increment, so it's going -1, -1 on each move rather than -1, 1 which it should be doing
        - Ended up fixing that by just using the abs val of row diff with times, then adding the row and col diff, then adding or subtracting 1 to them depending on whether they're positive or negative
        - Applied the same improvement to h and v movement as it significantly reduces nested if statements
    - So now the Black Queen can move again, however State#check? doesn't think the King is in check after she moves to d8
        - In fact it seems to print the warning, but not actually stop the move, every time other than the time the King is actually in check
        - It always prints that warning after checking whether the Queen can take the King
        - **However, on the move after the Queen puts the King in checkmate, the game correctly recognises the King is in check and won't allow the white player to move**
        - This doesn't seem like an easy fix, so time to write some more detailed tests for #checkmate?
            - Specifically for when the King is only put in checkmate after a certain move
            - And for when the King would be in checkmate but can be saved by another piece
                - For that one, is it enough if the piece which puts the King in check can be taken? Probably not, I need to check for multiple pieces that have the King in check and see if they can all be taken/blocked
        - I'll come back to this tomorrow, there's other stuff I need to do irl
    - Also, remember your realisation that #check? doesn't account for other pieces rescuing the King, and do something about that once you fix the current functionality

## Wed 14th
### Odin Project - Intermediate HTML & CSS
- Finished CSS diner
- Read "Positioning"
    - Static positioning: default positioning, top, bot, l and r don't affect position
    - Relative positioning: the properties above do in fact change the position of the element relative to where it would normally be
    - Absolute positioning: removes element from the normal flow, put it wherever you want on the page without disturbing other elements
        - positioned relative to an ancestor element (but only if the ancestor isn't static, otherwise positions relative to html element)
        - use t, b, l, r
        - useful for modals, captioned images and icons on top of other elements
    - Fixed positioning: like absolute, but relative to the viewport. Useful for stuff you want to stick as you scroll like nav bars and floating chat
    - Sticky positioning: act normally until you scroll past them, then act like fixed positioning
- Read "CSS Functions"
    - calc(): Used for mixing units, can nest. Calculates the math expression inside the brackets
    - min(): Will use whichever is smaller of the given arguments. Can do basic math inside. Ensures sets the maximum size of something.
    - max(): Will use whichever is larger of the given arguments. Can also do math. Ensures a minimum size.
    - clamp(): Takes 3 arguments; smallest, ideal and largest values.
- Read "CSS variables"
    - declare like --what-a-variable: value, can also set it to calc() etc.
    - to access, use var(--what-a-variable)
        - can also pass a second argument as a fallback value
        - or any number of arguments, can pass another variable then another fallback for example
    - they have scope, much like JS scope they're only accessible from the selector they're declared on or children of that selector
    - when you want it to be available to everything, declare it on :root
        - can use this to make a dark mode
            - declare variables for root.light and root.dark, set a default class on html and add js to switch the type
        - can also just set light as default, and use @media (prefers-color-scheme: dark) {root {rules}}
            - but then it's just gonna use the browser/OS default, user can't change it themselves
- Read "Browser compatibility"
    - Reminded that W3 schools is scummy for aping the W3C organisation's name
    - Apparently every browser on iOS uses webkit, even if it's called Chrome or Firefox???? Didn't know that
        - Chrome and FF are just skins for Safari
- Read "Frameworks and pre-processors"
    - For CSS, frameworks are usually just a bundle of CSS that implements common styles/feature like dropdown menus or what buttons look like
        - Pros:
            - Good documentation
            - Easy to find help
            - Easy to create MVP (or a backend system like an admin dashboard)
            - Saves you from making design decisions like color palette
        - Cons:
            - Can be difficult to customise framework code
            - Can be limited by the need to support old stuff
            - May have performance issues as not optimised for your specific use case
    - Pre-processors extend the functionality of CSS, allowing you to do stuff like write loops, join stylesheets and nest classes
        - Then converts to vanilla CSS when you import to your project
        - Apparently many useful features have been implemented in vanilla CSS now tho, so maybe not worth the overhead
        - Pros:
            - Makes it easier to write complex CSS
            - Nesting rules stops you having to repeat yourself
        - Cons:
            - Debugging is harder as line numbers mean nothing due to the compilation step
            - Compilation can take quite a while
            - CSS files could be huge
            - Most of the features they add can be duplicated in vanilla CSS now
    - Both can save time by quickly creating something which can be iterated on rather than starting from a blank project
    

## Thurs 15th
### Odin Project - Intermediate HTML & CSS
- Read "Forms"
    - Forms are container elements like divs, they wrap all the inputs that can be interacted with on a form
    - Action attribute gives the URL data should be sent for processing, and method attribute specifies the HTTP request method
        - e.g. GET to retrieve something from the server, POST to modify something on a server
    - Input elements take a type attribute and accept input/are formatted depending on that type
        - can also have a placeholder attribute which specifies the placeholder text
        - should have a name attribute, which serves as the variable name when it goes to backend. If no name, input will be ignored
        - input types include
            - Email: displays a diff keyboard including @ symbol on mobile, checks a valid email was entered
            - Password: masks the input
            - Number: only accepts numbers
            - Date: renders simple date-picker calendar
    - Label elements label inputs, they take a for attribute which is the id of the input they're labelling
    - If you're not using a backend server and just wanna get an input that affects/displays something on the page directly, you can use form controls outside the form element
    - textarea is not technically an input element, allows input of multiple lines of text in a resizable element.
        - has a closing tag, so you can enter initial text to display between tags
        - has rows and cols attributes which set the initial size of the text area
    - Selection elements:
        - select element wraps the option elements like a list, and takes a name attribute
        - each option has a value attribute which is the value that'll be submitted when the option is chosen
        - can set one as default by giving it the 'selected' attribute
        - can split options into groups using optgroup wrapper, which takes a label attribute
    - Radio buttons:
        - just input element with type = radio
        - each have a name attribute, selecting a button deselects all others with that name attribute
        - can set a default radio button by adding 'checked' to it
    - Checkboxes:
        - Input element with type 'checkbox'
        - Like radio boxes, but multiple options can be selected at once
        - Single checkbox can be used to agree to T&C for example
        - Can be checked by default by adding 'checked' attribute
    - Buttons
        - Its own element type, with text between the tags
        - Three types (set by type attribute):
            - Submit - Default if none specified. Submits the form it's contained in
            - Reset - clears the form of all user input
            - Button - just lets you click it, used to make stuff interactive with JS
    - Containers
        - Fieldset element: Groups related elements it contains into groups
        - Legend element: Goes right after opening fieldset tag and acts as a title for the fieldset. Text goes between the tags
    - Can't style certain form controls like the pop-up date pickers, have to build your own or use frameworks for that
    - **Finished the 2 MDN introductory guides**

## Fri 16th
### Odin Project - Intermediate HTML & CSS
- Continued the form code-alongs from MDN, for styling this time
    - Most form elements are easy to style now, though wasn't always the case 
        - mild exceptions are checkboxes, radio buttons and input type 'search'
        - almost impossible to thoroughly style input type color, date controls, it range, it file, anything involving dropdown widgets and progress/meter elements
        - for the almost impossible ones you may have to build your own to be able to style them
    - Some form elements won't inherit in some browsers, so make sure you set them to do that (and font-size 100%) manually in your css (font-family: inherit)
    - Can use appearance: none property to stop the OS styling some elements (as much as possible anyway)
        - necessary as some browsers restrict changing some elements like search boxes
        - especially useful for checkboxes/radio buttons as they disappear completely until you restyle them
            - can use :checked and :disabled pseudo-classes (disabled applies when user can't select that option)
    - File picker buttons (e.g. 'upload file') can't be styled at all, but you can hide them using {height: 0 opacity: 0 padding: 0}, which is delightfully janky
        - Then you simply add a label and style it as a button, because clicking the label activates the form control, in this case our now invisible button
    - :hover, :focus and :active pseudoclasses still exist
    - There's also:
        - :required/:optional - target the relevant category of form control (depends on whether required attribute is set)
        - :valid/:invalid and :in-range/:out-of-range - target form controls that are valid/invalid according to the validation constraints
            - If no constraint validation, will match with valid
            - If they have the required attribute and are empty, will match with :invalid and :required
            - If the input has built-in validation but is empty, will still match :valid
            - the range ones are for numeric inputs with min and max
            - they have both because the extra specificity might be useful when providing better error messages 
        - :enabled and :disabled, and :read-only and :read-write
            - read only is set with an attribute (readonly), default is read-write
        - :checked, :indeterminate and :default - for radio buttons/checkboxes in those states/with those attributes
            - indeterminate means its neither checked or unchecked
        - ::before and ::after add a pseudo-element that is the first/last child of the selected element
            - often used to insert content before/after a certain thing, like emoji before all instances of a certain heading (or those hashes on bookmark-able headings)
            - is invisible to screen readers, so don't use it for stuff needed for accessibility
            - since you can't put generated content on a form input, add an empty span to hang it on
            - need to make the span position: relative so you can position: absolute the ::before/::after

## Sat 17th
### Odin Project - Intermediate HTML & CSS   
- Read "Form Validation"
    - When an input is required, just add the 'required' attribute and put an asterisk/required label with ::before/::after
    - minlength and maxlength attributes set the allowed length of input
    - can use min/max attributes on number based inputs like number, date and time
    - can check it matches a pattern with 'pattern' attribute and regex argument
        - some input types already pattern validate, e.g. email and url
    - 'title' attribute can be used to provide a custom, more descriptive error message
    - 'placeholder' attribute can be used to set an example, placeholder value
    - You can validate inputs with custom JS as well, but the attributes are faster
    - Bookmarked a cheatsheet for form attributes, and a example for styling forms to help validation
- Finally finished reading, started working on the sign-up form project but for my ESL site, not the one they gave me
    - Reorganised my old ESL games site project that I made the landing page for, adding folders etc.
    - I really forgot a lot of HTML/CSS stuff haha, do still remember quite a bit though
    - Spent far too long being confused about why my styles weren't applying, turns out if you're in a child folder you need ../, not just / to go back one level
    - Created the basic components of the form
    - Eventually ended up setting up the two sections, with everything I currently have on the left in the correct place.
    - Added the site logo to the sidebar and fixed the lack of space in the attribution by putting it in a p, not div


## Sun 18th
### Odin Project - Intermediate HTML & CSS  
- Decided to actually read the project specs, added a background to the sidebar image and cleaned up some CSS rules which were handled in the site-wide.css or elsewhere
- Finished styling the form and button
    - figured out that you can chain :focus:valid to make required fields not red all the time/when empty
        - maybe another style for :empty?
    - but how do you make them red after something's been entered and it's invalid?
- Didn't validate the passwords being the same with JS as that's in a later lessons and I'll just do it then
- Called the project finished for now, though obviously I'll come back to the page as I continue to work on the site
- Started reading about CSS Grid, which is exciting because I've heard a lot of good things. Current belief before reading any of the Odin stuff is that Grid is best for overall page layout, flex for laying stuff out inside individual elements
- Yep the intro confirms those early impressions. Will continue on tomorrow. 

## Mon 19th
### Odin Project - Intermediate HTML & CSS  
- Grid is better at overlapping, and more consistent
- Most of Grid is defined on the parent element, but most of Flex is on the children
- Read 'Creating a Grid'
    - Can turn an element into a grid container by setting display: grid/inline-grid
    - each child element automatically becomes a grid item (only direct children)
    - Grid track is the space between lines in the grid. Column track is space between columns, row track between rows
        - explicitly define rows and columns with grid-template or grid-template-row/grid-template-column and a space separated list of sizes
        - names are automatically set to numbers from left to right and top to bottom, and from -1 from right to left or bottom to top
            - so you can span a whole row/col using start: 1, end: -1 
        - you can also name the row/column lines using [ name ] 50px
            - can have two names, just separate with a space inside the brackets
        - can avoid typing the same value repeatedly with repeat(times, values)
        - if multiple items have the same name, they can be referenced by the name followed by its name and count
        - fr unit lets you set track size as a fraction of total grid size (calculated after any non flexible items are added)
    - Extra rows can be implicitly defined for elements outside the explicitly defined rows/columns using grid-auto-rows and grid-auto-columns
        - you can define a pattern of implicit row/col sizes by separating the sizes with a space, same as for explicit
        - by default extra content is added below in new rows, so you won't need auto-columns
        - but you can set grid-auto-slow: column and they'll flow into new columns, so you need to set auto-column
    - Can set gap with row-gap, column-gap or the combined gap
- Read 'Positioning grid elements'
    - Grid tracks are what we create (the actual rows/cols), lines are implicitly created
    - Each track has a start and end line, e.g. 1 and 2 for the first row/col
    - Grid lines are used to position grid items
        - by using grid-column/row-start and the grid line number
        - also short-hand grid-row and grid-column, separated by a /
        - grid-area combines both col and row, all 4 separated by /
        - you can also set a name for the grid area, then lay them out with grid-template-areas in addition to the grid-template which creates the grid
            - grid-template-areas takes a string for each row, separated by spaces internally and lines externally of the items in the row
            - use a . to indicate empty cells
    

## Tues 20th
### Odin Project - Intermediate HTML & CSS  
- Did 01 folder practise exercises from the old CSS exercises repo
- Read 'Advanced grid properties'
    - Grid area can still only make rectangular areas
    - Officially learned about repeat(num, size [ name ]) for setting the grid template
        - you can set auto-fit and auto-fill as the number, which will return the largest number which won't cause your grid to overflow its container
        - works especially well with minmax etc. so you can have a dynamic number of rows/cols which is calculated using the min value, then they're resized up to the max value to fill the space
        - **only diff between auto-fit and auto-fill is when there aren't enough items to fill a single row. Auto fit will expand to the max size and attempt to fill the row, while auto-fill will fill the row with invisible columns**
    - Also fr, which allocates 1 fractional unit of the **remaining** space in the container after any fixed space is allocated
        - When you resize the grid to be as small as possible, individual cells won't become smaller than their content due to the grid item's min-content value
    - min() and max() (which return the min or max of a set of provided values) can be used with a collection of fixed and relative values to ensure minimum and maximum row/col sizes
    - minmax() is used specifically with CSS grid on template-rows/cols and auto-rows/cols to set a minimum and maximum row or col size
        - unlike with min() or max() it makes sense to use two fixed values
    - similarly, clamp(min, ideal, max) can be used
        - but here we use a relative value for ideal and fixed for min/max
- Did practice exercises 02 and 03
    - learned that you shouldn't define rows unless you have to, let the grid figure it out itself.
    - Also if you need elements in the grid to be a fixed height, just set it on the elements. Don't make the rows that height, it can lead to overflow
- Read "Using Flexbox & Grid"
    - Main point seems to be that you can use them both together, depending on which is better suited to a certain part of your page
    - Generally though, grid is better for the overall layout and flex is better for positioning stuff within cells of that overall layout
    - 1D vs 2D layouts is the most commonly cited differentiator, as Grid lets you explicitly define both while flex only lets you define one explicitly
    - Grid is more for precise placement, and if you want predictable behaviour at different viewport sizes. Also broken or asymmetrical layouts
    - Flex is for when you're more focused on the flow of the content, and want sizes to be defined by the size of the contents of the flex items
- Made it to the Admin Dashboard project, so I set up the files in the ESL site repo. Will start working on it tomorrow

## Wed 21st
### Odin Project - Intermediate HTML & CSS
- Finished the CSS Garden browser game 
- Admin Dashboard project
    - Created the overall layout using grid
        - There seem to be 7 rows even though I explicitly only defined 4 and there's no excess content?
        - Doesn't actually affect the layout though
    - Styled the header using site_wide.css
        - should look into a way of including the header and footer on each page without copying the whole thing
        - clamp doesn't seem to work on font-size?
        - one problem is that when I have a really narrow viewport the text doesn't resize, and it eventually stops shrinking/leaves content off the side of the screen
    - Styled the footer, also using site_wide.css
    - Styled the sidebar, using uls since it should look like a list
        - got the icons from feather, only history and home actually have live links
    - Styled the welcome bar
    - Styled the cards
        - after much confusion, realised that only direct children will span across the whole grid area. If there's a div with another div inside it, that div inside will stay stuck in a single cell
        - when you use auto-fit/auto-fill you have to use minmax() as well or it's invalid 
    - Does not look great on mobile, I used too many fixed sizes 
    - Is completely non-functional on Safari lol
    - But, it's done and looks good on Firefox/Chrome
- Finished Int HTML & CSS, plus I did the project in one day. Wooo!
- On to databases tomorrow

## Thurs 22nd
### Odin Project - Databases
- Read 'Databases'
    - used to store persistent data from your site, there's also caching but that's covered later
    - SQL underpins all relational databases, while stuff like MongoDB use a document model
        - relational databases are more "3D" than a simple table
        - forms data into well-defined units and relates them using 'keys'
        - primary keys **must** be unique, so they are usually equal to the primary key of the previous row/record incremented by one
        - Primary keys referred to in other tables are known as 'foreign keys', e.g. the keys for publisher and platform in a table of video games
    - did the Khan tutorial on SQL
        - create a table with "CREATE TABLE table_name (id INTEGER PRIMARY KEY, col_name DATA_TYPE, col_name DATA_TYPE);"
        - insert with "INSERT INTO table_name VALUES (values in order of table columns, comma separated);"
        - query with "SELECT col_name FROM table_name;"
            - can use * in place of col_name to select whole table
                - if you want to select multiple col_name but not the whole table separate with commas
                    - also works with aggregate functions, just separate with commas
            - can append WHERE (col_name <=>) to filter out results
            - can append ORDER BY col_name to order by the data in that column
            - can add an aggregate function (like SUM(col_name)) after SELECT to aggregate data from that column
                - can append GROUP BY col_name to get an aggregate for each row in that col_name
                - when you're selecting a col_name to display next to your grouped aggregates you wanna select the one you're grouping by

## Fri 23rd
Had to do some paperwork for the new job, cook for my date with Viktoria and go on said date today, so probably won't get much done. I'm writing this at 11:11, but I'll make sure to wake up early tomorrow and study hard. 

Yeah JOIN is too complicated for after 11pm, I'll continue tomorrow.

### Odin Project - Databases
- Read "Databases and SQL"
    - SQL likes lines to end with a ';' 
    - Use single quotes '' for strings
    - CRUD is Create, Read, Update, Destroy; not sure I've ever actually heard that before
    - Schema:
        - The file which stores the layout info for your database
        - updates whenever you change the structure of your database
        - possible to
            - only allow unique names in certain columns
            - use CREATE INDEX to index a col so you can search it faster later

## Sat 24th
### Odin Project - Databases
- Finished the assignment SQL tutorials; [SQL Teaching](https://www.sqlteaching.com/) made progress on [SQL Bolt](http://sqlbolt.com/)  
- You can nest SQL queries, e.g. "SELECT * FROM family_members WHERE num_legs = (SELECT MIN(num_legs) FROM family_members);" to get rows where the number of legs is equal to the minimum number of legs
- Dates are represented in the format YYYY-MM-DD
    - can be compared with < or >
- You can self-join using aliases to determine which is the left and right table

#### Query order of execution
1. FROM and JOINs

The FROM clause, and subsequent JOINs are first executed to determine the total working set of data that is being queried. This includes subqueries in this clause, and can cause temporary tables to be created under the hood containing all the columns and rows of the tables being joined.

2. WHERE

Once we have the total working set of data, the first-pass WHERE constraints are applied to the individual rows, and rows that do not satisfy the constraint are discarded. Each of the constraints can only access columns directly from the tables requested in the FROM clause. Aliases in the SELECT part of the query are not accessible in most databases since they may include expressions dependent on parts of the query that have not yet executed.

3. GROUP BY

The remaining rows after the WHERE constraints are applied are then grouped based on common values in the column specified in the GROUP BY clause. As a result of the grouping, there will only be as many rows as there are unique values in that column. Implicitly, this means that you should only need to use this when you have aggregate functions in your query.

4. HAVING

If the query has a GROUP BY clause, then the constraints in the HAVING clause are then applied to the grouped rows, discard the grouped rows that don't satisfy the constraint. Like the WHERE clause, aliases are also not accessible from this step in most databases.

5. SELECT

Any expressions in the SELECT part of the query are finally computed.

6. DISTINCT

Of the remaining rows, rows with duplicate values in the column marked as DISTINCT will be discarded.

7. ORDER BY

If an order is specified by the ORDER BY clause, the rows are then sorted by the specified data in either ascending or descending order. Since all the expressions in the SELECT part of the query have been computed, you can reference aliases in this clause.

8. LIMIT / OFFSET

Finally, the rows that fall outside the range specified by the LIMIT and OFFSET are discarded, leaving the final set of rows to be returned from the query.

#### Statements 
- ALTER TABLE
    - ALTER TABLE table_name 
        - ADD column DataType OptionalTableConstraint DEFAULT default_value
        - DROP column
        - RENAME TO new_name to rename the table
- COMMIT
- CREATE DATABASE
- CREATE TABLE
    - CREATE TABLE table_name (col_name DATA_TYPE TABLE_CONSTRAINT(opt) DEFAULT default_value(opt), ...)
    - IF NOT EXISTS skips creating the table and suppresses the error if the table already exists
    - col names must start with a letter and can contain letters, numbers and underscores. Don't use SQL keywords like 'select'
    - must be less than 30 characters long
    - Data types are all the usual suspects plus blobs, but those are difficult to find without the right metadata since they're opaque to the database
        - INT, BOOLEAN, FLOAT, DOUBLE, REAL
        - CHAR(num) and VARCHAR(num) are specified with the number of characters they can contain, making them more performant
            - CHAR sets a fixed length
            - VARCHAR sets the max length
        - DATE/DATETIME store timestamps, as expected can be tricky to work with, especially across timezones
        - NUMBER(size, d) size is max total digits, d is decimals
    - Table constraints limit the values which can be inserted
        - PRIMARY KEY - values must be unique and are used to identify rows
        - AUTOINCREMENT - for ints, value is automatically incremented and filled in when a new row is created. Not universally supported
        - UNIQUE - doesn't allow duplicates, diff from PK because it doesn't have to be a key for a row in the table
        - NOT NULL - inserted value can't be null
        - CHECK(expression) - allows you to store a complex expression which checks if the values are valid
        - FOREIGN KEY - Checks each value in this column corresponds to a value in another table
- DELETE:
    - DELETE FROM table WHERE condition
    - Make sure you use a WHERE clause, or you end up deleting all your users
    - can chain WHERE clauses with AND/OR/NOT and use the usual comparison operators
- DROP DATABASE
- DROP INDEX
- DROP TABLE
    - Different from DELETE because it deletes the table schema as well
    - Use IF EXISTS to suppress the error if the table doesn't exist
    - If the table you're dropping has foreign keys in other tables, you'll need to alter them to remove that column or drop them entirely too
    - I think you have to update the columns in the other tables **before** dropping the table
- INSERT INTO
    - can insert multiple rows at once by putting them one after the other in brackets, separated by commas
    - can use math and string expressions on the data you're inserting, e.g. divide by 1 million for "millions of dollars" col
    - You can title the columns explicitly after the table name and before VALUES in case you only want to insert values for certain columns
- JOIN
    - Used to zip tables together
    - You can chain joins to get data from relational tables in a database e.g.
    ```
    SELECT character.name, tv_show.name
    FROM character
    INNER JOIN character_tv_show
    ON character.id = character_tv_show.character_id
    INNER JOIN tv_show
    ON character_tv_show.tv_show_id = tv_show.id;
    ```
    - ON specifies the column to zip on e.g. ON users.id = posts.user_id
    - INNER JOIN keeps only the rows where the specified ON value exists in both tables
    - FULL OUTER JOIN produces a set of all records from the two tables. If no match, missing side will contain null
        - for records unique to either table, use WHERE and OR to select any record matched by a null value
    - LEFT OUTER JOIN produces a complete set of records from table A, with matches from B if possible and null if not
        - if you only want records that exist in table A and not B, append WHERE tableB.id IS null to select them
    - RIGHT OUTER JOIN is the opposite of left
    - CROSS JOIN joins everything to everything, so very dangerous to run on large tables
- ROLLBACK
- SELECT:
    - best practice to specify table name for the col like users.name or users.email
    - also have SELECT DISTINCT to get a list of all different usernames e.g. SELECT DISTINCT users.name FROM users
        - you actually prepend DISTINCT to the column name you want distinct values for, it's not a modifier on SELECT
- UPDATE
    - UPDATE table_name SET col = value, ... WHERE condition
    - make sure your WHERE is unique if you only wanna update one thing, or it'll update everything that matches

#### Clauses
- ALL
    - if you put it on the right side of the operator, lets your compare the left side to a list of values on the right side
- AS
    - lets you rename columns or aggregate functions or tables to call them later, e.g. "SELECT MAX(users.age) AS highest_age FROM users" returns a column called highest_age
    - goes directly after the thing you want to rename
- AND
- BETWEEN
    - use with AND to set a range e.g. BETWEEN 10 AND 1
    - can be modified with NOT
- COUNT
- DISTINCT
- IN
    - used with WHERE (like WHERE species IN ('cat', 'human')) to return records with a species that is cat or human
    - NOT IN is to find records where the value is NOT in the list
- LIKE
    - search through text-based values
    - special characters are % (representing 0, 1 or multiple characters) and _ represents one character
        - e.g. LIKE "super _" would match super 1, super a, super *
        - LIKE "super %" would match anything with super at the start, including super on its own
        - LIKE queries are not case sensitive
- LIMIT
    - use if you want to only get a few records from a large database
    - e.g. LIMIT 2
    - not available to all versions of SQL
    - can add an OFFSET to specify where the LIMIT should start counting from
    - goes after DESC if both are used
- OR
- ORDER BY
- WHERE
    - adds conditions to your query
- XOR 
    - like or, but only selects rows where one of the conditions is true, not both


#### Functions 
- AVG
- CASE
    - returns a certain value when selected values are fed in
    - syntax is CASE WHEN *conditional* THEN *value1* .... ELSE *value for all other situations* END 
    - e.g. to create a new named column SELECT*, CASE WHEN *conditional* THEN *value1* .... ELSE *value for all other situations* END AS new_col_name FROM table_name;
- COALESCE
    - takes a list of columns as arguments and returns the first non-null value
- COUNT
    - does not count NULL values
- You can use DAY(col), MONTH(col) and YEAR(col) to extract those values from a date value in a col
 - WEEKDAY(col) = 0 for Monday
- DATE_ADD(date, INTERVAL num week/day/month/yr)
    - Allows you to add number of interval to date
- DATE_FORMAT(date, template)
    - lets you format the date using the template
- HAVING
    - is WHERE for aggregate functions, you use the AS name you gave the aggregate function in the conditional (but maybe not? Didn't work in the example)
- LAG(col to lag, lag amount) OVER (PARTITION BY col ORDER BY col)
    - used to show data from preceding rows of the table
- LEAD(col to lead, lead amount) OVER (PARTITION BY col ORDER BY col)
    - used to show data from following rows of the table
- LENGTH
    - LENGTH(col) returns the length of the values in col
- MIN
- MAX
- ORDER BY
    - add a DESC to the end of the query to put in descending rather than the default ascending order
- RANK() OVER(PARTITION BY col ORDER BY col) AS col_name
    - ranks the rows by the ORDER BY value in a new col
    - PARTITION BY groups by the col you provide
- SUBSTR
    - syntax is SUBSTR(col_name, index, num_of_characters) which returns a string from the index for the number of characters
    - index can be negative to indicate distance from the end of the string
    - number of characters is optional, if omitted it'll just return the rest of the string from the index onwards
- SUM
- Can use on all columns with *
- Can include in a select statement like SELECT MAX(users.money) FROM users

## Sun 25th
### Odin Project - Databases
- Finished [SQL Bolt](http://sqlbolt.com/). Notes from them are above to avoid fragmentation
    - Remember **no spaces in numbers** in SQL
     
## Mon 26th
### Odin Project - Databases
- Finished SQL Course [beginner](https://www.sqlcourse.com/beginner-course/)/[advanced](https://www.sqlcourse.com/advanced-course/). Notes from them are above to avoid fragmentation
- Did the first 4 sets from SQLZOO, the project for the database section
    - Notes on each task from that project are (here)[https://github.com/Brett-Tanner/SQLZOO/blob/main/README.md]

## Tue 27th
### Odin Project - Databases
- Finished up to set 9 from SQLZOO, the project for the database section
    - Notes on each task from that project are (here)[https://github.com/Brett-Tanner/SQLZOO/blob/main/README.md]

## Wed 28th
### Odin Project - Databases
- Finished SQLZOO, the project for the database section
    - Notes on each task from that project are (here)[https://github.com/Brett-Tanner/SQLZOO/blob/main/README.md]

### Odin Project - Ruby on Rails
- Started looking at deploy options
    - Since Heroku free tier is gone (RIP) and that's what the materials are based on, I'll have to find my own
    - Shortlisted Supabase, Fly.io, Render and Railway
    - Cut it down to Render and Railway as they seem the most helpful/explicitly support Rails
        - will try both for a while and see which is easier/better, then pick one
- Installed Rails and created the test project. Got up to deploying it but it's after midnight and this could get complicated since I'm not using Heroku, so I'll continue tomorrow.

## Thurs 29th
### Odin Project - Ruby on Rails
- Yep deploying to other hosting services is tricky when all the instructions are for Heroku
    - had some issues with how to migrate a PG database to Railway when the gem isn't installed in my local env
    - tried Render next
        - internal database url: (postgres://my_first_rails_app:IWf0odHWEPxRMXVlYtOloTyLQl4Uv0rU@dpg-ccqg44sgqg4cmrh60c20-a/my_first_rails_app)[postgres://my_first_rails_app:IWf0odHWEPxRMXVlYtOloTyLQl4Uv0rU@dpg-ccqg44sgqg4cmrh60c20-a/my_first_rails_app]
        - seems Render is easier, you just follow directions from the (Rails Deployment tutorial)[https://render.com/docs/deploy-rails]
        - Finally got it working after being more thorough about the environment variables I added in database.yaml and the Render dashboard
- Read 'A Railsy Web Refresher'
    - The main 4 HTTP request verbs are GET, SET, PUT and DELETE but there are others. These days almost everything is done through GET or SET.
        - GET fetches a resource
        - SET creates a resource
        - PUT modifies
        - DELETE deletes
    - HTTP requests and responses both have header and body components
        - header contains meta-info about the request/response
        - body contains stuff like data submitted by a form or cookies for a request or the HTML you're trying to access for a response
    - REST (representational state transfer) is the idea there are only 7 things you really want to do to an individual web resource, and they can all be done with the HTTP verbs
        1. GET all the posts (aka “index” the posts)
        2. GET just one specific post (aka “show” that post)
        3. GET the page that lets you create a new post (aka view the “new” post page)
        4. POST the data you just filled out for a new post back to the server so it can create that post (aka “create” the post)
        5. GET the page that lets you edit an existing post (aka view the “edit” post page)
        6. PUT (or PATCH) the data you just filled out for editing the post back to the server so it can actually perform the update (aka “update” the post)
        7. DELETE one specific post by sending a delete request to the server (aka “destroy” the post)
            - the long way of implementing that for a controller would be:
            ```
            get "/posts", to: "posts#index"
            get "/posts/new", to: "posts#new"
            get "/posts/:id", to: "posts#show"
            post "/posts", to: "posts#create"  # usually a submitted form
            get "/posts/:id/edit", to: "posts#edit"
            put "/posts/:id", to: "posts#update" # usually a submitted form
            delete "/posts/:id", to: "posts#destroy"
            ```
                - :id means save anything here as the id in the params hash
                - several submit to the same URL, but because the HTTP verb is different they're submitted to different controllers
            - but in Rails, there's a shortcut to do all these common routes
            ```
             # in config/routes.rb
            ...
            resources :posts
            ...

            ```
    - Words in quotes correspond to Rails controller actions
    - In a URL, path is everything after the /, and parameters are the key/value pairs in the path
    - MVC
        - When a request comes from a client comes in
            1. The router (server) figures out which controller to send it to
            2. The controller asks the model for data
            3. The controller gets the data and passes it off to the views
                - views are just HTML templates waiting for the values
            4. Once the correct view has been filled with the data, it's sent to the client
        - So for the individual components
            - Controller receives requests from the client, gets the data and shuttles it around
            - Model has all the data, it communicates with the database
            - View is what the client sees/gets, is stored in your project as templates
        - API
            - how two applications talk to each other
            - usually doesn't return HTML, it's JSON or something instead
            - still uses HTTP, in fact that's how Rails components communicate with each other
            - to create an API mostly just tell your controller to respond to server requests and what you want it to respond with
        - Cookies
            - basically a way to remember who you are from one request to another, since HTTP requests are stateless
            - your browser sends the cookie each time it communicates with the site, so the site can preserve the state of your interactions
            - also stores login info, user preferences
        - Authentication tells you who the user is, authorisation tells you what the authenticated user can do
- Started reading 'Routing'
    - Router is the 'doorman' of your app
    - Looks at the HTTP request and matches it with the appropriate controller action to run
    - will throw an error if it can't find a route that matches the request
    - Makes parameters from the request available in a special hash called 'params' that can be used in the controller
    - the routes file in config/routes.rb has a link to the Rails Guide routing section
    - typing $ rails routes into cmd line will give you a list of all routes available to your app
        - they show in the format "route name   HTTP verb   URL    controller action"
            - (.:format) just means it's ok to specifiy a file extension at the end of the route
    - map the root URL (homepage) with 'root to: "controller, action(the method called action in controller)"
    - route helpers are automatically created for all your routes using the route name e.g. for edit_post
        - edit_post_path provides the path to the edit post link
        - edit_post_url provides the full URL
        - can put any parameters in () after either
    - link_to "text" name_path/_url creates a link using the text and the generated path/URL

## Fri 30th
### Odin Project - Ruby on Rails
- Continued reading 'Routing'
    -










### Odin Project - Ruby Foundations
- When making a move
    - 

- When checking for checkmate
    - 