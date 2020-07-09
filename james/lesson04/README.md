# LESSON 4 - Storing files

I'm going to try an experiment here - try reading section 7.2 of https://docs.python.org/2/tutorial/inputoutput.html.  Start at 7.2, and go all the way to the bottom of the page.  Some of it's new, and pretty complicated, but you have enough background now to make an attempt at it.

When you're done, here is a "capstone" program for this section:

When the program enters, give users the option of entering a new planet - let them keep entering planets with y/n until they say n.  When you have a planet, add it to a file - create the file if it isn't there, or add to the existing file if it is.

Each planet should have a mass (have them enter it in millions of kilograms, i.e. 1.5 means 1500000kg), and a position in xyz coordinates - each of x, y, and z should be a number that we will use for millions of kilometers later.

You can make a complicated variable to store this sort of information like this:

```
planet = {}
planet.m = 1.5
planet.x = 2.5
planet.y = 3.4
planet.z = 4.3
```

And then use json storage to write that to a file.

Finally, add a feature so that at the beginning of the program, all planets currently in a file are printed on the screen.

This is super challenging and will take a long time.
