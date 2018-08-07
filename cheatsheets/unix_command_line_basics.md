# UNIX Basics | Navigate and create files efficiently

c. 1 hour

## UNIX – what is it?
- "in the beginning was... the command prompt"

![Unix Family Tree](http://www.computerworld.com/common/images/site/features/2009/062009/unix_chart_775.jpg)

Before we had a GUI all we had in the command line interface. We will be using this frequently in the course as it will greatly speed up our development process.

## Navigating the command prompt

Use the TAB and up key in the command line to increase your speed while navigating the command line.

You can also increase speed by using aliases - added to the '.zshrc' file.

    alias working='cd ~/wdi_working'


`.` - Is the current directory
`..` - is the parent directory

`pwd` - present working directory
`ls` - list of items in current directory
`ls -a` - will list all items in the current directory including hidden files.
`ls -l` - Will give you a long list of item in the current directory including permissions, size and last modified date.
`cd <directory name>` - will move us into our specified directory. We can normally leave out cd in zsh.
`cd` - Without a specified directory this will take us to our home directory.
`history` - Will list your entire commands history (use `!line_number` to retrieve a specific command)
`grep` - Global regular expression parser - can be used with history to search - `history | grep <search item>`
`mkdir <directory name>` - Will create the specified directory.
`df -h` - display free disk space

## Managing files

`touch <filename>` - Will create the specified file
`mv` - Is used for both moving files and renaming them
`rm <filename>` - removes the specified file
`rm -rf <directory name>` - removes the specified directory (Use with caution, make sure you are in the right place. "-rf" stands for recursive forced, and you can imagine how bad the results could be if you did that in your home folder!)
`cp <file to be copied> <name to copy it to>` - Will copy first file to the name of the second file if specified

## Keyboard shortcuts

```
|keypress|action|
|--------|------|
|Ctrl + A|  Go to the beginning of the line you are currently typing on
|Ctrl + E|  Go to the end of the line you are currently typing on
|Ctrl + L|  Clears the Screen, similar to the clear command
|Ctrl + U|  Clears the line before the cursor position. If you are at the end of the line, clears the entire line.
|Ctrl + H|  Same as backspace
|Ctrl + R|  Let’s you search through previously used commands
|Ctrl + C|  Kill whatever you are running
|Ctrl + D|  Exit the current shell
|Ctrl + Z|  Puts whatever you are running into a suspended background process. fg restores it.
|Ctrl + W|  Delete the word before the cursor
|Ctrl + K|  Clear the line after the cursor
|Ctrl + T|  Swap the last two characters before the cursor
|Tab    |   Auto-complete files and folder names
```

