# LESSON 3 - Functions, loops, if statements, and arrays

# Functions
In case you don't have it sorted out yet, here is how to write a function:

```
def thing(toPrint):
	print('Hi')
	print(toPrint)
```

And here is how to call that function:

```
thing('xyz')
```

There are several parts to this short piece of code:
- `def` tells python that you are defining a function
- `thing` is the name of this particular function - notice that's how you "call" it, which means running the code
- `toPrint` is an "argument", which means a piece of information you can pass into the function.  You can make a function with multiple arguments by separating them with commas:
	`def otherThing(firstArg, secondArg):
- `:` is even important.  At the end of a line, the : tells you that you need to indent, i.e. press tab.  Any code indented belongs to that function, and the function ends when you have non-indented code.  For example:

```
def abc():
	print('This is in the function')
print('This is not in the function')
```

To make sure you have this right, enter the code above into a new file called `functions.py`, and make sure it prints what you send to the function.

# Loops and if statements
There's another kind of block that has lines that belong to it.  A "loop" is something you make when you want to do something similar several times.  The basic example is making sure someone enters valid input.  Let's look at an example like that.  Open a new file, name it `loops.py`, and put in the following code:

```
def check():
    valid = False
    while not valid:
        result = input('Continue? (y/n)')
        if result == 'y' or result == 'n':
            valid = True

	return result

print(check())
```

There's a lot to unpack there.  First there's the function, but you should probably know that.  Then there's the loop, which starts with `while`.  It's pretty much what it says: as long as the `valid` variable is False, and not True, keep looping.  Everything that is below that is part of the loop, down to `check()` - you know that because of the indentation.

Next comes something you should be familiar with - `result = input` etc. - we're getting a piece of information from the user.

Finally, and if statement.  An if statement will only run the indented code below it if it's "true".  In our case, we have a couple of options.  `result == 'y'` will be True if the user entered 'y', and `result == 'n'` will be True if... you get it.  Because there is an `or` in the middle, either one can be true and the code inside the if statement will run.

`valid = True`

Remember the while loop?  Keep looping while not valid.  Well, now valid is true.

So, the whole block will keep running until the user enters y or n.  Then, the result the user enters will be "returned" from the function, which means that it will be sent back to whomever called it.  So this:

```
print(check())
```

Will print the result of the function, y or n.

Try it out!
