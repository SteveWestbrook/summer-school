## LESSON 10 - Jumping

Making our little cat jump is going to take a few different steps.  The first thing we're going to do is set up our cat's position.  Before, we just got the middle of the screen, and put him there every time we drew him, but now, we want to move him around, so we're going to make that his *starting* position instead.

Go to the onload function again.  Right under `self.ready = true;` write these lines:

```
        const middle = getMiddle({ width: 16, height: 16 });
        self.position = middle;
```

This doesn't really do much - it just gets the same middle position, and stores it (in self.position) - that way it can be used somewhere else later.

Now, in the draw function, around line 32, find where it says `middle.x, middle.y`.  Replace that with `self.position.x, self.position.y` and you should be ok.  Reload the page to make sure it still works.

Now we have a position.  Soon, we'll be able to change the position our cat is in, but first, we have to give the player a way to do it.  Just above this line:

```
    this.draw = function() {
```

Add a new function, called jump:

```
    this.jump = function() {
        if (self.jumping) {
            return;
        }

        self.jumping = true;
        self.upwardSpeed = 2.0;
    }
```

This actually just sets up our cat for jumping - it says that yes, we're jumping (self.jumping = true) and it sets the speed at which we'll move up, which is 2.0.  At the beginning, it checks to see if self.jumping is true - if it is, it calls `return`, which as you may remember, will exit the function.  If you didn't have this in there, then your cat could jump again in mid-air!

Next we'll write the code to actually jump.  This goes in the `this.draw` function, just under the part on lines 32-34 that says 

```
        if (!this.ready) {
            return;
        }
```

It's a big chunk, but here it is.

```
        // Update position
        if (this.jumping) {
            this.position.y -= this.upwardSpeed;
            this.upwardSpeed -= 0.1;

            const middle = getMiddle({ width: 16, height: 16 });
            if (this.position.y >= middle.y) {
                this.jumping = false;
                this.position.y = middle.y;
            }
        }
```

Read carefully what this does, because you've seen these things a few times, so it's time to really learn them.  Let's go line by line:
`if (this.jumping)`

This checks whether `jumping` is set to `true`.  Remember that we did that inside the `jump` function.  If you're not `jumping`, this whole block won't get run.  You can see how much code is inside the `if` statement by looking at where it starts - with a { - and where it ends, with a }.  Notice that there's another } *inside* the if statement block.  That's for another `if` statement - the two of them are "nested," which means that one is inside the other.

Next line:

`this.position.y -= this.upwardSpeed;`

Remember when we set the `position` to the middle of the screen?  Now we're modifying it.  The `y` tells us how far we are from the top of the screen, so when we subtract from it, we go up.  That's what `-=` does - it means this.position.y should be made this.position.y MINUS this.upwardSpeed.

Next, we have this:
`this.upwardSpeed -= 0.1;`

You know when you jump that you start out fast, then slow down, and then reverse direction and fall to the ground.  So each time we go through the game loop, we subtract a little bit from the `upwardSpeed` value.  That way you'll go up, pause, then come down.  This is very simple, but you'll see it's surprisingly accurate.

Next, with `const middle = getMiddle({ width: 16, height: 16 });`, we get the `middle` again.  We are getting the position of the ground, so that we can stop jumping when we hit it.

Now,

`if (this.position.y >= middle.y) {`

we check the `middle` against our `y` value.  If our cat is at the middle, or below the middle (sometimes if you just keep adding, you'll fall through the ground!), we go inside the `if` block.  It has two statements:

```
                this.jumping = false;
                this.position.y = middle.y;
```

We set `jumping` to false, so our cat stops jumping, and then we make sure the cat is right on the ground, with the second line.  Without that second line, it wouldn't be so bad, but our cat might sometimes appear a little bit below the ground after he jumped.

## Handling the keyboard.

Now, we want to give the player a way to make the cat jump.  We'll use the spacebar for this.

At the bottom of the file, right on the very last line, put this:

```
window.onkeydown = function(e) {
    if (e.key == ' ') {
        cat.jump();
    }
}
```

That is a special function called an "event handler."  When the window (the window that you're running the game in) sees that the user has pressed a key, it calls this function for you.  `e` (short for `event`) has some useful information, including the key that was pressed.  In our case, we care about the spacebar, which makes a space: ' ', so that's what we check.  And to start the process off, we just call `cat.jump()`.

If you reload your browser now, and if everything worked, you should be able to make your cat jump by pressing spacebar.  If you have trouble, hit F12 in the browser and see if it tells you which line is causing problems.

