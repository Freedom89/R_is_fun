---
title       : Teaching R
subtitle    : Part 1
author      : Low Yi Xiang
framework   : revealjs        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : dark      # 
revealjs    :
  theme: night
  center: "false"
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft,selfcontained}
knit        : slidify::knit2slides
---

## R Prog. Part 2

<img src = "./assets/img/GINSlogo.png" width = 400px>

<br>

[Jump To Contents](#/3)

---&vertical

## R DataFrames 

A data frame is used for storing data tables. It is a list of vectors of equal length. For example, the following variable df is a data frame containing three vectors n, s, b.

Example:


```r
name <- c("mary","john","tom")
grades <- c(89,60,74)
df_student_grades <- data.frame(name,grades)
print(df_student_grades)
```

```
##   name grades
## 1 mary     89
## 2 john     60
## 3  tom     74
```

This tutorial will teach you the basics of manuiplating csv (excel) files within R to perform analysis, joining data, etc.

This tutorial also assumes you have installed Rstudio and know how to install packages.

***
## Dataframes (Indexing)

Dataframes can be index by their row and columns using a matrix like structure. 

For example to extract the first row and first column value:


```r
df_student_grades[1,1]
```

```
## [1] mary
## Levels: john mary tom
```

If only the first entry (row) is of interest:

```r
df_student_grades[1,]
```

```
##   name grades
## 1 mary     89
```

Or if only the grades are of interest:

```r
df_student_grades[,2] #the second column represent the grades 
```

```
## [1] 89 60 74
```

***

## Dataframes (Indexing - Cont)

To extract the column names of a dataframe:


```r
names(df_student_grades)
```

```
## [1] "name"   "grades"
```

We can also use column names instead of numerical value to extract a column. 
Note* this is also true for rows. 


```r
df_student_grades[,"grades"]
```

```
## [1] 89 60 74
```

We can edit a specific cell in the dataframe:


```r
df_student_grades[3,"grades"] <- 80 #edit grades for the 3rd row 
df_student_grades[3,"grades"]
```

```
## [1] 80
```

---

## Install Libraries required 

Please install the following libraries by running these codes:


```r
install.packages(c("dplyr","tidyr","datasets","ggplot2"))
```

<br>

Please check that you can install & run these libraries.

```r
library(dplyr);
library(tidyr);
library(datasets);
library(ggplot2)
```

---

## Learning DataFrames

#### Reading/Writing Files 

- [Set Working Directory](#/4)

- [Reading/Writing Excel files, DataTypes](#/5)

#### Understanding DPLYR

- [Introduction / CheatSheet](#/6)

- [Filtering](#/7)

- [Select / Contains / Start/End](#/8)

- [Piping](#/9)

- [Introduction to Chaining](#/10)

- [Arrange](#/11)

- [Create New Columns](#/12)

- [Summarizing](#/13)

- [Grouped Operations](#/14)

- [Combine Datasets (Advanced)](#/15)

- [Window Functions (Advanced)](#/16)

- [Reshaping Data (Advanced)](#/17)

---

## Set Working Directory 

In R, you can set the working directory you wish to find the files. Please create a folder <q><b>named R_dataframe</q></b> in a location you prefer.  

Then, set your working directory as follows: (slightly different for different OS users)


```r
setwd('/Users/lowyix/Desktop/R_dataframe/')
```

Alternatively, you can nagivate to the help bar and click <q>Session - Set Working Directory - Choose directory </q> and then select the folder R_dataframe

To get your current working directory,


```r
getwd()
```


```
## [1] "/Users/lowyix/Desktop/R_dataframe/"
```

To List all the files in the working directory, you can:

```r
list.files()
```


```
## character(0)
```

[Back To Contents](#/3)

---&vertical

## Reading/Writing Excel Files 

lets load a dataset from one of the libraries; [diamonds](http://docs.ggplot2.org/0.9.3.1/diamonds.html)


```r
diamonds_df <- diamonds #if the code fails to work, check that you have loaded ggplot2 
```

#### Writing out dataframes 

To write out an excel (csv) file, 

```r
write.csv(diamonds_df,"diamonds_data.csv", row.names = FALSE)
list.files()
```


```
## [1] "diamonds_data.csv"
```

More information can be found with:

```r
?write.csv
```

<br>

[Back To Contents](#/3)

***

## Reading in Dataframes


```r
diamonds_df <- read.csv("diamonds_data.csv")
head(diamonds_df) #more on this later 
```

```
## Source: local data frame [6 x 10]
## 
##   carat       cut  color clarity depth table price     x     y     z
##   (dbl)    (fctr) (fctr)  (fctr) (dbl) (dbl) (int) (dbl) (dbl) (dbl)
## 1  0.23     Ideal      E     SI2  61.5    55   326  3.95  3.98  2.43
## 2  0.21   Premium      E     SI1  59.8    61   326  3.89  3.84  2.31
## 3  0.23      Good      E     VS1  56.9    65   327  4.05  4.07  2.31
## 4  0.29   Premium      I     VS2  62.4    58   334  4.20  4.23  2.63
## 5  0.31      Good      J     SI2  63.3    58   335  4.34  4.35  2.75
## 6  0.24 Very Good      J    VVS2  62.8    57   336  3.94  3.96  2.48
```
<br>

In R, you can manage your files too, such as deleting the files in the directory 

```r
file.remove("diamonds_data.csv")
```

<br>

[Back To Contents](#/3)


***

## Other Packages

There are other packages avaliable on CRAN to read/write excel tables and other formats such as xls or xlsx. 

However generally CSV is the prefered format as it is machine readable. (Remember that formats such as XLSX allows merge cells, multiple sheets per file etc)

<br>
<br>

Example of such packages are 

> - [openxlsx](https://cran.r-project.org/web/packages/openxlsx/openxlsx.pdf)
> - [readr](https://cran.r-project.org/web/packages/readr/readr.pdf)
> - [readxl](https://cran.r-project.org/web/packages/readxl/readxl.pdf)

<br>
<br>

[Back To Contents](#/3)

*** 

## Data Types 

In R Dataframes, there are mainly 3 types of columns, <u>Factors</u>, <u>Characeers</u> and <u>Integer/Numeric</u>. 

<br>

You can convert one class to another with commands like 

```r
as.integer(x)
as.numeric(x)
as.character(x)
as.factor(x)
```

<br>

[Back To Contents](#/3)

***

## Integer/Numeric 

Integer values means whole numbers only. For instance,


```r
as.integer(1.6)
```

```
## [1] 1
```

<br>

Numeric values means "floats" or "decimals". You can convert "strings" or integers to numerics 


```r
string_one <- "1.6"
as.numeric(string_one)
```

```
## [1] 1.6
```

```r
as.integer(string_one)
```

```
## [1] 1
```

<br>

[Back To Contents](#/3)

***

## Character

Character types are essentially "strings". For instance:


```r
as.character(c(1,2,3))
```

```
## [1] "1" "2" "3"
```

## Factors

Factors are essentially categories or "Groups" within the data. There are particularly useful when you want to do factor level operations - generally used when plotting graphs. 

They are also useful when you want to restrict operations within a Dataframe Factor Column.


```r
as.factor(c(1,2,3))
```

```
## [1] 1 2 3
## Levels: 1 2 3
```

[Back To Contents](#/3)

***

## Factors (cont)
In the dataframe diamonds_df, the "str" command runs a quick summary and we can see the "cut","color" and "clarity" are factor columns.


```r
str(diamonds)
```

```
## Classes 'tbl_df', 'tbl' and 'data.frame':	53940 obs. of  10 variables:
##  $ carat  : num  0.23 0.21 0.23 0.29 0.31 0.24 0.24 0.26 0.22 0.23 ...
##  $ cut    : Ord.factor w/ 5 levels "Fair"<"Good"<..: 5 4 2 4 2 3 3 3 1 3 ...
##  $ color  : Ord.factor w/ 7 levels "D"<"E"<"F"<"G"<..: 2 2 2 6 7 7 6 5 2 5 ...
##  $ clarity: Ord.factor w/ 8 levels "I1"<"SI2"<"SI1"<..: 2 3 5 4 2 6 7 3 4 5 ...
##  $ depth  : num  61.5 59.8 56.9 62.4 63.3 62.8 62.3 61.9 65.1 59.4 ...
##  $ table  : num  55 61 65 58 58 57 57 55 61 61 ...
##  $ price  : int  326 326 327 334 335 336 336 337 337 338 ...
##  $ x      : num  3.95 3.89 4.05 4.2 4.34 3.94 3.95 4.07 3.87 4 ...
##  $ y      : num  3.98 3.84 4.07 4.23 4.35 3.96 3.98 4.11 3.78 4.05 ...
##  $ z      : num  2.43 2.31 2.31 2.63 2.75 2.48 2.47 2.53 2.49 2.39 ...
```

The different types of cut of a diamonds are:

```r
diamonds_df %>% select(cut) %>% distinct()
```

```
## Source: local data frame [5 x 1]
## 
##         cut
##      (fctr)
## 1     Ideal
## 2   Premium
## 3      Good
## 4 Very Good
## 5      Fair
```

[Back To Contents](#/3)

***

## Factors (cont)

If one tries to edit / add data that is not within the 5 categories, an error will occur. Observe:


```r
diamonds_df[1,"cut"]  #this should return a value "Ideal"
```

```
## Source: local data frame [1 x 1]
## 
##      cut
##   (fctr)
## 1  Ideal
```

<br>

Suppose the value is changed to another category within the list, such as Premium,

```r
diamonds_df[1,"cut"] <- "Premium" #this does not produce any error
```

The "NA" value will be generated instead:


```r
diamonds_df[1,"cut"]
```

```
## Source: local data frame [1 x 1]
## 
##       cut
##    (fctr)
## 1 Premium
```

<br>

[Back To Contents](#/3)

***

## Factor (cont)

If the value is not within the list:

```r
diamonds_df[1,"cut"] <- "testing" #this does not produce any error
```

```
## Warning in `[<-.factor`(`*tmp*`, iseq, value = "testing"): invalid factor
## level, NA generated
```

```r
diamonds_df[1,"cut"]
```

```
## Source: local data frame [1 x 1]
## 
##      cut
##   (fctr)
## 1     NA
```

This is particularly useful when you want to make sure certain columns only accept certain values.

Lastly, reset the diamonds_df to its orginial value with the following code. 


```r
diamonds_df <- diamonds
```

<br>

[Back To Contents](#/3)

***

## Factors (Advance)

Just as an side note, it is possible to change the "levels" of the columns. 

The default settings in R is such that they will arrange the levels according to numeric/alphabetical order. Sometimes this may not be ideal (especially in plots), this can be corrected by the following steps:


```r
new_diamonds_df<- ggplot2::diamonds
levels(new_diamonds_df$cut)
```

```
## [1] "Fair"      "Good"      "Very Good" "Premium"   "Ideal"
```

<br>

In the case of diamonds, suppose we want the order Premium, Very Good, Good, Ideal, and Fair instead, we define a new numeric reflecting the previous levels shown above.

Note* - If you do not understand R indexing it is ok, the point of this slide is to show levels manipulation. 


```r
new_ordering <- c(4,3,2,5,1)
levels(new_diamonds_df$cut)[new_ordering] #observe the new changes 
```

```
## [1] "Premium"   "Very Good" "Good"      "Ideal"     "Fair"
```

<br>

[Back To Contents](#/3)

***

## Factors (Advance - Cont)

After defining the numeric vector, replace the orignial column with the new order:

<br>


```r
new_diamonds_df$cut <- factor(new_diamonds_df$cut,
                              levels = levels(new_diamonds_df$cut)[new_ordering])  

levels(new_diamonds_df$cut)
```

```
## [1] "Premium"   "Very Good" "Good"      "Ideal"     "Fair"
```

<br>

We can see that the levels are readjusted to the levels we desire! 

<br>

[Back To Contents](#/3)

---&vertical

## Introduction to DPLYR 

DPLYR is a package written by [Hadley Wickham](https://en.wikipedia.org/wiki/Hadley_Wickham) who is currently Chief Scientist at RStudio. 

It is a fast, consistent tool for working with data frame like objects, both in memory and out of memory.

> - [Github](https://cran.r-project.org/web/packages/dplyr/dplyr.pdf)

> - [Cheatsheet](https://www.rstudio.com/wp-content/uploads/2015/02/data-wrangling-cheatsheet.pdf)

Note* - The Cheatsheet covers a significant portion of DPLYR and a short description of each function. 

[Back To Contents](#/3)

---&vertical

## Filtering 

Lets look at the dataset again:


```r
head(diamonds_df)
```

```
## Source: local data frame [6 x 10]
## 
##   carat       cut  color clarity depth table price     x     y     z
##   (dbl)    (fctr) (fctr)  (fctr) (dbl) (dbl) (int) (dbl) (dbl) (dbl)
## 1  0.23     Ideal      E     SI2  61.5    55   326  3.95  3.98  2.43
## 2  0.21   Premium      E     SI1  59.8    61   326  3.89  3.84  2.31
## 3  0.23      Good      E     VS1  56.9    65   327  4.05  4.07  2.31
## 4  0.29   Premium      I     VS2  62.4    58   334  4.20  4.23  2.63
## 5  0.31      Good      J     SI2  63.3    58   335  4.34  4.35  2.75
## 6  0.24 Very Good      J    VVS2  62.8    57   336  3.94  3.96  2.48
```

As well as the names:

```r
names(diamonds_df)
```

```
##  [1] "carat"   "cut"     "color"   "clarity" "depth"   "table"   "price"  
##  [8] "x"       "y"       "z"
```

<br>

[Back To Contents](#/3)

***

## Filtering (Cont)

Suppose we want to look at diamonds with color 'D':


```r
diamonds_df_color_D <- filter(diamonds_df,color == 'D')
head(diamonds_df_color_D,3)
```

```
## Source: local data frame [3 x 10]
## 
##   carat       cut  color clarity depth table price     x     y     z
##   (dbl)    (fctr) (fctr)  (fctr) (dbl) (dbl) (int) (dbl) (dbl) (dbl)
## 1  0.23 Very Good      D     VS2  60.5    61   357  3.96  3.97  2.40
## 2  0.23 Very Good      D     VS1  61.9    58   402  3.92  3.96  2.44
## 3  0.26 Very Good      D     VS2  60.8    59   403  4.13  4.16  2.52
```

Suppose we want to look at diamonds with a larger carat, say size 2 and above:

```r
diamonds_df_carat_abv2 <- filter(diamonds_df,carat >= 2)
head(diamonds_df_carat_abv2,3)
```

```
## Source: local data frame [3 x 10]
## 
##   carat     cut  color clarity depth table price     x     y     z
##   (dbl)  (fctr) (fctr)  (fctr) (dbl) (dbl) (int) (dbl) (dbl) (dbl)
## 1  2.00 Premium      J      I1  61.5    59  5051  8.11  8.06  4.97
## 2  2.06 Premium      J      I1  61.2    58  5203  8.10  8.07  4.95
## 3  2.14    Fair      J      I1  69.4    57  5405  7.74  7.70  5.36
```

<br>

[Back To Contents](#/3)

***

## Filtering (Cont)

You can combine 'and' conditions or 'or' conditions as follows:

Example 'and':

```r
diamonds_df_color_D_and_carat_abv2 <- filter(diamonds_df, color == "D" & carat >= 2)
head(diamonds_df_color_D_and_carat_abv2,3)
```

```
## Source: local data frame [3 x 10]
## 
##   carat     cut  color clarity depth table price     x     y     z
##   (dbl)  (fctr) (fctr)  (fctr) (dbl) (dbl) (int) (dbl) (dbl) (dbl)
## 1  2.00    Good      D     SI2  63.8    57 10528  7.93  7.88  5.04
## 2  2.02 Premium      D     SI2  61.1    57 12108  8.12  8.05  4.94
## 3  2.00 Premium      D     SI2  59.3    62 12576  8.12  8.06  4.80
```

<br>

Example 'or'

```r
diamonds_df_color_D_or_carat_abv2 <- filter(diamonds_df, color == "D" & carat >= 2)
head(diamonds_df_color_D_or_carat_abv2,3)
```

```
## Source: local data frame [3 x 10]
## 
##   carat     cut  color clarity depth table price     x     y     z
##   (dbl)  (fctr) (fctr)  (fctr) (dbl) (dbl) (int) (dbl) (dbl) (dbl)
## 1  2.00    Good      D     SI2  63.8    57 10528  7.93  7.88  5.04
## 2  2.02 Premium      D     SI2  61.1    57 12108  8.12  8.05  4.94
## 3  2.00 Premium      D     SI2  59.3    62 12576  8.12  8.06  4.80
```

<br>

[Back To Contents](#/3)

---&vertical

## Selecting Columns

You can select Columns with the <u>"select"</u> command. For example:


```r
diamond_df_selected <- select(diamonds_df,carat,cut)
head(diamond_df_selected,3)
```

```
## Source: local data frame [3 x 2]
## 
##   carat     cut
##   (dbl)  (fctr)
## 1  0.23   Ideal
## 2  0.21 Premium
## 3  0.23    Good
```

<br> 

There are other kind of commands that can be used in conjunction with Dplyr, for example <u>"contains"</u>:


```r
diamonds_df_contains_ri <- select(diamonds_df, contains("ri"))
head(diamonds_df_contains_ri,3)
```

```
## Source: local data frame [3 x 2]
## 
##   clarity price
##    (fctr) (int)
## 1     SI2   326
## 2     SI1   326
## 3     VS1   327
```

<br>

[Back To Contents](#/3)

***

## Selecting Columns (Cont)

Example <u>'starts_with'</u>:

```r
diamonds_df_start_with_c <- select(diamonds_df, starts_with("c"))
head(diamonds_df_start_with_c,3)
```

```
## Source: local data frame [3 x 4]
## 
##   carat     cut  color clarity
##   (dbl)  (fctr) (fctr)  (fctr)
## 1  0.23   Ideal      E     SI2
## 2  0.21 Premium      E     SI1
## 3  0.23    Good      E     VS1
```
Example <u>'ends_with'</u>:

```r
diamonds_df_ends_with_t <- select(diamonds_df, ends_with("t"))
head(diamonds_df_ends_with_t,3)
```

```
## Source: local data frame [3 x 2]
## 
##   carat     cut
##   (dbl)  (fctr)
## 1  0.23   Ideal
## 2  0.21 Premium
## 3  0.23    Good
```

<br>

More information can be found in the [Cheatsheet](https://www.rstudio.com/wp-content/uploads/2015/02/data-wrangling-cheatsheet.pdf)

<br>

[Back To Contents](#/3)

---&vertical

## Piping

To understand piping, lets first understand a mock example by creating a function.


```r
multiply_each_other <- function(x,y){
  return(x*y)
}
```

Then, we can call this function as follows:

```r
multiply_each_other(2,4)
```

```
## [1] 8
```

With Piping, we can perform a similar operation as follows:

```r
2 %>% multiply_each_other(4)
```

```
## [1] 8
```

<br> 

[Back To Contents](#/3)

***

## Piping (Cont)

In other words, when you pipe an object to another function, it "fills" up the first argument of the new function. 

Observe the two codes we used earlier:

```r
df1 <- select(diamonds_df,carat)
head(df1,3)
```

```
## Source: local data frame [3 x 1]
## 
##   carat
##   (dbl)
## 1  0.23
## 2  0.21
## 3  0.23
```
vs

```r
df2 <- diamonds_df %>% select(carat)
head(df2,3)
```

```
## Source: local data frame [3 x 1]
## 
##   carat
##   (dbl)
## 1  0.23
## 2  0.21
## 3  0.23
```

<br>

[Back To Contents](#/3)

---&vertical

## Introduction to Chaining

The advantage of piping means it allows us to do chaining. To explain this concept, lets assume that you have to select some columns and filter by certain conditions. You would either:


```r
df_select <- select(diamonds_df, starts_with("c"))
df_select_filter <- filter(df_select, carat >=2)
head(df_select_filter,3)
```

```
## Source: local data frame [3 x 4]
## 
##   carat     cut  color clarity
##   (dbl)  (fctr) (fctr)  (fctr)
## 1  2.00 Premium      J      I1
## 2  2.06 Premium      J      I1
## 3  2.14    Fair      J      I1
```

OR:

```r
df_select_filter2 <- filter(select(diamonds_df, starts_with("c")),carat>=2)
head(df_select_filter2,3)
```

```
## Source: local data frame [3 x 4]
## 
##   carat     cut  color clarity
##   (dbl)  (fctr) (fctr)  (fctr)
## 1  2.00 Premium      J      I1
## 2  2.06 Premium      J      I1
## 3  2.14    Fair      J      I1
```

Notice the code can be a little hard to read - What if you have multiple functions to run?

[Back To Contents](#/3)

***

## Introduction to Chaining (Cont)

This is where Chaining is very useful by combining piping, 

Observe:

```r
df4 <- diamonds_df %>% 
  select(starts_with("c")) %>%
  filter(carat >= 2)

head(df4,3)
```

```
## Source: local data frame [3 x 4]
## 
##   carat     cut  color clarity
##   (dbl)  (fctr) (fctr)  (fctr)
## 1  2.00 Premium      J      I1
## 2  2.06 Premium      J      I1
## 3  2.14    Fair      J      I1
```

In the subsequent examples, you will see more of piping in action. 

Additional Note* - Piping exists in many other packages, such as tidyr, ggvis, leaflet and many other libraries.

[Back To Contents](#/3)

---&vertical

## Arranging

To sort the data by a particular column,


```r
diamonds_df %>% arrange(carat) %>% head(3)
```

```
## Source: local data frame [3 x 10]
## 
##   carat     cut  color clarity depth table price     x     y     z
##   (dbl)  (fctr) (fctr)  (fctr) (dbl) (dbl) (int) (dbl) (dbl) (dbl)
## 1   0.2 Premium      E     SI2  60.2    62   345  3.79  3.75  2.27
## 2   0.2 Premium      E     VS2  59.8    62   367  3.79  3.77  2.26
## 3   0.2 Premium      E     VS2  59.0    60   367  3.81  3.78  2.24
```

You can arrange by two columns as well, for example by carat and clarity:

```r
diamonds_df %>% arrange(carat,clarity) %>% head(3)
```

```
## Source: local data frame [3 x 10]
## 
##   carat     cut  color clarity depth table price     x     y     z
##   (dbl)  (fctr) (fctr)  (fctr) (dbl) (dbl) (int) (dbl) (dbl) (dbl)
## 1   0.2 Premium      E     SI2  60.2    62   345  3.79  3.75  2.27
## 2   0.2 Premium      E     VS2  59.8    62   367  3.79  3.77  2.26
## 3   0.2 Premium      E     VS2  59.0    60   367  3.81  3.78  2.24
```

[Back To Contents](#/3)

***

## Arranging (Cont)

To sort in a decreasing order, use the <u>"desc"</q></u> function:

```r
diamonds_df %>% arrange(carat,desc(clarity)) %>% head(3)
```

```
## Source: local data frame [3 x 10]
## 
##   carat     cut  color clarity depth table price     x     y     z
##   (dbl)  (fctr) (fctr)  (fctr) (dbl) (dbl) (int) (dbl) (dbl) (dbl)
## 1   0.2 Premium      E     VS2  59.8    62   367  3.79  3.77  2.26
## 2   0.2 Premium      E     VS2  59.0    60   367  3.81  3.78  2.24
## 3   0.2 Premium      E     VS2  61.1    59   367  3.81  3.78  2.32
```

Another example:

```r
diamonds_df %>% arrange(desc(carat),desc(price)) %>% head(3)
```

```
## Source: local data frame [3 x 10]
## 
##   carat    cut  color clarity depth table price     x     y     z
##   (dbl) (fctr) (fctr)  (fctr) (dbl) (dbl) (int) (dbl) (dbl) (dbl)
## 1  5.01   Fair      J      I1  65.5    59 18018 10.74 10.54  6.98
## 2  4.50   Fair      J      I1  65.8    58 18531 10.23 10.16  6.72
## 3  4.13   Fair      H      I1  64.8    61 17329 10.00  9.85  6.43
```

[Back To Contents](#/3)

---&vertical

## Creating New Columns

Creating new columns can be done with the <u>"mutate"</u> or <u>"transmute"</u>" columns. The difference between transmute and mutate is transmute drops its orginial columns.

For example, lets compute the price per carat: 


```r
diamonds_df %>% mutate(price_per_carat = price/carat) %>% 
  select(starts_with('c'),price_per_carat) %>% head(3)
```

```
## Source: local data frame [3 x 5]
## 
##   carat     cut  color clarity price_per_carat
##   (dbl)  (fctr) (fctr)  (fctr)           (dbl)
## 1  0.23   Ideal      E     SI2        1417.391
## 2  0.21 Premium      E     SI1        1552.381
## 3  0.23    Good      E     VS1        1421.739
```

With transmute:

```r
diamonds_df %>% transmute(price_per_carat = price/carat) %>% head(3)
```

```
## Source: local data frame [3 x 1]
## 
##   price_per_carat
##             (dbl)
## 1        1417.391
## 2        1552.381
## 3        1421.739
```

[Back To Contents](#/3)

***

## Creating New Columns (Cont)

You can combine ifelse / functions along with <u>mutate</u> functions.

For example you want to create a new column to differentiate large diamonds (abv 1 carat) and small diamonds. 


```r
set.seed(5) #set seed allows everyone to have the same results
diamonds_df %>% 
  mutate(big_or_small = ifelse(carat >=1, "big","small")) %>% 
  select(starts_with('c'),big_or_small) %>%
  sample_n(5) %>%
  head(5)
```

```
## Source: local data frame [5 x 5]
## 
##   carat       cut  color clarity big_or_small
##   (dbl)    (fctr) (fctr)  (fctr)        (chr)
## 1  1.00      Good      H     VS2          big
## 2  0.41   Premium      G     VS1        small
## 3  0.70      Good      E     SI1        small
## 4  1.01 Very Good      F     VS2          big
## 5  0.90 Very Good      D     SI1        small
```

<br>

[Back To Contents](#/3)

***

## Creating New Columns (Cont)

You can use functions as well:

```r
carat_big_small <- function(x){
  temp = ifelse(x>=1,"big","small")
  return(temp)
}

set.seed(5) #set seed allows everyone to have the same results
diamonds_df %>% 
  mutate(big_or_small = carat_big_small(carat)) %>% 
  select(starts_with('c'),big_or_small) %>%
  sample_n(5) %>%
  head(5)
```

```
## Source: local data frame [5 x 5]
## 
##   carat       cut  color clarity big_or_small
##   (dbl)    (fctr) (fctr)  (fctr)        (chr)
## 1  1.00      Good      H     VS2          big
## 2  0.41   Premium      G     VS1        small
## 3  0.70      Good      E     SI1        small
## 4  1.01 Very Good      F     VS2          big
## 5  0.90 Very Good      D     SI1        small
```

<br>

[Back To Contents](#/3)

---&vertical

## Summarizing

There are numerous summarize functions, lets look at some examples:


```r
diamonds_df %>% summarise(mean(table))
```

```
## Source: local data frame [1 x 1]
## 
##   mean(table)
##         (dbl)
## 1    57.45718
```

You can include multiple functions as follows:


```r
diamonds_df %>% summarise(mean = mean(table),
                          median = median(table),
                          unique_carat = n_distinct(carat),
                          max_carat = max(carat))
```

```
## Source: local data frame [1 x 4]
## 
##       mean median unique_carat max_carat
##      (dbl)  (dbl)        (int)     (dbl)
## 1 57.45718     57          273      5.01
```

[Back To Contents](#/3)

---&vertical

## Grouped Data

<u>group_by</u> should be a familar operation for those who use SQL, let's see an example first:

We want to know the relationship between the cut and the price. 

```r
diamonds_df %>% 
  group_by(cut) %>% 
  summarise(mean(price))
```

```
## Source: local data frame [5 x 2]
## 
##         cut mean(price)
##      (fctr)       (dbl)
## 1      Fair    4358.758
## 2      Good    3928.864
## 3 Very Good    3981.760
## 4   Premium    4584.258
## 5     Ideal    3457.542
```

<br>

[Back To Contents](#/3)

***

## Grouped Data (Cont)

What about the color?


```r
diamonds_df %>%
  group_by(color) %>%
  summarise(mean(price))
```

```
## Source: local data frame [7 x 2]
## 
##    color mean(price)
##   (fctr)       (dbl)
## 1      D    3169.954
## 2      E    3076.752
## 3      F    3724.886
## 4      G    3999.136
## 5      H    4486.669
## 6      I    5091.875
## 7      J    5323.818
```

<br>

[Back To Contents](#/3)

***

## Grouped Data (Cont)

Suppose you want to find out the max price within each group


```r
diamonds_df %>%
  group_by(color, cut) %>%
  summarise(max_price = max(price)) %>%
  arrange(max_price) %>%
  head(10)
```

```
## Source: local data frame [10 x 3]
## Groups: color [2]
## 
##     color       cut max_price
##    (fctr)    (fctr)     (int)
## 1       D      Fair     16386
## 2       D      Good     18468
## 3       D Very Good     18542
## 4       D   Premium     18575
## 5       D     Ideal     18693
## 6       E      Fair     15584
## 7       E      Good     18236
## 8       E   Premium     18477
## 9       E     Ideal     18729
## 10      E Very Good     18731
```

We can see that (E, Very Good) has a higher value than (D, Fair). This is because when using the group_by operation, it finds out the max price within each group. 

<br>

[Back To Contents](#/3)

***

## Grouped Data (Cont)

Sometimes you will need to <u>"ungroup()"</u> your data to remove the grouping, lets see an example:

Question : find out the highest average price within each group and then list the top 5 groups with the highest everage price. 


```r
df5 <- diamonds_df %>%
  group_by(color, cut) %>%
  summarise(mean_price = mean(price)) %>%
  arrange(desc(mean_price))

df5 %>% head(6)
```

```
## Source: local data frame [6 x 3]
## Groups: color [2]
## 
##    color       cut mean_price
##   (fctr)    (fctr)      (dbl)
## 1      D      Fair   4291.061
## 2      D   Premium   3631.293
## 3      D Very Good   3470.467
## 4      D      Good   3405.382
## 5      D     Ideal   2629.095
## 6      E      Fair   3682.312
```

We can see that (E,fair) has a higher price than (D,Ideal).

<br>


[Back To Contents](#/3)

***

## Grouped Data (Cont)

We can fix this with the <u>"ungroup"</u> option: 


```r
diamonds_df %>%
  group_by(color, cut) %>%
  summarise(mean_price = mean(price)) %>%
  ungroup() %>%
  arrange(desc(mean_price)) %>%
  head(10)
```

```
## Source: local data frame [10 x 3]
## 
##     color       cut mean_price
##    (fctr)    (fctr)      (dbl)
## 1       J   Premium   6294.592
## 2       I   Premium   5946.181
## 3       I Very Good   5255.880
## 4       H   Premium   5216.707
## 5       H      Fair   5135.683
## 6       J Very Good   5103.513
## 7       I      Good   5078.533
## 8       J      Fair   4975.655
## 9       J     Ideal   4918.186
## 10      I      Fair   4685.446
```

Now the highest 10 mean prices belong to J, I, H cuts. One can conclude that color affects the price more than the cut. 

<br>

Question:Find out which cut has the highest price within each color. 

[Back To Contents](#/3)

***

## Grouped Data (Cont)

Answer:


```r
diamonds_df %>% 
  group_by(color,cut) %>%
  summarise(mean_price = mean(price), count = n()) %>%
  ungroup() %>%
  group_by(color)%>%
  filter(mean_price == max(mean_price))
```

```
## Source: local data frame [7 x 4]
## Groups: color [7]
## 
##    color     cut mean_price count
##   (fctr)  (fctr)      (dbl) (int)
## 1      D    Fair   4291.061   163
## 2      E    Fair   3682.312   224
## 3      F Premium   4324.890  2331
## 4      G Premium   4500.742  2924
## 5      H Premium   5216.707  2360
## 6      I Premium   5946.181  1428
## 7      J Premium   6294.592   808
```

---&vertical

## Combine Datasets (Advance)

[Back To Contents](#/3)

There are two ways to join data set, either by joining, or binding. For joining data there is <u>left_join</u>, <u>right_join</u>, <u>inner_join</u>, <u>full_join</u>, <u>semi_join</u>, <u>anti_join</u>.

Define the following variables:

```r
data_A <- data.frame(names = c("amber","bryan","diana"), grades = c(84,93,56))
data_B <- data.frame(names = c("amber","bryan","charlie"), gender = c("F","M","M"))
```

left_join : join matching rows from B to A

```r
data_A %>% left_join(data_B, by = "names")
```

```
## Warning in left_join_impl(x, y, by$x, by$y): joining factors with different
## levels, coercing to character vector
```

```
##   names grades gender
## 1 amber     84      F
## 2 bryan     93      M
## 3 diana     56   <NA>
```

<br>

[Back To Contents](#/3)

***

## Combine Datasets (Adv-Cont)

Recall that dealing with factor with differnet levels will result in a warning message. To overcome this, lets change them to character levels:


```r
data_A <- data_A %>% mutate(names = as.character(names))
data_B <- data_B %>% mutate(names = as.character(names))
```

<br>

[Back To Contents](#/3)

***

## Combine Datasets (Adv-Cont)

left_join: join matching rows from b to a

```r
data_A %>% left_join(data_B, by = "names")
```

```
##   names grades gender
## 1 amber     84      F
## 2 bryan     93      M
## 3 diana     56   <NA>
```
right_join:Join matching rows from a to b.

```r
data_A %>% right_join(data_B, by = "names")
```

```
##     names grades gender
## 1   amber     84      F
## 2   bryan     93      M
## 3 charlie     NA      M
```
inner_join:Join data. Retain only rows in both sets.

```r
data_A %>% inner_join(data_B, by = "names")
```

```
##   names grades gender
## 1 amber     84      F
## 2 bryan     93      M
```

<br>

[Back To Contents](#/3)

***

## Combine Datasets (Adv-Cont)

full_join: Join data. Retain all values, all rows.

```r
data_A %>% full_join(data_B, by = "names")
```

```
##     names grades gender
## 1   amber     84      F
## 2   bryan     93      M
## 3   diana     56   <NA>
## 4 charlie     NA      M
```

semi_join: All rows in a that have a match in b.

```r
data_A %>% semi_join(data_B, by = "names")
```

```
##   names grades
## 1 amber     84
## 2 bryan     93
```
anti_join: All rows in a that do not have a match in b.

```r
data_A %>% anti_join(data_B, by = "names")
```

```
##   names grades
## 1 diana     56
```

<br>

[Back To Contents](#/3)

***

## Combine Datasets (Adv-Cont)

You can bind datasets together as well:

bind_rows:

```r
data_C <- data.frame(names = c("cheryl","elieen","faith"), grades = c(40,60,100)) %>%
  mutate(names = as.character(names))

data_A %>% bind_rows(data_C)
```

```
## Source: local data frame [6 x 2]
## 
##    names grades
##    (chr)  (dbl)
## 1  amber     84
## 2  bryan     93
## 3  diana     56
## 4 cheryl     40
## 5 elieen     60
## 6  faith    100
```

bind_cols:

```r
data_A %>% bind_cols(data_C)
```

```
## Source: local data frame [3 x 4]
## 
##   names grades  names grades
##   (chr)  (dbl)  (chr)  (dbl)
## 1 amber     84 cheryl     40
## 2 bryan     93 elieen     60
## 3 diana     56  faith    100
```

[Back To Contents](#/3)

---&vertical

## Window Functions (Advanced)

Window Functions are essentially functions that performs specific analysis. 

more details can be found [here](https://www.rstudio.com/wp-content/uploads/2015/02/data-wrangling-cheatsheet.pdf)

Suppose you want to find your cumulative sales each month: 


```r
data_sales <- data.frame(month = 1:12, sales = rnorm(12,10000,2000))
data_sales %>% mutate(cumulative_sales = cumsum(sales))
```

```
##    month     sales cumulative_sales
## 1      1 11054.889         11054.89
## 2      2 11740.625         22795.51
## 3      3  7551.755         30347.27
## 4      4  9952.436         40299.70
## 5      5 10297.745         50597.45
## 6      6  8330.116         58927.57
## 7      7 12430.554         71358.12
## 8      8 12006.911         83365.03
## 9      9 11169.850         94534.88
## 10    10  8493.949        103028.83
## 11    11  9899.260        112928.09
## 12    12 13649.063        126577.15
```

[Back To Contents](#/3)

---&vertical

## Reshaping Data (Advanced)

There are two types of data, "wide" and "long"/"narrow" format. 

The following shows a "wide" format.

<br>


|names   | weight| height|
|:-------|------:|------:|
|Amber   |     60|    152|
|Bryan   |     90|    184|
|Charlie |     80|    178|

<br>

[Back To Contents](#/3)

***
## Reshaping Data (Adv-Cont)

The following shows a 'long' format:

<br>


|names   |variable | measurements|
|:-------|:--------|------------:|
|Amber   |weight   |           60|
|Bryan   |weight   |           90|
|Charlie |weight   |           80|
|Amber   |height   |          152|
|Bryan   |height   |          184|
|Charlie |height   |          178|

<br>

More information can be found [here](https://en.wikipedia.org/wiki/Wide_and_narrow_data). There are many uses cases where you need wide over long data. 

<br>

For examples, refer [here](http://www.theanalysisfactor.com/wide-and-long-data/)

[Back To Contents](#/3)

***

## Reshaping Data (Adv-Cont)

Lets look at a more complicated example with the following mock dataset of 2 students over 2 years:

```
##   names grades_Q1_2015 grades_Q2_2015 grades_Q3_2015 grades_Q4_2015
## 1 amber             60             54             90             87
## 2 bryan             80             83             74             76
##   grades_Q1_2016 grades_Q2_2016 grades_Q3_2016 grades_Q4_2016
## 1             60             58             40             93
## 2             79             87             85             81
```

Suppose i want to find out the average score of each year, i have to write the following code:

```r
data_E %>% transmute(Y2015 = 0.25*(grades_Q1_2015+grades_Q2_2015+grades_Q3_2015+grades_Q4_2015),
                     Y2016 = 0.25*(grades_Q1_2016+grades_Q2_2016+grades_Q3_2016+grades_Q4_2016))
```

```
##   Y2015 Y2016
## 1 72.75 62.75
## 2 78.25 83.00
```

This requires lots of coding + sometimes it may not be just 8 columns in this example ; what if the data for sales is over a 10 years period and a monthly breakdown is required?

<br>

[Back To Contents](#/3)

***

## Reshaping Data (Adv-Cont)



This is when converting wide to long data can be extremely helpful for further analysis. Usually as a rule of thumb, long format is for analysis while wide format is for viewing consumption (i.e on a presentation).

For the same analysis in the previous slide: 


```r
data_E %>%
  gather(key = variable, value = score, 
         grades_Q1_2015,grades_Q2_2015,grades_Q3_2015,grades_Q4_2015,
         grades_Q1_2016,grades_Q2_2016,grades_Q3_2016,grades_Q4_2016) %>%
  separate(variable, c("grades","quarter","year"), sep = "_") %>% #More information in next slides
  group_by(names,year) %>%
  summarise(mean(score))
```

```
## Source: local data frame [4 x 3]
## Groups: names [?]
## 
##    names  year mean(score)
##   (fctr) (chr)       (dbl)
## 1  amber  2015       72.75
## 2  amber  2016       62.75
## 3  bryan  2015       78.25
## 4  bryan  2016       83.00
```

[Back To Contents](#/3)

***

## Reshaping Data (Adv-Cont)

Lets explain the first part how <u>"gather"</u> works


```r
data_E %>%
  gather(key = variable, value = score, 
         grades_Q1_2015,grades_Q2_2015,grades_Q3_2015,grades_Q4_2015,
         grades_Q1_2016,grades_Q2_2016,grades_Q3_2016,grades_Q4_2016) %>%
  head(2)
```

```
##   names       variable score
## 1 amber grades_Q1_2015    60
## 2 bryan grades_Q1_2015    80
```

OR:


```r
data_E %>%
  gather(key = variable, value = score, 
         -names) %>% #notice the hypen sign
  head(2)
```

```
##   names       variable score
## 1 amber grades_Q1_2015    60
## 2 bryan grades_Q1_2015    80
```

In other words, you specify the new key column name, the new value column name, followed by either the key columns (with the minus sign) or the value columns. 

[Back To Contents](#/3)

***

## Reshaping Data (Adv-Cont)

Heres another example with the iris dataset which is found in the documentation of gather:

By specifying the "value" columns:

```r
mini_iris <- iris[c(1, 51, 101), ]
gather(mini_iris, key = flower_att, value = measurement,
       Sepal.Length, Sepal.Width, Petal.Length, Petal.Width)
```

```
##       Species   flower_att measurement
## 1      setosa Sepal.Length         5.1
## 2  versicolor Sepal.Length         7.0
## 3   virginica Sepal.Length         6.3
## 4      setosa  Sepal.Width         3.5
## 5  versicolor  Sepal.Width         3.2
## 6   virginica  Sepal.Width         3.3
## 7      setosa Petal.Length         1.4
## 8  versicolor Petal.Length         4.7
## 9   virginica Petal.Length         6.0
## 10     setosa  Petal.Width         0.2
## 11 versicolor  Petal.Width         1.4
## 12  virginica  Petal.Width         2.5
```


[Back To Contents](#/3)

***

## Reshaping Data (Adv-Cont)

By specifying the "key" columns:

```r
gather(mini_iris, key = flower_att, value = measurement, -Species)
```

```
##       Species   flower_att measurement
## 1      setosa Sepal.Length         5.1
## 2  versicolor Sepal.Length         7.0
## 3   virginica Sepal.Length         6.3
## 4      setosa  Sepal.Width         3.5
## 5  versicolor  Sepal.Width         3.2
## 6   virginica  Sepal.Width         3.3
## 7      setosa Petal.Length         1.4
## 8  versicolor Petal.Length         4.7
## 9   virginica Petal.Length         6.0
## 10     setosa  Petal.Width         0.2
## 11 versicolor  Petal.Width         1.4
## 12  virginica  Petal.Width         2.5
```


[Back To Contents](#/3)

***

## Reshaping Data (Adv-Cont)

Usually the column names in a database or an excel sheet is uniformly labeled, such as the example provided:


```r
names(data_E)
```

```
## [1] "names"          "grades_Q1_2015" "grades_Q2_2015" "grades_Q3_2015"
## [5] "grades_Q4_2015" "grades_Q1_2016" "grades_Q2_2016" "grades_Q3_2016"
## [9] "grades_Q4_2016"
```

After the gather step, we arrive at and we want to split the names to 3 different columns:


```r
data_E %>%
  gather(key = variable, value = score, 
         -names) %>% #notice the hypen sign
  head(2)
```

```
##   names       variable score
## 1 amber grades_Q1_2015    60
## 2 bryan grades_Q1_2015    80
```

<br>

[Back To Contents](#/3)

***

## Reshaping Data (Adv-Cont)

We can achieve this by the <u>"separate"</u> function: 

The way to use it is separate(col_name,new_col_names, separator)

```r
data_F <- data_E %>%
  gather(key = variable, value = score, 
         -names) %>% #notice the hypen sign
    separate(variable, c("grades","quarter","year"), sep = "_") 
data_F %>% head(2)
```

```
##   names grades quarter year score
## 1 amber grades      Q1 2015    60
## 2 bryan grades      Q1 2015    80
```

you can type ?separate in your console to find out more! the opposite of this is unite. 

<br>

[Back To Contents](#/3)

***

## Reshaping Data (Adv-Cont)

Example <u>unite</u>:

unite(new_col_name,col_to_merge(s),separator)

```r
data_G <- data_F %>% unite(variable,grades,quarter,year,sep="_") 
data_G %>% head(5)
```

```
##   names       variable score
## 1 amber grades_Q1_2015    60
## 2 bryan grades_Q1_2015    80
## 3 amber grades_Q2_2015    54
## 4 bryan grades_Q2_2015    83
## 5 amber grades_Q3_2015    90
```

you can type ?unite in your console to find out more! 

<br>

[Back To Contents](#/3)

***

## Reshaping Data (Adv-Cont)

The opposite of gather is <u>spread</u>:
gather(variable_column,value_column)

```r
data_G %>% spread(key = variable, value = score)
```

```
##   names grades_Q1_2015 grades_Q1_2016 grades_Q2_2015 grades_Q2_2016
## 1 amber             60             60             54             58
## 2 bryan             80             79             83             87
##   grades_Q3_2015 grades_Q3_2016 grades_Q4_2015 grades_Q4_2016
## 1             90             40             87             93
## 2             74             85             76             81
```

<br>

[Back To Contents](#/3)

---&vertical

#End!

<br>
<br>
<br>
[Back To Contents](#/3)









