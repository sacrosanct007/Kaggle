---
title: "R_notes_datacamp"
output: 
  html_document: 
    keep_md: yes
---


***
***
***
***
*************
#Introduction to R
*************
***
***
***
***
***

**Basic data types in R**
- Numeric (eg:4.5), Integers (eg:4), Boolean(eg: FALSE), characters(eg:"a") 

check variable type in r: class(variable_name)

If you want to check out the contents of the workspace, you can type ls() in the console.

This will give you a quick overview of the contents of a variable:summary(my_var)

## Vectors
are one-dimension arrays that can hold numeric data, character data, or logical data.In R, you create a vector with the combine function c(). You place the vector elements separated by a comma between the parentheses. For example:

numeric_vector <- c(1, 2, 3)
character_vector <- c("a", "b", "c")

You can give a name to the elements of a vector with the names() function. Have a look at this example:
some_vector <- c("John Doe", "poker player")
names(some_vector) <- c("Name", "Profession")

**sum()**

It calculates the sum of all elements of a vector. For example, to calculate the total amount of money you have lost/won with poker you do:

total_poker <- sum(poker_vector)

To select the first element of the vector, you type poker_vector[1] and so on.

Suppose you want to select the first and the fifth day of the week: use the vector c(1, 5) between the square brackets. For example, the code below selects the first and fifth element of poker_vector:

poker_vector[c(1, 5)]
c(2, 3, 4) can be abbreviated to 2:4.

Just like you did in the previous exercise with numerics, you can also use the element names to select multiple elements, for example:

poker_vector[c("Monday","Tuesday")]


## matrix 
is a collection of elements of the same data type (numeric, character, or logical) arranged into a fixed number of rows and columns. Since you are only working with rows and columns, a matrix is called two-dimensional.

You can construct a matrix in R with the matrix() function. Consider the following example:

matrix(1:9, byrow = TRUE, nrow = 3)

Similar to vectors, you can add names for the rows and the columns of a matrix

rownames(my_matrix) <- row_names_vector
colnames(my_matrix) <- col_names_vector

 rowSums() conveniently calculates the totals for each row of a matrix. This function creates a new vector:

rowSums(my_matrix)

You can add a column or multiple columns to a matrix with the cbind() function, which merges matrices and/or vectors together by column. For example:

big_matrix <- cbind(matrix1, matrix2, vector1 ...)

## factor 
To create factors in R, you make use of the function factor(). First thing that you have to do is create a vector that contains all the observations that belong to a limited number of categories. For example, sex_vector contains the sex of 5 different individuals:

sex_vector <- c("Male","Female","Female","Male","Male")
It is clear that there are two categories, or in R-terms 'factor levels', at work here: "Male" and "Female".

The function factor() will encode the vector as a factor:

factor_sex_vector <- factor(sex_vector)

temperature_vector <- c("High", "Low", "High","Low", "Medium")
factor_temperature_vector <- factor(temperature_vector, order = TRUE, levels = c("Low", "Medium", "High"))

## Data frame

You construct a data frame with the data.frame() function. As arguments, you pass the vectors from before: they will become the different columns of your data frame. Because every column has the same length, the vectors you pass should also have the same length. But don't forget that it is possible (and likely) that they contain different types of data.

name <- c("Mercury", "Venus", "Earth", "Mars", "Jupiter", "Saturn", "Uranus", "Neptune")
type <- c("Terrestrial planet", "Terrestrial planet", "Terrestrial planet", 
          "Terrestrial planet", "Gas giant", "Gas giant", "Gas giant", "Gas giant")
diameter <- c(0.382, 0.949, 1, 0.532, 11.209, 9.449, 4.007, 3.883)


** Create a data frame from the vectors**
planets_df <-data.frame(name,type,diameter)


** Select planets with diameter < 1**
subset(planets_df,subset=diameter<1)

order() is a function that gives you the ranked position of each element when it is applied on a variable, such as a vector for example:

> a <- c(100, 10, 1000)
> order(a)
[1] 2 1 3


** Sorting the data frame**

Use order() to create positions
positions <-  order(planets_df$diameter)

Use positions to sort planets_df
planets_df[positions,]


## Lists

A list in R is similar to your to-do list at work or school: the different items on that list most likely differ in length, characteristic, and type of activity that has to be done.

A list in R allows you to gather a variety of objects under one name (that is, the name of the list) in an ordered way. These objects can be matrices, vectors, data frames, even other lists, etc. It is not even required that these objects are related to each other in any way.

