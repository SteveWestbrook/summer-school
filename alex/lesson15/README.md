## LESSON 15 - Scoring

We'll want to add a score to our game now, so we can see how well we're doing.  So let's do that!  Start by adding a new "score" variable up with all the other `var`s:

```
var score = 0;
```

As you can see, this one is set to 0 when we start.  That way our system knows it's a number.

We should increase our score every time we have jumped over a hill.  Since we know exactly where our cat is, we don't really need to calculate that; we just need to check to see if a hill has passed the middle mark.  We will do this in the `update` function of the `Hill` object.  First, find this line inside the update function:

```
        this.position.x -= 5;
```

You'll want to add the next few lines under this one.

First we want to know where the middle of the screen is:

```
        const middleX = (canvas.width - this.image.width) / 2;
```

Now that we have found this, we want to check it against the hill's position.  We also want to make sure the hill hasn't already been scored so that we don't give the player points more than once for the same hill:

```
        if (middleX > this.position.x && !this.scored) {
            this.scored = true;
            score += 10;
        }
```

Once you've done this, points will start adding up when you jump over a hill.  But we also want to display those points.  Let's go to the bottom of the file and add a new function:

```
function printScore() {
    context.fillStyle = '#000';
    context.font = '14px Arial';

    var text = "Score: " + score;
	var textSize = context.measureText(text);
    context.fillText(text, canvas.width - textSize.width - 5, textSize.actualBoundingBoxAscent + 5);
}
```

This figures out where to put the score, and then writes it in the top right corner.  But we still have to call the function:

Find the `gameLoop` function, and then find where it draws the background, which looks like this:

```
drawBackground();
```

Underneath that line, write the call to printScore:

```
printScore();
```

That should work.  Refresh the page and you will see your score go up when you jump over a hill.
