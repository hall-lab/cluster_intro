# Example of a project layout

Neil is one of our CS experts in lab and he contributed some tips about how to keep your code and working environment tidy and organized, and here's an example of his direcotry layout when he started a new project:
( Feel free to adjust it/ make your own!)

<img src="https://github.com/hall-lab/cluster_intro/blob/master/projec_layout_exp.png" width="470" height="525" />

And he explained the duty of each directory as:
* the bin directory is for scripts
* the data directory is for data (the “external” subdirectory is for data received by outside collaborators, website, etc.;  the “derived” directory is for data generate by code created in this project)
* the logs directory are generally the output generated by scripts (i usually run scripts like bin/1-awesome-script 2>&1 | tee logs 1-awesome-script.log
* the src directory is for any custom python, R, (or whatever) code that i might call as a library
* the vendor directory is for taking care of the virtualenv / R library directories for the current project, like which version of ggplot, matplotlib, pandas, etc.  