You could say that a list is some kind super data type: you can store practically any piece of information in it!

Construct list with these different elements:
my_list <- list(my_vector,my_matrix,my_df)


**Selecting elements from a list**

One way to select a component is using the numbered position of that component. For example, to "grab" the first component of shining_list you type

shining_list[[1]]
A quick way to check this out is typing it in the console. Important to remember: to select elements from vectors, you use single square brackets: [ ]. Don't mix them up!

You can also refer to the names of the components, with [[ ]] or with the $ sign. Both will select the data frame representing the reviews:

shining_list[["reviews"]]
shining_list$reviews
Besides selecting components, you often need to select specific elements out of these components. For example, with shining_list[[2]][1] you select from the second component, actors (shining_list[[2]]), the first element ([1]). When you type this in the console, you will see the answer is Jack Nicholson.

To conveniently add elements to lists you can use the c() function, that you also used to build vectors:

ext_list <- c(my_list , my_val)
This will simply extend the original list, my_list, with the component my_val. This component gets appended to the end of the list. If you want to give the new list item a name, you just add the name as you did before:

ext_list <- c(my_list, my_name = my_val)

***
***
***
***
*************
#Intermediate R
*************
***
***
***
***
***


## The if statement

if (condition1) {
  expr1
} else if (condition2) {
  expr2
} else if (condition3) {
  expr3
} else {
  expr4
}

## while loop and break

while (speed > 30) {
  print(paste("Your speed is", speed))
  
  # Break the while loop when speed exceeds 80
  if ( speed>80) {
    break
  }
}

## for loop over a vector

primes <- c(2, 3, 5, 7, 11, 13)

loop version 1
for (p in primes) {
  print(p)
}

loop version 2
for (i in 1:length(primes)) {
  print(primes[i])
}


## for loop over a list

primes_list <- list(2, 3, 5, 7, 11, 13)

loop version 1
for (p in primes_list) {
  print(p)
}

loop version 2
for (i in 1:length(primes_list)) {
  print(primes_list[[i]])
}


## Loop over a matrix

 The tic-tac-toe matrix ttt has already been defined for you
ttt
 define the double for loop
for (i in 1:nrow(ttt)) {
  for (j in 1:ncol(ttt)) {
    print(paste("On row", i, "and column", j, "the board contains", ttt[i,j]))
  }# Pre-defined variables



Loop over a string
rquote <- "r's internals are irrefutably intriguing"
chars <- strsplit(rquote, split = "")[[1]]

Initialize rcount
rcount <- 0

Finish the for loop

for (char in chars) {
  if(char=="r"){
    rcount<-rcount+1
      }else if (char=="u"){
break        
        }
              }
 
 print(rcount)
  
}

The break statement abandons the active loop: the remaining code in the loop is skipped and the loop is not iterated over anymore.
The next statement skips the remainder of the code in the loop, but continues the iteration.

## Functions

mean() function also has this argument, na.rm, and it does the exact same thing. By default, it is set to FALSE, as the Usage of the default S3 method shows:

mean(x, trim = 0, na.rm = FALSE, ...)

**Creating your own functions**

Create a function pow_two()
pow_two<- function(x){
  return(x*x)
}

## Packages

install.packages(), which as you can expect, installs a given package.
library() which loads packages, i.e. attaches them to the search list on your R workspace.

search(), to look at the currently attached packages and
qplot(mtcars$wt, mtcars$hp), to build a plot of two variables of the mtcars data frame.


## Apply functions

**lapply(X, FUN, ...)**

To put it generally, lapply takes a vector or list X, and applies the function FUN to each of its members. If FUN requires additional arguments, you pass them after you've specified X and FUN (...). The output of lapply() is a list, the same length as X, where each element is the result of applying FUN on the corresponding element of X.

split_low<-lapply(split_math,tolower)

** Use anonymous function inside lapply()**
lapply(list(1,2,3), function(x) { 3 * x })

** lapply with additional arguments**
multiply <- function(x, factor) {
  x * factor
}
lapply(list(1,2,3), multiply, factor = 3)



Suppose you want to display the structure of every element of a list. You could use the str() function for this, which returns NULL:

lapply(list(1, "a", TRUE), str)
This call actually returns a list, the same size as the input list, containing all NULL values. On the other hand calling

