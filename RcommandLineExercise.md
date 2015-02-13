## R from Command Line

This exercise is a shortened and modified version of this
[Software Carpentry page](http://software-carpentry.org/v5/novice/r/06-cmdline.html).
\
\


The R Console and other interactive tools like RStudio are great for prototyping code and exploring data, but sooner or later we will want to use our program in a pipeline or run it in a shell script to process thousands of data files.

### A very simple R Script

Using the text editor of your choice, save the following line of code in a text file called `session-info.R`:


```r
sessionInfo()
```

Run the script using

```
Rscript session-info.R
```


```
## R version 3.0.3 (2014-03-06)
## Platform: x86_64-apple-darwin10.8.0 (64-bit)
## 
## locale:
## [1] de_CH.UTF-8/de_CH.UTF-8/de_CH.UTF-8/C/de_CH.UTF-8/de_CH.UTF-8
## 
## attached base packages:
## [1] stats     graphics  grDevices utils     datasets  methods   base     
## 
## loaded via a namespace (and not attached):
## [1] digest_0.6.3     evaluate_0.5.5   formatR_1.0      htmltools_0.2.6 
## [5] knitr_1.7        rmarkdown_0.2.68 stringr_0.6.2    tools_3.0.3     
## [9] yaml_2.1.13
```


### Allowing arguments

Now let's create another script that does something more interesting. Write the following lines in a file named `print-args.R`:


```r
args <- commandArgs()
cat(args, sep = "\n")
```

Then run `print-args.R` from the shell:

```
Rscript print-args.R first second third
```


```r
args <- commandArgs()
cat(args, sep = "\n")
```

```
## /Library/Frameworks/R.framework/Resources/bin/exec/R
## --slave
## -e
## rmarkdown::render('RcommandLineExercise.Rmd',~+~~+~encoding~+~=~+~'');
```

commandArgs() adds each of those arguments to the vector it returns. Since the first elements of the vector are always the same, we can tell commandArgs to only return the arguments that come after `--args`. Let's update `print-args.R` and save it as `print-args-trailing.R`:


```r
args <- commandArgs(trailingOnly = TRUE)
cat(args, sep = "\n")
```

And then run print-args-trailing from the shell:
```
Rscript print-args-trailing.R first second third
```



\
\


**Tip** `Rscript print-args.R arg1 arg2` is more convenient but the same as `R --slave --no-restore -f print-args.R --args arg1 arg2` which is what is run internally.  

- `--slave:`:`Make R run as quietly as possible`
- `--no-restore`: For reproducible code we should not restore previously saved objects. The script(s) should start from scratch and create all objects necessary for the analysis (or save intermediate objects using save() and load()).

\
\


### Now a more useful script

Write the following code in a file called `readings.R`. It always prints the per-patient (per-row) mean of a single data file.
 

```r
main <- function() {
  args <- commandArgs(trailingOnly = TRUE)
  filename <- args[1]
  dat <- read.csv(file = filename, header = FALSE)
  mean_per_patient <- apply(dat, 1, mean)
  cat(mean_per_patient, sep = "\n")
}

main()
```

Next download the input file `inflammation-01.csv`


```r
wget https://raw.githubusercontent.com/swcarpentry/python-novice-inflammation/gh-pages/data/inflammation-01.csv
```

Now we have everything to run it

```
Rscript readings.R inflammation-01.csv
```


### Handling Command-Line Flags

We would like a program which can calculates different options of summary statistics.
`--min`, `--mean`, or --max flag to determine what statistic to print.


### Key Points

- Use commandArgs(trailingOnly = TRUE) to obtain a vector of the command-line arguments that a program was run with.
- Use cat(vec, sep = "\n") to write the elements of vec to standard output, one per line.
- If you use many arguments, have a look at [argparse](http://cran.r-project.org/web/packages/argparse/index.html)

### Advanced examples

Rscript can also handle multiple files and read standard input (for using in a pipe). See 
this Software Carpentry [page](http://software-carpentry.org/v5/novice/r/06-cmdline.html).

- Use readLines(con = file("stdin")) to read a program's standard input.
