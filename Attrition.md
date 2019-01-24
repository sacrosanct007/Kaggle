---
title: "Attrition"
output: 
  html_document: 
    keep_md: yes
---



The below analysis is inspired from Kaggle Kernel below:
https://www.kaggle.com/janiobachmann/attrition-in-an-organization-why-workers-quit/notebook

---------------------------------------------------------------------------
# Importing libraries
---------------------------------------------------------------------------

##Pacman

Pacman is more than just a nicer way to load packages. Instead of having to write 5 lines of code to load for 5 common data munging packages, like so:

library(dplyr)
library(tidyr)
library(plyr) 
library(magrittr)
library(ggplot2)

You can write one line

pacman::p_load(dplyr,tidyr,plyr,ggplot2, magrittr)

##require()

The library() and require() can be used to attach and load add-on packages which are already installed. 
The main difference between these functions are,

The library() by default returns an error if the requested package does not exist.

example:
library(xyz)
Error in library(xyz) : there is no package called ‘xyz’

The require() is designed to be used inside functions as it gives a warning message and returns a logical value say, FALSE if the requested package is not found and TRUE if the package is loaded.

example:
 require(xyz)
 
 
##How to resize the plots in a Jupyter notebook?

To set the plot width and height to something else, e.g. 4 inches wide and 3 inches high, use:

options(repr.plot.width=4, repr.plot.height=3)




##How to suppress warnings globally in an R Script?

I could use
suppressWarnings(expr)

for single statements. But how can I suppress warnings in R globally?

You want options(warn=-1). However, note that warn=0 is not the safest warning level and it should not be assumed as the current one, particularly within scripts or functions. Thus the safest way to temporary turn off warnings is:

oldw <- getOption("warn")
options(warn = -1)

[your "silenced" code]

options(warn = oldw)




