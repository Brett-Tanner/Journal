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


## Sat 17th
### Odin Project - Intermediate HTML & CSS  
- 



### Odin Project - Ruby Foundations
- When making a move
    - 

- When checking for checkmate
    - 

