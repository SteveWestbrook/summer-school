# LESSON 7 - Adding to What We Have

We're going to do a couple of different things today.  First, we're going to move the image you are rendering into a more appropriate position, and we're also going to organize our cat so that it's separate from the rest of the code.

## Starting the game (loop)

The way a game works is that it loops through a set of instructions over and over again.  We're going to do that now - we won't do anything in the loop, but we'll set it up, so that we can start showing things later.

First, add a new function to the very bottom of `game.js`:

```
function gameLoop() {
}
```
This is a bit of code that doesn't do anything yet.

Now, we're going to add a line inside the `setup` function.  Look for this line in your code:

```
function setup() {
```

Right underneath it, add this line:

```
    setInterval(gameLoop, 25);
```

What does this do?  `setInterval` is a special JavaScript function.  It tells us to run the function we want every little while.  In this case, we have said the function is `gameLoop`, and the time between running it is 25 milliseconds.  That's 0.025 seconds - this will run 50 times every second!

## Things are getting complicated

Before, we loaded our cat image and showed it on the screen.  But we are going to have a lot more than a single little cat to show.  We need to organize things, and all of the things we load have a lot in common.  So we're going to make something called an "object."  An object holds a bunch of information about something - in this case our cat.  Let's start simple - put this code right under your `var`s:

```
function Sprite(path) {
    this.image = new Image();
    this.image.src = path;
	this.ready = false;
    const self = this;

    this.image.onload = function() {
        self.ready = true;
    }
}
```

Remember when you made the cat image show up?  This does mostly the same thing, but this time you can pass anything you want to it - it can be a cat or something else.  It makes the image, loads it, and when the image is loaded, it makes it ready.  It doesn't draw it yet - that comes later.

Now, under your `setInterval` line (the one you just wrote a little while ago), add this:

```
    cat = new Sprite('./cat.png');
```

That makes a new Sprite - it runs the code in the funtion you just finished.  But because you put `new` in front of it, it makes an "object" instead of just running the code.  That means you can make lots of these.

Now we have a new kind of `cat`, so we want to delete the old one.  Delete these lines:

```
    cat = new Image();
    cat.src = './cat.png';
```

Also delete this:

```
    cat.onload = function() {
        const middle = getMiddle(cat);
        context.drawImage(cat, middle.x, middle.y);
    }
```

Oh my.  We have deleted the code that shows the cat!  Not to worry.  We're going to add it back in.

Go to your gameLoop function:

```
function gameLoop() {
```

Right under that line, put this:

```
context.clearRect(0, 0, canvas.width, canvas.height);
```

This will wipe out everything on the canvas, from top left (0, 0) to bottom right (canvas.width, canvas.height).  Why do we do this?  Otherwise, when we updated, the old things we saw would remain there.

Under that line, draw the cat, if it's ready to draw:

```
    // Draw cat
    if (cat.ready) {
        context.drawImage(cat.image, 0, 0);
    }
```

Now, if you reload the page, you should see your cat again.

## Move That Cat

Finally, we're getting to some new stuff.  We want to draw the cat right in the middle of the screen.  This takes a bit of math.  To get the middle of the screen, we need to take the canvas width and split it in half:

canvas.width / 2

and do the same thing with height:

canvas.height / 2

But that's not enough.  When we draw an iamge, the position we give is the top left corner of the image.  So to draw it right in the middle of the screen, we need to take away half of its width and height as well.

(canvas.width - image.width) / 2
(canvas.height - image.height) / 2

Now we'll put it all together in a new function.  Put this function above `function setup() {`.

```
function getMiddle(image) {
    return {
        x: (canvas.width - image.width) / 2,
        y: (canvas.height - image.height) / 2
    };
}
```

Now, when we call getMiddle, it will return an object that has an x and a y to put the cat right in the middle of the screen.

Down where you draw the cat, find this line:

```
        context.drawImage(cat.image, 0, 0);
```

Delete it and put these two lines in place:

```
        const middle = getMiddle(cat.image);
        context.drawImage(cat.image, middle.x, middle.y);
```

See the difference?  Instead of putting the cat at 0, 0, we're putting it at middle.x, middle.y.  If you reload the page, it should be in the middle of the screen.

## Bonus: Filling in the background

Now we want to put our cat on a background, so that it isn't just sitting in the middle of a blank screen.

In the gameLoop function, just below the line that says `context.clearRect(0, 0, canvas.width, canvas.height);`, add this function call:

```
    drawBackground();
```

Now, above the gameLoop function, enter this:

```

function drawBackground() {
	const GROUND_OFFSET = 8;
    const groundY = canvas.height / 2 + GROUND_OFFSET;
    context.fillStyle = 'CornFlowerBlue';
    context.fillRect(0, 0, canvas.width, groundY);
    context.fillStyle = 'green';
    context.fillRect(0, groundY, canvas.width, canvas.height - groundY);
}
```

Refresh the page, and you will see your cat on a green field under a blue sky.

There is a bit of math that is meant to work out where to draw the rectangles.  Then we set color (CornFlowerBlue for the sky, green for the ground) and fill in rectangles with those colors.  Look at the numbers in the `fillRect` lines.  They both go from the top left all the way across the page (from 0 to canvas.width).  The first one goes down to "groundY", which is where the ground is.  The second one starts there, and goes down to the bottom of the canvas - its height is canvas.height - groundY.  That's a lot of math, but think about it.  Draw it out on a piece of paper, and label all the parts, if you like.
