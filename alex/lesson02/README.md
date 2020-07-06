# LESSON 2 - Writing some code

Make sure VS Code and a terminal are open, as well as your web browser.

## Continuing from last time
Review where you were at the end of the last lesson - you should have a terminal open, and you should navigate to the directory `~programming/cats`.

## Writing a new web page
Go to VS Code using Alt-Tab.  

In VS Code, navigate to the same directory (`~/programming/cats`) with

File > Open Folder

Select the folder first by clicking "Home" on the left-hand side, then going to programming, and then to cats.  Finally, hit the "OK" button at the bottom of the window.

Now on the left-hand side, you should see "practice" under a couple of other headings.  Beside "practice" there are some icons - hover over the first one and it should say "New File."  Press it, and name your file `index.html`.  Double click the file if it hasn't opened already.  Then in the file, write this:

```
<html>
</html>
```

You'll notice that the second part - `</html>` - gets put in automatically.  This is the code editor helping you out.

So what have you just written?  Well, you've told the computer you want an "HTML" page - that is, a web page.  The first part, `<html>`, tells the computer that the page is beginning, and the end part with the `/` in it tells the computer that the page is ending.  Everything in your page will go between these two "tags".

Now go and put in a couple of new tags as shown below, inside the html "block".  The whole document will look like this:

```
<html>
    <head>

    </head>
    <body>

    </body>
</html>
```

Here are the "head" and "body".  The head holds things that the user won't see, but that your webpage might need.  More on that later.  The body holds everything that the user sees.  But right now it's empty!  Add a "paragraph" tag, so that you will be able to see something:

```
        <p>Hello world!</p>
```

Now, if you have done everything right, the whole page should look like this:

```
<html>
    <head>

    </head>
    <body>
        <p>Hello world!</p>
    </body>
</html>
```

Save your work with Ctrl-S.

## Checking your work
You can see if what you did is right by running your webpage.  This takes a few steps, but don't worry; it's pretty simple.

First, go to your terminal.  Make sure you're in the ~/programming/cats directory, and make sure you see index.html:

`ls`

should output

`index.html`

Now make the web page available:

`python -m SimpleHTTPServer 8000`

Finally, open a browser window (Go to the web browser if you have one open, and press Ctrl-N; if you don't have one open, click the "world" icon at the top left of your screen).

In the address bar of the browser - the text box at the top - type this:

`localhost:8000`

and hit Enter.  If everything worked, you should see your web page, which says "Hello World."

