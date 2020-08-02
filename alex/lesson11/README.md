## LESSON 11 - Getting Ready for the Hills

Today we're going to add hills to the game for the cat to jump over.  This is going to take a few different steps.  We'll start by making some changes to our code to allow for new hill sprites.

You remember that we made an object called Sprite to hold all the stuff we needed for the cat.  Well, now some of that stuff will be useful with hills, so we're going to split the code into the basic Sprite and a Cat object that is related.  All of the stuff that only matters for the Cat is going to go into the new object, but it will be able to use all of the stuff in the Sprite because of "inheritance," which means that the Cat builds on what is in the Sprite.

First things first: Go to the line underneath the Sprite object.  Remember that functions and objects are like this:

```
function xyz() {
  (here is a bunch of stuff)
}
```

So when I say underneath the function or object, I mean under that last }.  This can get complicated, because there are sometimes {} within functions, so make sure that you have the correct one.

Once you've found the right place, put in this:

```
function Cat() {
    Sprite.call(this, './cat.png');
}

Cat.prototype = new Sprite;
```

This basically makes the "Cat" object take everything from Sprite.

Now go to where it says `cat = new Sprite('./cat.png')` and change it to say `cat = new Cat()` instead.

Save, and reload the page.  The cat should still be there, and should still work and everything.

Now we'll go through and make the code more generalizable.  Start with the line at the top of Sprite:

```
function Sprite(path) {
```
 
Add a "frameCount" parameter:

```
function Sprite(path, frameCount) {
```

And then underneath, save it

```
this.frameCount = frameCount;
```

We'll use this below.  On line 19 or so, you'll see this:

```
self.frameIndex = self.frameIndex % 2;
```

Change that to use the frameCount:

```
self.frameIndex = self.frameIndex % self.frameCount;
```

This is in the code that makes our cat run.  The hills won't update, so they'll only have one "frame," where our cat has 2 - the running frames.

We need to tell the program that we're giving the cat 2 frames.  Go to where we call Sprite, inside our new Cat object:

`Sprite.call(this, './cat.png');`

And change it to provide that information:

`Sprite.call(this, './cat.png', 2);`

There's one more thing to do for this part.  In the onload function, we're setting the position of our cat to the middle of the screen.  We want to do that for the cat, but we don't want to do that for the hills, so we're going to move that somewhere else.

First, make a new "initialize" function in the Sprite object.  Right under the place where all the things are assigned (on line 12 or so), add this:

```
    this.initialize = function() {
    }
```

This is just an empty function that we will "override" in the Cat object.

Find these two lines around line 18-19:

```
        const middle = getMiddle({ width: 15, height: 16 });
        self.position = middle;
```

Cut them out of there, and replace them with this: `self.initialize();`.

Move the two lines you just cut out into the Cat function, along with the same initialize declaration, right under the call to `Sprite.call`:

```
    this.initialize = function() {
        const middle = getMiddle({ width: 16, height: 16 });
        this.position = middle;
    }
```

That's the most complicated part for a bit - the next function, the jump function, we'll just move right over into the Cat.

Take this code:
```
    this.jump = function () {
        if (self.jumping) {
            return;
        }

        self.jumping = true;
        self.upwardSpeed = 2.0;
    }
```

And move it in to the cat, so that the whole Cat looks like this:

```
function Cat() {
    Sprite.call(this, './cat.png', 2);
    this.initialize = function() {
        const middle = getMiddle({ width: 16, height: 16 });
        this.position = middle;
    }

    this.jump = function () {
        if (self.jumping) {
            return;
        }

        self.jumping = true;
        self.upwardSpeed = 2.0;
    }
}
```

Save and reload - everything should work.

No we are going to split up the two steps of the game loop - update and draw.  In the Sprite object, below the initialize function, add a new `update` function:

```
	this.update = function() {
	}
```

Then, call it from the draw function.  Just below this block:

```
        if (!this.ready) {
            return;
        }
```

Add the call:

```
this.update();
```

Add an update function to the Cat as well -	Right at the bottom of the Cat object, add the same update declaration:

```
    this.update = function() {
    }
```

Now, go back to the draw function in the Sprite, and find where the cat's jumping is done:

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

Take all of this, cut it out, and paste it inside the update function in the Cat object.

Save, and reload.  Everything should work, including jumping.

