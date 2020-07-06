# Starting with JavaScript

## Adding a new JavaScript (JS) file
Just as you added index.html a little while ago, you'll want to add a new file, called `game.js`.  If you can't remember how to do that, go back to the other lesson and go through the steps again.

Once you have the new file, write the following in it:

```
alert('Hi there');
```

This is going to pop up a little message, so that we know the file is loaded.

But how to load it?  Go back to `index.html`.  You'll notice that you now have a couple of tabs open in VS Code - one for index.html, and one for game.js.  You can switch between them with Ctrl-Tab, or by clicking on the tabs themselves.

Now, in `index.html`, add the script right under the `<head>` tag, like this:

```
        <script src="game.js"></script>
```

Now, save both documents.  You can switch to each one and press Ctrl-S, or you can use File > Save All.

Switch to the browser, and reload the page.  If the script loaded, it should show you a popup that says "Hi there" when you load the page.



