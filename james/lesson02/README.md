# LESSON 2 - Some Python Programming

## What is Python?
Python is a computer programming language used by the scientific community, as well as by regular programmers.  It has a lot of similarities to other programming langues, but it has some superficial differences that make it look quite different from many others.

The easiest way to run python is in "interative" mode.  Open a terminal and type 

`python3`

To start python version 3 (this is the new one - after many many years of use, python 2 is being phased out).

You will see something like this:

```
Python 3.7.3 (default, Dec 20 2019, 18:57:59)
[GCC 8.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

The `>>>` at the bottom tells you it's ready to go.  You can ask it questions - this is valid python code:

```
>>> 2 + 2
```

Hit enter, and you will see the result.

You can also store python programs for later use.  Exit python now, by typing `exit()` or pressing Ctrl-D.

We'll use VS Code for the next part.

## Writing and storing a Python program

In a terminal, create a new directory - let's call it `~/programming/practice`.  The `~` means that it's in your home folder - that's where you start when you open a new terminal.

In VS Code, navigate to the directory you just created with

File > Open Folder

Now on the left-hand side, you should see "practice" under a couple of other headings.  Beside "practice" there are some icons - hover over the first one and it should say "New File."  Press it, and name your file `plus.py`.  Double click the file if it hasn't opened already.  Then in the file, write this:

`print(2+2)`

And save the file (Ctrl-S).  Now switch to your terminal, and make sure you're in the right directory:

`cd ~/programming/practice`

then run the program

`python3 plus.py`

You should see the output

## Repeating a job
What if you want to add numbers other than 2 and 2?  For this, you would want to ask the user what numbers they want, and then output the result.  Go back to plus.py and delete the line you have in there.  Write these lines:

```
x = input('Enter a number\n')
y = input('Enter a second number\n')
```

We're getting variables for two numbers - those numbers are going to be called x and y.

Notice the text we're using to ask the user for numbers:

`Enter a number\n`

What's that `\n` at the end?  Well, that is called a "newline," and is denoted by a special character combination, \n.  There are others - \t is the same as pressing Tab on your keyboard, for example.

So now we have two numbers, x and y.  How do we add them?  Well... first, we have to make them numbers!  That may seem strange, but what you got just now was text - it could be anything - you could type in "abc" instead of a number.  So we need to convert x and y to numbers:

```
x = int(x)
y = int(y)
```

`int` is short for "Integer," which means a whole number, i.e. 1 or 10 or 547, and not 1.5 or 3.227171.  If the user has put non-numeric values into x or y, the program will output an error here and shut down.

Now we have our two numbers, so all we have to do is add them and print the result:

```
print(x + y)
```

Notice that the computer is happy to convert the numbers to text - that's because unlike converting text to numbers, it's not possible to lose information.  All numbers can be represented as text, whereas not all text is necessarily a number.

Now save your program again.  Switch to the terminal and run it.  You should see the output.  If not, go back and make sure all your code exactly matches what's here.

## Getting Fancy
Now you'll notice that at the end, we just see a number plunked onto the screen without any explanation.  Maybe we're writing a more complicated program than "Add two numbers" and we want to make sure the user knows what they're getting.  So let's try this instead:

```
print(f'{x} + {y} = {x+y}')
```

This is a little more complicated, but what's going on is that we can embed our variables into a "string" - which is the programming word for text - if we put the letter `f` in front of the string, and put { and } around the variables.  You can even put little equations like `x+y` in there if you want, although it is in poor taste to jam too much into a string like this.

## Some convenient operations

In scientific notation, you'll see numbers written like this:

6.67430 × 10<sup>-11</sup>

This is relatively hard to represent in python, in that you need to do a few steps.  First, you need to go to the very top of the file and enter

```
import math
```

Which will tell you that you want to use python's math library.

Then you want to set a variable with all the parts:

```
G = 6.67430 * math.pow(10, -11)
```

Notice that `*` means "multiply" in python.  `math.pow(10, -11)` means 10 to the power of -11, which is equivalent to 0.00000000001 if I have counted the zeroes right.  (Other examples: 10<sup>-1</sup> is 0.1, 10<sup>1</sup> is 10, 10<sup>2</sup> is 100, 10<sup>3</sup> is 1000, etc.)

To divide numbers, use `/`.  So 10 * 3 / 2 would be 10 times 3 divided by 2.

## A real program
Now, make a new file and write a program to calculate the force of gravitational attraction between two objects.  Get the distance between the objects, and their masses from the user.  You can set the gravitational constant directly, since it's, well, constant.  Instead of `int`, you should use `float`.  `float` is also a number, but it allows for decimal places.

This is expected to take you a fairly long time.  I believe all the information you need is present in the lesson above, so try hard to bring it all together.

