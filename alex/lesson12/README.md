## LESSON 12 - HILLS

Now that we have the idea of a Cat separated from the idea of a Sprite in general, it's easy-ish for us to add some hills for our cat to jump over.  At first we won't make anything happen when we hit a hill - we'll just randomly throw hills onto the screen.

The first thing we want to do is make a Hill type, and just like the Cat type, it's a Sprite.

```
function Hill() {

}

Hill.prototype = new Sprite;
```

We also want to set up some basic stuff for it.  Change the hill so it looks like this:

```
function Hill() {
    Sprite.call(this, './hill1.png', 1);

    this.initialize = function() {
    }

    this.update = function() {
    }
}
```

You might have to change the name of the file you pass in - mine is "hill1.png" but maybe yours is different.

We'll make more changes to the Hill, but for now we'll come up with a way of adding new hills to the scene every once in a while.

## Adding and removing hills

Let's make a place for us to keep track of all our hills.  Way up at the very top of the file, you will see code like this:

```
var cat;
var canvas;
var context;
```

Add this line underneath those ones:

```
var hills = [];
```

That makes an "array" - a list of hills.  For now there are no hills in it.  We're going to make a way of having hills randomly appear.

Find the setup function.  It should look like this:

```
function setup() {
    setInterval(gameLoop, 25);
```

Right under that code, add this:

```
	setTimeout(addHill, 5000);
```

This will call an "addHill" function (which we're about to write) 5000 milliseconds (which is 5 seconds) after the setup function is run.

Now let's write the addHill function.  Put this under the END of the setup function.  You know how to find that - it's after the funtion's `}`.

The addHill function is pretty short:

```
function addHill() {
    hills.push(new Hill());
    var newTimeout = 500 + Math.random() * 2000;
    setTimeout(addHill, newTimeout);
}
```

What does this do?  The first line does two things at once - makes a new Hill object with `new Hill()`, and adds it to the hills array with `hills.push`.

The next line does some calculation.  Long story short, it finds a random timeout between half a second and 2.5 seconds.  That's how long the game will wait before adding a new hill.

Finally, we have a familiar line - we set the timeout before adding another new hill.

So what this will do is keep adding hills to the game.  We'll take old ones out later.

Now we're adding hills, but we also have to draw them.  Find the gameLoop function.  You'll want to add this new code inside the function, at the very end.

```
    for (var i = 0; i < hills.length; i++) {
        hills[i].draw();
    }
```

This is a `loop`.  It goes through all the hills in the hills array, and draws each one.  But right now, it doesn't know WHERE to draw them.  So let's do that next.  We're going to start the hill off on the right-hand side of the screen, and then we'll have it move to the left so our cat can jump over it.

Find the Hill object's `initialize` function.  We're going to want to put an initial position in it.  We'll find the middle, so that we know where the "ground" is, and then put in the middle vertically, and on the right-hand side horizontally.

```
        const middle = getMiddle(this.image);
        this.position = { x: canvas.width, y: middle.y };
```

Now we'll have the hill roll past using the update function.  We'll also want to remove the hill once it goes past the left-hand side of the screen.

```
        this.position.x -= 5;
        if (this.position.x < -this.image.width) {
            hills.shift();
        }
```

The first bit sets up the movement of the hill.  The second bit - the `if` statement - checks to see if the hill has gone past the edge.  If it has, it removes it using `hills.shift()`.  The `shift` function just removes the first hill in the array, which is always the one furthest to the left.

Reload your page and you should be able to see the hills coming by.  Try to jump over them!

## Tweaking our numbers
If you play the game a little, you'll find that the cat's jumps aren't really right for the hills.  Sometimes it's impossible to miss the hill.  That can be fixed easily by tweaking the jump.  We'll make it faster, and make it complete in less time.  Find this: `this.upwardSpeed = 2.0;` and change it so it says 4.0 instead of 2.0.  Also find this: `this.upwardSpeed -= 0.1;` and change it so that it says 0.4 instead of 0.1.  Try again; that might do it.

## Next time on "Making your game"
You'll notice that you don't actually die when you run into a hill.  We'll set that up next, and make it so you can end and restart the game.  It'll probably take a couple of lessons, but we're getting close to being done!
