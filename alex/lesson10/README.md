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

Then finally, at the bottom of the file, right on the very last line, put this:

```
window.onkeydown = function(e) {
    if (e.key == ' ') {
        cat.jump();
    }
}
```

Add this to the bottom of the file:
