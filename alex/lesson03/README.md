#LESSON 3 - The Canvas and How To Use It

## What are we doing here?
We're trying to make a game that shows a cat jumping over hills, and shows you your score as you do it.  We're going to use a web page to hold this game, because that is actually one of the easiest ways to do it.  Most of what we do will not involve web programming, but there's a little more to do.

## Adding a "Canvas" to your page
The way that you can show moving pictures as in a game on a webpage is by way of an element called the "canvas."  You can add it to your page just like you would any other element:

```
<canvas>
</canvas>
```

While you're at it, delete the "Hello world" paragraph, so that your page looks like this:

```
<html>
    <head>

    </head>
    <body>
        <canvas>

        </canvas>
    </body>
</html>
```

Now your page will have nothing visible.  So let's make sure we can see where the canvas is, by giving it a border.  Change the "start tag" of the canvas, i.e. the first `<canvas>`, so that it says this:

```
        <canvas style="border: 1px solid black; width: 100%; height: 100%;">
```

That new style "attribute" is doing three things: it's giving the canvas a border (1 pixel, solid line, black color); it's making the canvas the same width as the whole page; and it's making the canvas the same height as the whole page too.

Now go back to the web browser that has your web page in it.  Hit F5 at the top of the keyboard to reload the page.  Does it still say "Hello world?"  If so, hit Ctrl-F5.  Once you have reloaded the page successfully, you should see a square that takes up the whole page.  Now, no matter how big or small your page, the canvas will always fit nicely inside it.

## So What?
Now we have a canvas, but how do we put things inside of it?  Well, HTML is ok for displaying things, but to make them move, we need something called JavaScript.  HTML just puts boxes and text on the screen; JavaScript is there to control movement, and to figure out what to do when the player presses a button.  The next lesson is therefore going to be about JavaScript.
