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

# Visualizing tab-delimited data

It can often be difficult to properly visualize tab-delimited data when the fields have variable length. An easy solution to this is to use `column -t`. For example:
![Column Example](ColumnExample.png?raw=true "Column Example")

# Monitoring jobs

To watch jobs over a period of time without having to constantly type `bjobs`, `watch` can be used. For example, to watch all of your currently running jobs (refreshing once every second):
```
watch -n 1 bjobs
```
Any options can be added to `bjobs` while using `watch`. For example, to watch all jobs on the `research-hpc` queue:
```
watch -n 1 bjobs -q ccdg
```
To exit `watch`, press CTRL-C

# Free GitHub pro for students

Students can get free unlimited public and private GitHub repositories. Sign up for the GitHub Student Developer Pack here: https://education.github.com/pack

# Discounted Spotify, Hulu, and Showtime for students

Students can get Spotify premium for $4.99 a month. This also gives you access to Hulu's basic ad-supported plan and a Showtime account. Sign-up details can be found here: https://support.spotify.com/us/account_payment_help/premium_for_students/student-discount/

# Fuzzy cuteness

If you need a smile, join the #pets page on the Hall lab slack. Enjoy cute pictures of your lab-mate's pets and share pictures of your own. Pet pictures/videos from the internet are also welcome!

# Quick reference cheat sheets

* **R**: cookbook for R - http://www.cookbook-r.com
* **SED**: useful one-line script - http://sed.sourceforge.net/sed1line.txt
* **ggplot2**: powerful R plotting package - https://www.rstudio.com/wp-content/uploads/2015/03/ggplot2-cheatsheet.pdf
* Create a personal cheat sheet of your own frequently used commands! 

# Directory and script organization

Here are some tips for organizing your projects:
* Separate scripts and data into different directories
* Version control 
  - Github 
  - Add info when naming script (like a date suffix)
  - Add information inside the script
* Name the scripts by the order of execution, e.g.: 0-preprocess_data.sh, 1-quality_control.sh, etc.

