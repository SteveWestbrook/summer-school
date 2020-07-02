# LESSON 1 - Using Your Computer

The computer you are using for this course is a Raspberry Pi Model 4b running the Debian Linux operating system (OS).  You will find variants of this operating system on many comptuers.

The first lesson will teach you a few commands that will be helpful in using your computer.

## Using a terminal
A terminal is a program that allows you to type commands into your computer.  You may already be familiar with it.  You can see an icon near the top left corner of your screen - it is black and blue, and has symbols like this: `>_` in it.  Click once on this, and it will open a terminal for you.  Click the ^ button at the top right of the new window that has opened, and the terminal will take up the whole screen.  Switch back to your web browser, where you are reading these instructions, by holding down Alt and pressing Tab.  This is the fastest way to switch between programs, so give it a few practice tries until you are comfortable with it.

Much of the work you do will be in the terminal.

The first thing you will want to do is install a program called "pinta."  This is basically the same as Paint.  Here is how you can do it: type this into your terminal:

`sudo apt install pinta`

Now press enter.  A bunch of text will appear on your screen, and then it will ask you if you want to install.  Press "y" and it will go ahead and install the program.

You'll want to install software this way in the future, so let's learn about the commands you just entered and what they mean.

`sudo`

Some things, like installing software, can't be done by just anyone.  That's because you could ruin someone else's computer by installing the wrong software on it.  The word `sudo` is like "Simon Says" - The computer will do the installation instead of failing, and it will make sure you're allowed to do it before continuing.

`apt`

This calls apt, which is a program called a "package manager."  This program goes out and gets a list of other programs that you might want to install.  It can also remove packages if you want.  For example, if you wanted to remove pinta, you would type 

`sudo apt remove pinta`

But don't type that.

`install pinta`

Hopefully this is obvious by now - it installs pinta.

Once the program has installed, see if it worked - type

`pinta`

and press Enter.  Pinta should open up, and you should see a window with a blank canvas and some colour selectors in it.  Close that for now - we'll use it later.

## More advanced installation

You're about to find out why it's nice to have a package manager, because we also need to install some software that isn't available in the package manager, and as you'll see, it takes more effort.  We're going to install VSCode, which helps with writing computer programs.  It doesn't have very many features, but it's free and easy to learn.

The first thing you'll want to do is add it to your repository.  That will take a very long line:

`wget https://packagecloud.io/headmelted/codebuilds/gpgkey -O - | sudo apt-key add -'

That takes too long to type.  So copy it from the browser.  You can do that like this:

1. Use your mouse to select the line.  Make sure you select only the text in that one line, and nothing else.
2. Hold down Ctrl (bottom left of keyboard) and then press C (C stands for "copy").
3. Switch to the terminal with Alt-Tab.
4. Hold down Ctrl and Shift at the same time, and then press P (P stands for "paste").  When you're copying and pasting in the terminal, you use Ctrl-Shift-C and Ctrl-Shift-P.  Everywhere else, it's Ctrl-C and Ctrl-P.  Be careful - in a terminal, Ctrl-C means "Stop Program," and it will shut down whatever program is running there!
5. Once you have pasted in the command, press Enter.  It will run pretty fast.

The command above - the one you just pasted - first gets a special key - that's the thing starting at `wget` and going all the way up to the `|` symbol.  Then it "pipes" that key, using the pipe | character, to the next command - `sudo apt-key add -`.  That command adds the special key piped to it to a special list, which means you'll be allowed to install it.

Now you'll do the actual installation:

`curl -L https://raw.githubusercontent.com/headmelted/codebuilds/master/docs/installers/apt.sh | sudo bash`

You should practice your copy-pasting with this one as well.

`curl` is another program to get a file from the internet, and `sudo bash` will run the program.  Often enough, it is very dangerous and stupid to run programs you have downloaded from the internet, but in this case we'll take the risk.  In future, be very careful about what you download and run.

Just like we did with pinta, we want to make sure the program installed correctly.  Once it has run, press the button at the very top right of the screen.  A menu should pop up, and the first item on it should be called "Programming."  Hover over that with your mouse, and you should see a long list of all sorts of things.  One of them should say "Code - OSS (headmelted)."  That is the program you just installed.  Click it and it will run.  You'll need that open for our next lesson!