str(TRUE)
on its own prints only the structure of the logical to the console, not NULL. That's because str() uses invisible() behind the scenes, which returns an invisible copy of the return value, NULL in this case. This prevents it from being printed when the result of str() is not assigned.


**sapply()**
You can use sapply() similar to how you used lapply(). The first argument of sapply() is the list or vector X over which you want to apply a function, FUN. Potential additional arguments to this function are specified afterwards (...):

sapply(X, FUN, ...)

sapply function simplifies the output format wherever it can. else the result is same as lapply.


** vapply()**

vapply(X, FUN, FUN.VALUE, ..., USE.NAMES = TRUE)
Over the elements inside X, the function FUN is applied. The FUN.VALUE argument expects a template for the return argument of this function FUN. USE.NAMES is TRUE by default; in this case vapply() tries to generate a named array, if possible.

there are cases where the structure of the output of the function you want to apply, FUN, does not correspond to the template you specify in FUN.VALUE. In that case, vapply() will throw an error that informs you about the misalignment between expected and actual output

vapply(temp, basics, numeric(4))

As highlighted before, vapply() can be considered a more robust version of sapply(), because you explicitly restrict the output of the function you want to apply. Converting your sapply() expressions in your own R scripts to vapply() expressions is therefore a good practice (and also a breeze!).

**Convert to vapply() expression**
sapply(temp, function(x, y) { mean(x) > y }, y = 5)
vapply(temp, function(x, y) { mean(x) > y }, y = 5,logical(1))


## Utility functions

Reverse Elements
rev provides a reversed version of its argument.

seq(): Generate sequences, by specifying the from, to, and by arguments.
rep(): Replicate elements of vectors and lists.
sort(): Sort a vector in ascending order. Works on numerics, but also on character strings and logicals.
rev(): Reverse the elements in a data structures for which reversal is defined.
str(): Display the structure of any R object.
append(): Merge vectors or lists.
is.*(): Check for the class of an R object.
as.*(): Convert an R object from one class to another.
unlist(): Flatten (possibly embedded) lists to produce a vector.

eg:rep(seq(1, 7, by = 2), times = 7)
 output: 1 3 5 7 1 3 5 7 1 3 5 7 1 3 5 7 1 3 5 7 1 3 5 7 1 3 5 7


## Regular expressions

grepl & grep
In their most basic form, regular expressions can be used to see whether a pattern exists inside a character string or a vector of character strings. For this purpose, you can use:

grepl(), which returns TRUE when a pattern is found in the corresponding character string.
grep(), which returns a vector of indices of the character strings that contains the pattern.
Both functions need a pattern and an x argument, where pattern is the regular expression you want to match for, and the x argument is the character vector from which matches should be sought.

You can use the caret, ^, and the dollar sign, $ to match the content located in the start and end of a string, respectively. This could take us one step closer to a correct pattern for matching only the ".edu" email addresses from our list of emails. But there's more that can be added to make the pattern more robust:

@, because a valid email must contain an at-sign.

```r
# The emails vector has already been defined for you
emails <- c("john.doe@ivyleague.edu", "education@world.gov", "dalai.lama@peace.org",
            "invalid.edu", "quant@bigdatacollege.edu", "cookie.monster@sesame.tv")

# Use grepl() to match for .edu addresses more robustly
grepl("@.*\\.edu$",emails)
```

```
## [1]  TRUE FALSE FALSE FALSE  TRUE FALSE
```

```r
# Use grep() to match for .edu addresses more robustly, save result to hits
hits<-grep("@.*\\.edu$",emails)

# Subset emails using hits
emails[hits]
```

```
## [1] "john.doe@ivyleague.edu"   "quant@bigdatacollege.edu"
```
 
**sub & gsub**
While grep() and grepl() were used to simply check whether a regular expression could be matched with a character vector, sub() and gsub() take it one step further: you can specify a replacement argument. If inside the character vector x, the regular expression pattern is found, the matching element(s) will be replaced with replacement.sub() only replaces the first match, whereas gsub() replaces all matches.


```r
# The emails vector has already been defined for you
emails <- c("john.doe@ivyleague.edu", "education@world.gov", "global@peace.org",
            "invalid.edu", "quant@bigdatacollege.edu", "cookie.monster@sesame.tv")

# Use sub() to convert the email domains to datacamp.edu
sub("@.*\\.edu$","@datacamp.edu",emails)
```

