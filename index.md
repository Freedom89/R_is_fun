---
title       : Teaching R
subtitle    : Part 1
author      : Low Yi Xiang
framework   : revealjs        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
revealjs    :
  theme: night
  center: "false"
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft,selfcontained}
knit        : slidify::knit2slides
---

## R Prog. Part 1

[My linkedin profile](www.google.com)

--- .class #id 

## The R programming

.fragment <q> R is an open source langauge with multiple libraries avaliable. It is a widely used programming langauge for various purposes, such as data wrangling, visualization, modeling and even building this deck! </q>


--- &vertical

## Downloading R

.fragment Head over to website https://cran.r-project.org/bin/ or Google <q> Install R for <mac/windows> </q> and click on the first link

<br>

.fragment Choose the OS your machine is on, download & Install software. 

<br>

***

## Download Rstudio 

.fragment Head over to Rstudio website https://www.rstudio.com/products/rstudio/download2/ , download Rstudio (Free license) and install it. 

<br>

.fragment Launch Rstudio and you should arrive at this image below:

***

## Rstudio! 

![width](https://www.safaribooksonline.com/library/view/getting-started-with/9781449314798/httpatomoreillycomsourceoreillyimages1135858.png)

---

## Learning R (part 1)

Things we will go through in the next 1-2 hours!

<br>

-  [Basics Calculations](#/4)

-  [Assigning Variables](#/5)

-  [if-else statements](#/6)

-  [Vectors](#/7)

-  [Lists](#/8)

-  [Functions](#/9)

-  [Loops](#/10)

-  [Installing packages](#/11)

-  Datatypes (characters, numeric, integers, factors) (part 2)

-  Dataframes (part 2)

-  Intermediate R (part2)

---

## Basic calculations

In any programming languages, parenthesis are very important. (e.g, every bracket must have closure, commas must be used carefully). 
 
In R, you can do basic calculations like most scientifc computing languages such as Matlab, Python. 


```r
1+1 #addition

10-2 #substraction

100+2 - 4 #addition and substraction

224*2 #multiplication

84/4 #division

2^7 #power
```

### R can handle strings too!


```r
"a"
"b"
"this is a cat"
```

[Back To Contents](#/3)

---&vertical

## Assigning Variables

in R, you can assign values / calculations to words with the __"<-"__ or __"="__ symbol


```r
one <- 1
two <- 2
three <- 3
cat <- "cat"
dog <- "dog"
```

you can print them out by typing them or with the __<u>print</u>__ command


```r
print(cat)
```

```
## [1] "cat"
```

[Back To Contents](#/3)

*** 

## Do More Stuff With Variables!

You can perform calculations with Variables, for example:


```r
one+one

two/three

three*two + one 
```

However, if you have not defined the variable, an error is returned


```r
four
```

```
## Error in eval(expr, envir, enclos): object 'four' not found
```

You can also assign new variables to these calculations

```r
four = two*two
four = three+one

print(four)
```

```
## [1] 4
```

[Back To Contents](#/3)

---&vertical

## if-else statements

You can write conditions to check on variables and other kind of objects such as lists, matrices, dataframes etc. Recall that parenthesis is important, watch out for your brackets! 

<br> 

#### Understanding conditions

The <q>if statement</q> allows you to check for a condition, and the condition must return <u>TRUE</u> or <u>FALSE</u>. Example of conditions can be found below:


```r
animal <- "cat"
print(animal == "cat")
```

```
## [1] TRUE
```

There are other functions (more on that later) and conditions symbol, such as <q>!=</q> (not equal), <q> >= </q> (greater than) as well as <q><=</q> (smaller than)

##### Examples:


```r
one <- 1 ; two <-2 
two <= one
```

```
## [1] FALSE
```

[Back To Contents](#/3)

***

## Writing your first if statement

Here is an example of an if-statement. <q>(animal == "cat")</q> is the condition, and the round brackets are required. 

In addition, notice the curly brackets which are the parenthesis. 


```r
animal <- "cat"
if(animal == "cat"){
  print("your animal is a cat!")
}
```

```
## [1] "your animal is a cat!"
```

#### Exercise:

### Question 1.1

What happens when you declare a variable <q> animal <- "cat" </q> and write an if statement that if the animal is a bird, print the statement <i>"your animal is a bird" </i>?

### Question 1.2

Write another if statement that if the animal is not a dog, print the statement <i>"your animal is not a dog" </i>.

[Back To Contents](#/3)


***

## Answer for Question 1

#### Question 1.1 Solution

```r
animal <- "cat"

if(animal == "bird"){
  print("your animal is a bird")
}
```

Nothing is printed out! 

#### Question 1.2 Solution

```r
animal <- "cat"

if(animal != "dog"){
  print("your animal is not a dog")
}
```

```
## [1] "your animal is not a dog"
```

What if for question 1.1 you wanted to follow up with the if statement and also print out <q> "your animal is not a bird" </q> ?

[Back To Contents](#/3)

***

## Else statement

#### Introducing the else statement 

Example: 


```r
animal <- "cat"

if(animal == "bird"){
  print("your animal is a bird")
}else{
  print("your animal is not a bird")
}
```

```
## [1] "your animal is not a bird"
```

What if you have multiple conditions you want to check? One way to do it is to write multiple else-if statements. 


```r
animal <- "cat"

if(animal == "bird"){
  print("your animal is a bird")
}else if(animal == "dog"){
  print("your animal is a dog")
}else{
  print("your animal is not a bird or dog")
}
```

```
## [1] "your animal is not a bird or dog"
```

[Back To Contents](#/3)

***

## ifelse statements

There is also an if-else statement that is fairly convenient for simple tasks. In R, you can type <q>?ifelse</q> or any functions with a question mark infront to access the documentation. 

<br>

try the command <q>?ifelse</q> and read the documentation now. 

<br>

Heres an additional example:


```r
first_digit <- 2
second_digit <- 4

ifelse(first_digit <= second_digit, "first digit is bigger", "second digit is bigger")
```

```
## [1] "first digit is bigger"
```


[Back To Contents](#/3)

***
## More on conditions 

You should notice by now that in all of these statements all require a conditional statement that turns either <i> TRUE </i> or <i> FALSE </i>.

<br>

You can combine these conditions with additional and statements or assign them to variables. 


```r
digit1 <- 1 ;digit2 <- 2 ; digit3 <-3
condition1 <- digit2 >= digit1
condition2 <- digit3 <= digit2

print(condition1 & condition2 ) #TRUE AND FALSE = FALSE
```

```
## [1] FALSE
```

```r
print(condition1 || condition2) #TRUE OR FALSE = TRUE 
```

```
## [1] TRUE
```

```r
#you can then stack them together. 
condition3 <- condition1 || condition2
if(condition3){
  #code here
}
```

```
## NULL
```

[Back To Contents](#/3)

---&vertical

## Vectors

In R, sometimes you want to store multiple values, such as observations of a person height. You can declare them by using <q>c()</q>. More information can be found by <q>?c</q>

#### Example:


```r
random_numbers <- c(1,6,3,1,8,5,7,9,0,2)
```

You can perform math operations on vectors, try them out! 


```r
sum(random_numbers) #find the sum
mean(random_numbers) #find the average
mode(random_numbers) #find the most freq. item
min(random_numbers) #find the minimum number 
max(random_numbers) #find the maximum number
random_numbers*2  #multiply by 2
random_numbers -1 #substract each element by 1 
```

There is alot more functionality avaliable in vectors - but usually you will google them as you need them along the way. 

[Back To Contents](#/3)

***

## Vectors Methods

Vectors have some methods, such as finding out the length of the vector with <q> length(vector)</q>.
You can also index specific part of the vectors with square brackets. Multiple elements can be extracted out with either a another vector as follows:


```r
random_numbers[1] #extract the first element
```

```
## [1] 1
```

```r
random_numbers[c(4,6)] #extract the 4th and 6th element
```

```
## [1] 1 5
```

You can also use a TRUE/FALSE vector 


```r
greater_than_two <- random_numbers > 2
greater_than_two
```

```
##  [1] FALSE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
```

```r
random_numbers[greater_than_two]
```

```
## [1] 6 3 8 5 7 9
```

[Back To Contents](#/3)

---&vertical

## Lists

One limitation with vectors is that you can only store individual elements in them. Suppose that you want to store 2 different vectors together:


```r
a <- c(1,2,3)
b <- c(4,5,6)
new_vect <- c(a,b)
print(new_vect)
```

```
## [1] 1 2 3 4 5 6
```

Lists overcome this problem:


```r
new_list <- list(a,b)
print(new_list)
```

```
## [[1]]
## [1] 1 2 3
## 
## [[2]]
## [1] 4 5 6
```

[Back To Contents](#/3)

***

## Indexing Lists 

Lists can be indexed in the same way with vectors however they need double square brackets. <q> list[[elements]] </q>.

#### Example:


```r
new_list[[c(1)]]
```

```
## [1] 1 2 3
```

In Lists, it is also possible to assign names and index them by their names. For example: 


```r
new_list2 <- list(first_A=a,second_B=b)
new_list2[["first_A"]]
```

```
## [1] 1 2 3
```


[Back To Contents](#/3)

***
## Indexing Lists (Part2)

In list, indexing multiple elements is slightly different. 

#### Example


```r
new_list[c(1,2)] 
```

```
## [[1]]
## [1] 1 2 3
## 
## [[2]]
## [1] 4 5 6
```

Using double square results would mean that you are taking sub-elements. 


```r
new_list[[c(1,2)]] #taking the first element, then take the second element. 
```

```
## [1] 2
```

Usually to take sub-elements, you would extract out each element and use indexing appropriate for that class. 


```r
new_list[[1]][2]
```

```
## [1] 2
```

[Back To Contents](#/3)

***
## List (Advanced)

List have apply functions that is beyond the scope of this course More information can be found [here](http://stackoverflow.com/questions/3505701/r-grouping-functions-sapply-vs-lapply-vs-apply-vs-tapply-vs-by-vs-aggrega). You can also type <q>?lapply</q> to find out more. 

<br>

Do note that with the introduction of dataframes and the dplyr package (part2), most people prefer using dataframes rather than lists when it comes to manipulating data. 

<br> 

Nevertheless, Lists are still very important and could be extremly useful as they can store many different objects. Infact, <b><u>they can store about anything such as models, dataframes, functions</b></u>. They can also be used for [functional programming](http://adv-r.had.co.nz/Functional-programming.html) which is considered an advance topic.

[Back To Contents](#/3)

---&vertical

## Functions

Functions

[Back To Contents](#/3)

---&vertical

## Loops

Loops

[Back To Contents](#/3)

---&vertical

## Installing packages

Packages

[Back To Contents](#/3)

---&vertical

## End! 

<q> <b> Part 2 - DataFrames </b> </q>




