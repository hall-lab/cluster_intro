# Plotting a histogram with R on the cluster

The Rscript below will generate a histogram from an input file containing a column of numbers.

```
#!/usr/bin/env Rscript
# print usage
usage <- function() {
  cat(
    'usage: histogram.R <file>
    
    histogram.R
    description: Plot a histogram from a column of numbers
    
    positional arguments:
    file               File of numerical values, one per line.
    ')
}
# Draw a histogram from a text file
args <- commandArgs(trailingOnly=TRUE)
file <- args[1]
filename <- basename(args[1])

# Check input args
if (is.na(file)) {
  usage()
  quit(save='no', status=1)
}

x <- as.numeric(scan(file))
pdf(paste0(filename, '.pdf'), height=4, width=5)
par(c(4,4,4,4))
hist(x, col='steelblue3', main='', breaks=100, xlim=c(0,6))
dev.off()
```

To run the above script on the cluster, save the code above in a document titled "histogram.R" and submit a job to the cluster by typing the following command:
```bash
bsub -q research-hpc -M 1000000 -R "rusage[mem=1000] select[mem>1000]" -oo %J.log -a "docker(registry.gsc.wustl.edu/genome/genome_perl_environment)" "Rscript histogram.R input.txt"
```
This will generate a file called "input.pdf" that contains a histogram plot of the data contained in input.txt.
### Note that this is a very simple R script that does not require any additional libraries, therefore the copy of R available in genome_perl_environment Docker container is sufficient. For more complex R scripts, you may want to look into the Docker containers found here: https://github.com/hall-lab/docker-toolbox or build your own.

