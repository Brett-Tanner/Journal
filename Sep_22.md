# September 2022

## Fri 2nd
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
-