
# Programming Exercises

We want to practice what we have learned so far. 

Work in the Rstudio editor and write a script that also serves as documentation. Try to write clean code (readable and as simple as possible):

* use consistent variable names (e.g. PropBlond or Prop_Blond) 
* indent your code
* write functions

***

Before starting let's install the `ggplot2` package:


```r
install.packages("ggplot2")
```

Load the `ggplot2` package as we will use some of its data: 


```r
library(ggplot2)
```

```
## Loading required package: methods
```


***

# Data Set 1: Sleep in mammals

The msleep data set is part of the `ggplot2` package. It contains a mammals sleep dataset (see ?msleep for details).

First let's first look at the structure of the dataset:


```r
str(msleep)
```

```
## 'data.frame':	83 obs. of  11 variables:
##  $ name        : chr  "Cheetah" "Owl monkey" "Mountain beaver" "Greater short-tailed shrew" ...
##  $ genus       : chr  "Acinonyx" "Aotus" "Aplodontia" "Blarina" ...
##  $ vore        : Factor w/ 4 levels "carni","herbi",..: 1 4 2 4 2 2 1 NA 1 2 ...
##  $ order       : chr  "Carnivora" "Primates" "Rodentia" "Soricomorpha" ...
##  $ conservation: Factor w/ 7 levels "","cd","domesticated",..: 5 NA 6 5 3 NA 7 NA 3 5 ...
##  $ sleep_total : num  12.1 17 14.4 14.9 4 14.4 8.7 7 10.1 3 ...
##  $ sleep_rem   : num  NA 1.8 2.4 2.3 0.7 2.2 1.4 NA 2.9 NA ...
##  $ sleep_cycle : num  NA NA NA 0.133 0.667 ...
##  $ awake       : num  11.9 7 9.6 9.1 20 9.6 15.3 17 13.9 21 ...
##  $ brainwt     : num  NA 0.0155 NA 0.00029 0.423 NA NA NA 0.07 0.0982 ...
##  $ bodywt      : num  50 0.48 1.35 0.019 600 ...
```


### 1. Which mammal sleeps the least, the most?

### 2. Is there a association between total sleep duration and body weight (bodywt)?  

### 3. Make a scatterplot of sleep_total vs. sleep_rem

### 4. Make point size proportional to log(body mass)

### 5. Add a OLS (Ordinary least square) regression line

### 6. Color-code the points according to vore. Does the scaling of REM & total sleep differ with diet?

### (advanced) 7. Make the figure from the question 6 in publication quality (Axes labels, font sizes, ..)

Original publication in [PNAS](http://www.pnas.org/content/104/3/1051.abstract)

****

## Data Set 2: Baby names

(Data set 1 is borrowed from a [lecture](http://stat405.had.co.nz/lectures/11-adv-data-manip.pdf) by Hadley Wickham)

The data set contains the top 1000 male and female baby names in the US, from
1880 to 2008 (1000* 2 * 129 = 258,000 records). All names with more than 5 uses
are given.

It contains 5 variables: year, name, soundex, sex and proportion

Download bnames2.csv.bz2 from http://stat405.had.co.nz/data/bnames2.csv.bz2
(Under Windows download the zipped file [bnames2.csv.zip](https://www.dropbox.com/s/hax6jullt8a9kd7/bnames2.csv.zip?dl=0) and extract it before reading)

You can directly read in the compressed file like (on Linux and Mac OS)

```r
bnames <- read.csv("bnames2.csv.bz2")
```

Also load a file containing the total number of birth per years (for boys and girls separately)

```r
births <- read.csv("http://stat405.had.co.nz/data/births.csv")
```


Now it's your turn.
### 1. Extract your name from the dataset. Plot the trend over time.

### 2. Use the soundex variable to extract all names that sound like yours. Plot the trend over time.

### 3. Find out the most frequently used similar sounding name

### (advanced) 4. Which boy and girl name was used most over the whole time? 

### (advanced) 5. Did first names became shorter over time? 

### (advanced) 6. Which names became very rare after 1944? 

### (advanced) 7. Think of another question you could answer with the dataset. E.g. Identify the most popular firstname in 1980ies the or identify the most popular name that was used for boys and girls.

***

## Data Set 3: Hair and Eye Color

The next data set is the distribution of hair and eye color and sex in 592 statistics students stored in the table `HairEyeColor` (see ?HairEyeColor for details).

We load the data set with the data() function and have a look at the structure using str().


```r
data("HairEyeColor")
str(HairEyeColor)
```

```
##  table [1:4, 1:4, 1:2] 32 53 10 3 11 50 10 30 10 25 ...
##  - attr(*, "dimnames")=List of 3
##   ..$ Hair: chr [1:4] "Black" "Brown" "Red" "Blond"
##   ..$ Eye : chr [1:4] "Brown" "Blue" "Hazel" "Green"
##   ..$ Sex : chr [1:2] "Male" "Female"
```

Now it's your turn.

### 1. What class of data is HairEyeColor?

### 2. Visualize the data
Use the mosaicplot() function to plot categorical data

### 3. Look at the mosaicplot() help
The most important parts are at the top and bottom. Try to understand what similar functions are available (<See Also>). Run the mosaicplot() examples.
With a new function I often just look at the examples or run them. Its often faster to understand what it does than reading the whole help entry.

`example(mosaicplot)` runs the examples of any function

***

# Data Set 4: Movie ratings

The movies data set is from the `ggplot2` package. The internet movie database,
[http://imdb.com/](http://imdb.com/), is a website devoted to collecting movie
data supplied by studios and fans (See ?movies for details). 

The data set contains data for 58'788 movies, namely the title of the movie,
year of release, budget, length, rating and genre.

### 1. Look at the structure of `movies` using function str() or head(). Make a histogram of the rating.

### 2. Do old movies perform better or worse than recent movies?

Some movies obtained less than 10 votes. Remove them and repeat the plotting. Do you see a change? 

### 3. Does the movie genre influence the rating? 

Add a new variable Genre.simple containing genre information like this:
movies$Genre.simple <- ifelse(movies$Action == 1, "Action", ifelse(movies$Comedy == 1, "Comedy", ifelse(movies$Drama == 1, "Drama", "other")))
Then plot the rating per genre

By default genres are alphabetically ordered. Let's order the genres according to their median rating (tip: use factors and function factor()). 

### 4. Which movie is the longest and how long is it?

### 5. Does the movie length have an impact on its rating?
Tip: use the function cut to make categories.