```
## [1] "john.doe@datacamp.edu"    "education@world.gov"     
## [3] "global@peace.org"         "invalid.edu"             
## [5] "quant@datacamp.edu"       "cookie.monster@sesame.tv"
```

## Time in R

In R, dates are represented by Date objects, while times are represented by POSIXct objects. Under the hood, however, these dates and times are simple numerical values. Date objects store the number of days since the 1st of January in 1970. POSIXct objects on the other hand, store the number of seconds since the 1st of January in 1970.


```r
# Get the current date: today
today<-Sys.Date()

# See what today looks like under the hood
unclass(today)
```

```
## [1] 17939
```

```r
# Get the current time: now
now<-Sys.time()

# See what now looks like under the hood
unclass(now)
```

```
## [1] 1550004493
```

Create and format dates
To create a Date object from a simple character string in R, you can use the as.Date() function. The character string has to obey a format that can be defined using a set of symbols (the examples correspond to 13 January, 1982):

%Y: 4-digit year (1982)
%y: 2-digit year (82)
%m: 2-digit month (01)
%d: 2-digit day of the month (13)
%A: weekday (Wednesday)
%a: abbreviated weekday (Wed)
%B: month (January)
%b: abbreviated month (Jan)

 default R matches your character string to the formats "%Y-%m-%d" or "%Y/%m/%d".


```r
# Definition of character strings representing dates
str1 <- "May 23, '96"
str2 <- "2012-03-15"
str3 <- "30/January/2006"

# Convert the strings to dates: date1, date2, date3
date1 <- as.Date(str1, format = "%b %d, '%y")
date2<-as.Date(str2)
date3<-as.Date(str3,format="%d/%B/%Y")

# Convert dates to formatted strings
format(date1, "%A")
```

```
## [1] "Thursday"
```

```r
format(date2, "%d")
```

```
## [1] "15"
```

```r
format(date3, "%b %Y")
```

```
## [1] "Jan 2006"
```

Create and format times
Similar to working with dates, you can use as.POSIXct() to convert from a character string to a POSIXct object, and format() to convert from a POSIXct object to a character string. Again, you have a wide variety of symbols:

%H: hours as a decimal number (00-23)
%I: hours as a decimal number (01-12)
%M: minutes as a decimal number
%S: seconds as a decimal number
%T: shorthand notation for the typical format %H:%M:%S
%p: AM/PM indicator
For a full list of conversion symbols, consult the strptime documentation in the console:

?strptime
Again,as.POSIXct() uses a default format to match character strings. In this case, it's %Y-%m-%d %H:%M:%S. In this exercise, abstraction is made of different time zones.


```r
# Definition of character strings representing times
str1 <- "May 23, '96 hours:23 minutes:01 seconds:45"
str2 <- "2012-3-12 14:23:08"

# Convert the strings to POSIXct objects: time1, time2
time1 <- as.POSIXct(str1, format = "%B %d, '%y hours:%H minutes:%M seconds:%S")
time2<-as.POSIXct(str2)

# Convert times to formatted strings
format(time1,"%M")
```

```
## [1] "01"
```

```r
format(time2,"%I:%M %p")
```

```
## [1] "02:23 PM"
```
***
***
***
***
*************
#Tidyverse
*************
***
***
***
***
***

**Filtering**

library(dplyr)

eg: Filter for China in 2002
gapminder %>% filter(year==2002, country=="China")

**Arranging**

Sort in ascending order of lifeExp
gapminder %>% arrange(lifeExp)

  
Sort in descending order of lifeExp
gapminder %>% arrange(desc(lifeExp))


Filter for the year 1957, then arrange in descending order of population
gapminder %>% filter(year==1957) %>% arrange(desc(pop))

Use mutate to change lifeExp to be in months
gapminder %>% mutate(lifeExp=lifeExp*12)

Change this plot to put the x-axis on a log scale
ggplot(gapminder_1952, aes(x = pop, y = lifeExp)) +
  geom_point()+scale_x_log10()
  
Scatter plot comparing gdpPercap and lifeExp, with color representing continent
and size representing population, faceted by year
ggplot(gapminder,aes(x=gdpPercap,y=lifeExp,color=continent,size=pop))+geom_point()+
scale_x_log10()+facet_wrap(~year)

Summarize to find the median life expectancy
gapminder %>% summarize(medianLifeExp=median(lifeExp))

