# Change back to previous directory

To quickly move to the last directory you were working in, type:
```bash
cd -
```

# Quickly search matching commands in your bash history

To quickly search through your bash history using the up and down arrows, add the following to your ~/.inputrc file. Log out and log back in after editing this file to initate the changes.
```bash
"\e[A": history-search-backward
"\e[B": history-search-forward
```
This will allow you to search through everything in your history that matches whatever you have already typed into the command line. For example, if you type "cd" and press the up arrow, you will search through everythign in your bash history that starts with "cd". This is similar to using "ctrl-r" but the search is anchored to the beginning of the line you have typed.

# Fuzzy cuteness

If you need a smile, join the #pets page on the Hall lab slack. Enjoy cute pictures of your lab-mate's pets and share pictures of your own.
