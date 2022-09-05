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