# LESSON 6 - Loading the cat and showing it.

## Clear out your file

We're going to do our programming in JavaScript, so open your JavaScript file, which should be called game.js.  First thing, delete this line:

`alert('hello there');`

if you haven't already.

Next, we want to put all of our setup code in a function called... setup!  A function is a block of code that you can run whenever you want.  We'll want to run it on setup.  To make that function, write this:

```
function setup() {
}
```

## Load the cat
First things first.  We want a picture of a cat!  We'll be adding code to two places, so pay super close attention to where things go.

First, we want to add a "variable."  A variable is a special word that is kind of like a name.  If I say, "Hey Alex," you know I'm talking to you.  So if we say "Hey Cat," we know we're talking to the cat.  So how do we do that?  Like this:

BEFORE the `function setup` part, add this line:

`var cat;`

That just tells the computer we have a variable (a "var"), and that we are naming it cat.  The `;` at the end tells the computer we're done.  It's like a period at the end of a sentence.

Now, RIGHT UNDER the `function setup` line, we'll tell the computer what `cat` is.  Write these two lines:

```
cat = new Image();
cat.src = './cat.png';
```

The first line tells us that `cat` is an image, that is, a picture.  The second line gives a "source" (src) for the image - the cat picture you saved in the last lesson.  In that src, you see './' - that just means that the file is in the same directory.  And of course cat.png is the picture itself.

Now your code should look like this:

```
var cat;

function setup() {
    cat = new Image();
    cat.src = './cat.png';
}
```

## Done right?

Wrong!  We loaded the image, but that's it.  Now we have to show it on the canvas.
First thing, we want to get the canvas.  First, under where you declared cat, i.e. the line `var cat;`, put these two lines:

```
var canvas;
var context;
```

Under the line `cat.src = './cat.png';`, write these lines:

```
var elements = document.getElementsByTagName('canvas');
canvas = elements[0];
context = canvas.getContext('2d');
```

This gives you a new variable, called canvas.  First we get elements with the tag name `<canvas>` - remember that those are called tags in HTML - and then we pick the first one.  That's what `elements[0]` means - it's getting the first "element" in a list.  `elements[1]` would get the second one, `elements[2]` would get the third one, and so on.

What's the context?  This is a bit weird.  A "context" is where you draw things on the canvas.  I know, it's weird.  This one is '2d' because we're drawing a 2d thing, and not a 3d thing.

So now we have a canvas, a context, and an image.  Let's put them together!

Under the line `context = canvas.getContext('2d');`, add these lines:

```
cat.onload = function () {
	context.drawImage(cat, 0, 0);
}
```

cat.onload is a special "function" that gets called when the image of the cat has finished loading - it can take a little while over the internet.  Once you have it, it called the function that you just set.  That calls the one line that actually draws your cat: `context.drawImage(cat, 0, 0);`.

Your whole code file should look like this now:

```
var cat;
var canvas;
var context;

function setup() {
    cat = new Image();
    cat.src = './cat.png';

    const elements = document.getElementsByTagName('canvas');
    canvas = elements[0];
    context = canvas.getContext('2d');

    cat.onload = function() {
        context.drawImage(cat, 0, 0);
    }
}
```

## Just one more thing to do
You are almost ready to see the cat.  Open up index.html, and call the setup function when the body loads.  But how?  Like this.  Find this line:

```
<body>
```

And change it so it says this:
```
<body onload="setup()">
```

Now run the server.  Remember the line with `python` and `8000` in it?  That one.  Try to remember it each time you type it in, so you don't have to go back and look it up!

Finally, go to localhost:8000 in a browser, and you should see your cat!
