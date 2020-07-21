# LESSON 9 - Animating your cat

We have spent a whole lot of effort on making a couple of cats.  Hopefully you can now display the pair of cats on the screen.  If not, go back and finish off your last lesson.

Today we are going to make our little cat run.  We will do this by rapidly switching out the two images you have made, creating the illusion of a running animal.

## More cleanup yet again

The way we draw a sprite is going to start getting a little more complicated.  We'll organize our code by moving it around a little.

First we'll add a draw function to the cat.  Go to near the top of the game.js file.  Look for this:

```
    this.image.onload = function() {
        self.ready = true;
    }
```

Right underneath that, add this code:

```
    this.draw = function() {
        if (!this.ready) {
            return;
        }

        const middle = getMiddle(this.image);
        context.drawImage(this.image, middle.x, middle.y);
    }
```

Let's go through this line by line so you know what it does.

First, this:

```
        if (!this.ready) {
            return;
        }
```

This is saying "if this is NOT ready" - that `!` means not - get out of the function (`return`).  Once you call return, nothing else in the function will happen.  The program will go back to the parent function.

Next, the previous stuff:
```
        const middle = getMiddle(this.image);
        context.drawImage(this.image, middle.x, middle.y);
```

This is almost the same as the code you put into the gameLoop function.  It gets the middle of the canvas and puts the cat on it.

Now, go and replace the old code.  Down near the bottom of the file, find these lines:
```
    if (cat.ready) {
        const middle = getMiddle(cat.image);
        context.drawImage(cat.image, middle.x, middle.y);
    }
```

Delete them.  Replace them with this:
```
cat.draw();
```

That will run the code you just wrote up in the Sprite object.  That's because cat is a kind of Sprite - you made it one when you wrote `cat = new Sprite('./cat.png')`.

Now refresh, and you should still see your two cats standing side by side.

## Clipping the cat
Obviously, we don't want to show both cats at the same time.  What we're going to do is clip out part of the image so that only one cat is showing at each time.  Then every little while, we'll switch out which one is showing.

First, we'll set up the "frame" (which cat) we want to show.  Right under the line that says `this.ready = false;` (it should be around line 8), add this line:

```
this.frameIndex = 0;
```

This tells us which cat - #0 or #1 - to show.

Now, in the draw() function, find this line:

```
        const middle = getMiddle(this.image);
```

This finds the middle.  But soon, we won't be showing the whole image, so we'll change it so it knows we are only showing a 16x16 part of the image:

```
        const middle = getMiddle({ width: 16, height: 16 });
```

Next, find this line:

```
context.drawImage(this.image, middle.x, middle.y);
```

We're going to change it so that it looks like this:

```
        context.drawImage(this.image,
            16 * this.frameIndex,
            0,
            16,
            16,
            middle.x, middle.y, 16, 16);
```

That's a lot bigger, isn't it?  There's a lot more going on.  Basically, the 16 * this.frameIndex says we either want to show the first cat or the second one.  The other stuff says we want to show a 16x16 image.

Now refresh.  You should see only one cat - the first one.

## Making the cat run
Finally, we want to make the cat run. This actually isn't all that hard - we have done most of the work already!

Find the `image.onload` line.  It should be around line 12.  Change it so it goes from this:

```
    this.image.onload = function() {
        self.ready = true;
    }
```

to this:

```
    this.image.onload = function() {
        self.ready = true;
        this.timer = setInterval(function() {
            self.frameIndex++;
            self.frameIndex = self.frameIndex % 2;
        }, 100);
    }
```

Make sure you get all the {} curly brackets in the right places.

There are a few things to look at here.  First, there's this:

```
setInterval(something, number);
```

This is a special function.  It calls the `something` function every `number` milliseconds.  There are 1000 milliseconds in one second, so when we use 100, that means we'll call our function 10 times every second.

Save your file, then reload.  Your cat should be running!