Find median life expectancy and maximum GDP per capita in each year
gapminder %>% group_by(year) %>% summarize(medianLifeExp=median(lifeExp),
maxGdpPercap=max(gdpPercap))

Be sure to add expand_limits(y = 0) to make sure the plot's y-axis includes zero.

Add a title to this graph: "Comparing GDP per capita across continents"
ggplot(gapminder_1952, aes(x = continent, y = gdpPercap)) +
  geom_boxplot() +ggtitle("Comparing GDP per capita across continents")
  scale_y_log10()
  
  
***
***
***
***
*************
# Importing data in R (part1)
*************
***
***
***
***
***

read.csv
The utils package, which is automatically loaded in your R session on startup, can import CSV files with the read.csv() function.

stringsAsFactors
With stringsAsFactors, you can tell R whether it should convert strings in the flat file to factors.

For all importing functions in the utils package, this argument is TRUE, which means that you import strings as factors. This only makes sense if the strings you import represent categorical variables in R. If you set stringsAsFactors to FALSE, the data frame columns corresponding to strings in your text file will be character.


Import swimming_pools.csv correctly: pools
pools<-read.csv("swimming_pools.csv",stringsAsFactors=FALSE)

Check the structure of pools
str(pools)

read.delim
Aside from .csv files, there are also the .txt files which are basically text files. You can import these functions with read.delim(). By default, it sets the sep argument to "\t" (fields in a record are delimited by tabs) and the header argument to TRUE (the first row contains the field names).


read.table
If you're dealing with more exotic flat file formats, you'll want to use read.table(). It's the most basic importing function; you can specify tons of different arguments in this function. Unlike read.csv() and read.delim(), the header argument defaults to FALSE and the sep argument is "" by default.

Path to the hotdogs.txt file: path
path <- file.path("data", "hotdogs.txt")

Import the hotdogs.txt file: hotdogs
hotdogs <- read.table(path, 
                      sep= "", 
                      col.names = c("type", "calories", "sodium"))

Call head() on hotdogs
head(hotdogs)


Finish the read.delim() call
hotdogs <- read.delim("hotdogs.txt", header = FALSE, col.names = c("type", "calories", "sodium"))

Select the hot dog with the least calories: lily
lily <- hotdogs[which.min(hotdogs$calories), ]

Select the observation with the most sodium: tom
tom<-hotdogs[which.max(hotdogs$sodium),]

Column classes
Next to column names, you can also specify the column types or column classes of the resulting data frame. You can do this by setting the colClasses argument to a vector of strings representing classes:

read.delim("my_file.txt", 
           colClasses = c("character",
                          "numeric",
                          "logical"))
                          
                          
read_tsv
Where you use read_csv() to easily read in CSV files, you use read_tsv() to easily read in TSV files. TSV is short for tab-separated values.

This time, the potatoes data comes in the form of a tab-separated values file; potatoes.txt is available in your workspace. In contrast to potatoes.csv, this file does not contain columns names in the first row, though.

There's a vector properties that you can use to specify these column names manually.


```r
# readr is already loaded

# Column names
properties <- c("area", "temp", "size", "storage", "method",
                "texture", "flavor", "moistness")

# Import potatoes.txt: potatoes
# potatoes<-read_tsv("potatoes.txt",col_names=properties)

# Call head() on potatoes
#head(potatoes)
```

**read_delim**
Just as read.table() was the main utils function, read_delim() is the main readr function.

read_delim() takes two mandatory arguments:

file: the file that contains the data
delim: the character that separates the values in the data file


eg:

```r
# readr is already loaded

# Column names
properties <- c("area", "temp", "size", "storage", "method",
                "texture", "flavor", "moistness")

# Import potatoes.txt using read_delim(): potatoes
#potatoes<-read_delim("potatoes.txt",delim="\t",col_names=properties)
```


skip and n_max
Through skip and n_max you can control which part of your flat file you're actually importing into R.

skip specifies the number of lines you're ignoring in the flat file before actually starting to import data.
n_max specifies the number of lines you're actually importing.
Say for example you have a CSV file with 20 lines, and set skip = 2 and n_max = 3, you're only reading in lines 3, 4 and 5 of the file.

Watch out: Once you skip some lines, you also skip the first line that can contain column names!


```r
# Import 5 observations from potatoes.txt: potatoes_fragment
#potatoes_fragment <- read_tsv("potatoes.txt", skip = 6, n_max = 5, col_names = properties)
```


