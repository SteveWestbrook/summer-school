## LESSON 13 - GAME OVER

We're going to have to do a little tweaking to make sure our cat runs into hills in the right way.  Once we've done that we can make our cat game come to an end.

### Are we bumping into a hill?

The first thing we're going to do is check every hill to see if it's running into our cat.  Let's make a function that checks whether the cat runs into the hill.  It's only one line long, but it's a really long line.  Put the function right at the bottom of the whole file.

```
function isOverlapping(cat, hill) {
    return cat.position.x < hill.position.x + hill.image.width &&
        cat.position.x + cat.image.width > hill.position.x &&
        cat.position.y < hill.position.y + hill.image.height &&
        cat.position.y + cat.image.height > hill.position.y;
}
```

Now we want to call this function, and if it tells us we're running into a hill, declare game over.

Find this code inside the gameLoop function:

```
    for (var i = 0; i < hills.length; i++) {
        hills[i].draw();
    }
```

You will want to add a call to the isOverlapping function that we just wrote, so that the whole thing looks like this:

```
    for (var i = 0; i < hills.length; i++) {
        hills[i].draw();
		if (isOverlapping(cat, hills[i])) {
            gameOver();
            return;
        }
    }
```

We haven't written the gameOver function yet, so this won't work.  We have to do a little setup before we're ready for that.

First thing, we're going to keep track of the timer that keeps the gameLoop function running.  Go to the top of the file, where you declare `var cat` and all the other vars.  In that section, add a couple of new lines:

```
var loopInterval;
var hillTimer;
```

That tells the computer that we want to track a variable named "loopInterval."

Now we're going to use it.  At the beginning of the setup function, you'll see two lines like this:

```
    setInterval(gameLoop, 25);
    setTimeout(addHill, 5000);
```

Change them to this:

```
    loopInterval = setInterval(gameLoop, 25);
    hillTimer = setTimeout(addHill, 5000);
```

Now we're ready to write the gameOver function.  Go to the very bottom of the file one more time, and write this function:

```
function gameOver() {
    // Stop the game from running
    clearInterval(loopInterval);
    clearTimeout(hillTimer);

    // Get rid of hills
    hills = [];

    // Get rid of cat
    cat = null;

    // Tell the player the game is over
    context.fillStyle = "#880000";
    context.font = '24px Arial';

    var text = "GAME OVER";
    var textWidth = context.measureText(text).width;
    var middle = getMiddle({ width: textWidth, height: 24 });
    context.fillText(text, middle.x, middle.y);
}
```

This does a bunch of stuff - it stops the game from running, it clears out the cat and the hills, and it prints "GAME OVER" in the middle of the screen.

If you have gotten this far, congratulations!  The game kinda sorta works!
