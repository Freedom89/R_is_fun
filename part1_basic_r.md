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

## R Prog. Part 1


<img src = "./assets/img/GINSlogo.png" width = 400px>

<br>

[Jump To Contents](#/3)

--- .class #id 

## The R programming

.fragment <q> R is an open source langauge with multiple libraries avaliable. It is a widely used programming langauge for various purposes, such as data wrangling, visualization, modeling and even building this deck! </q>

<br>

.fragment RStudio and R 3.3.x have been risk-assessed for local computer usage including the packages that are available on CRAN

<br>

.fragment Some resources (including Shiny Server Pro etc) on how Merck uses R can be found here: https://share.merck.com/pages/viewpage.action?pageId=93356897

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

***

## Scripting Environment

Click on the top left icon with the green "plus" sign to launch a script

![width](http://rprogramming.net/wp-content/uploads/2012/10/RStudio-Screenshot.png)

***

## Saving Scripts

You can create a folder you like and click on the save icon (floppy disk). A Pop up menu should guide you along.

<br>

Alternatively if you prefer to save a new copy at a differnet location, do the usual File -> Save as -> ... 


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

You can write conditions to check on variables and other kind of variables such as lists, matrices, dataframes etc. Recall that parenthesis is important, watch out for your brackets! 

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

Usually to take sub-elements, one would extract out each element and use appropriate indexing for that class. In this example the class happens to be a vector. 


```r
new_list[[1]][c(1,2)]
```

```
## [1] 1 2
```

[Back To Contents](#/3)

***
## List (Advanced)

List have apply functions that is beyond the scope of this course More information can be found [here](http://stackoverflow.com/questions/3505701/r-grouping-functions-sapply-vs-lapply-vs-apply-vs-tapply-vs-by-vs-aggrega). You can also type <q>?lapply</q> to find out more. 

<br>

Do note that with the introduction of dataframes and the dplyr package (part2), most people prefer using dataframes rather than lists when it comes to manipulating data. 

<br> 

Nevertheless, Lists are still very important and could be extremly useful as they can store many different variables. Infact, <b><u>they can store about anything such as models, dataframes, functions</b></u>. They can also be used for [functional programming](http://adv-r.had.co.nz/Functional-programming.html) which is considered an advance topic.

[Back To Contents](#/3)

---&vertical

## Functions

.fragment If you are familar with programming, you will understand that functions are very important. 

<br>

.fragment For those who are not familar, functions are essentially methods you can use to apply to variables and some output. 

<br>

.fragment In other words, there are sometimes you need to apply the same code multiple times, this is where functions are useful as it (1) reduces the code you need , (2) readability, (3) saves time

<br>

[Back To Contents](#/3)

***

## Functions (Example)

For instance, you need to take the square of a variable, square it, substract by itself, and add 8 to it. 


```r
x <- 2 
x <- x^2- x + 8 
x
```

```
## [1] 10
```

Suppose you need to do it multiple times, this might be a better approach. 


```r
x<-2
function_example <- function(x){
  x <- x^2-x+8
  return(x)
}
x <- function_example(x)
```


[Back To Contents](#/3)

***

## Functions (Details)

As seen in the previous slides, functions are essentially codes that you can re-use without explicitly typing them out. A function has to contain 3 parts, declaration of variables / function name, the body, and the output which is the return function. 

<br>

In the earlier example, <q>function_example</q> is the function name, <q>x</q> is the input variable, while <q> x <- x^2 - x+8</q> is the body, and <q>return(x)</q> is the code.

<br>

Heres another (trivial) example, suppose we want to two numbers and multiply them together with a function:


```r
multiply_two_numbers <- function(x,y){
  new_number <- x*y
  return(x*y)
}
```

[Back To Contents](#/3)

***
## Functions (Summary)

The code below shows the outline of a function:

<br>


```r
<function_name> <- function(input_1,input_2, ... , input_n){ #notice the brackets
  #your code here
        .
        .
        .
  return(<return the variables you require>)
}
```

[Back To Contents](#/3)

***

## Functions (Questions)

<br>

#### Question 2.1

Write a function that takes in a string variable, checks whether it is a dog or a cat, otherwise return the string <u> "it is neither a dog nor a cat" </u>

<br>

#### Question 2.2 

Write a funtion that takes in a vector of numerical values, and return a list of results computing the length,max, min, and mean. 

[Back To Contents](#/3)

***

## Functions (Answers)

#### Question 2.1


```r
test_cat_dog <- function(animal){
  
  if(animal == "dog"){
    return("your animal is a dog")
    
  }else if(animal == "cat"){
    return("your animal is a cat")
    
  }else{
    return("your animal is neither a cat nor a dog")
  }
}

test_cat_dog("dog")
```

```
## [1] "your animal is a dog"
```

```r
test_cat_dog("bird")
```

```
## [1] "your animal is neither a cat nor a dog"
```

<br>

[Back To Contents](#/3)

***

## Functions (Answers)

#### Question 2.2


```r
summary_stats <- function(x){
  length_x <- length(x)
  mean_x   <- mean(x)
  min_x    <- min(x)
  max_x    <- max(x)
  
  return_list <- list(length = length_x, mean = mean_x, min = min_x, max = max_x)
  
  return(return_list)
}

summary_stats(c(1,2,3,4,5))
```

```
## $length
## [1] 5
## 
## $mean
## [1] 3
## 
## $min
## [1] 1
## 
## $max
## [1] 5
```

<br>

[Back To Contents](#/3)

***

## Functions (Further comments)

<br>

.fragment There are other features about functions in R such as inheritance, functional programming or specifiying default values which are out of scope of this course. 

<br>

.fragment To recap, functions are a extremely useful way to write neater and shorter codes. As a rule of thumb, if you need to write the same code twice or more, it is probably a good idea to write a function for it. 

<br>

.fragment Sometimes, you would be using functions that are built by others in the form of packages(#/11), it is thus important that you know how to write / read / call functions to help your data analysis in R! 

<br>

[Back To Contents](#/3)

---&vertical

## Loops

.fragment There are times when you need to do some task over and over again - in this case, you should think of loops! 

<br>

.fragment There are two kind of loops - <q>for</q> and <q>while</q> loops.

<br>

.fragment  <q>for</q> loops runs within a fixed set and perform some tasks for you. More examples will be shown later. 

<br>

.fragment <q>while</q> loops runs until a certain condition is satisified. 

[Back To Contents](#/3)

***

## For Loops

In <q>for</q> loops, the structure is as follows:


```r
for(i in 1:10){ #do something for ten times 
  #do something
}
```

It also possible to specify a vector to 'loop' through :


```r
student_names <- c("Mary","John","Peter","Berry")
for(i in student_names){
  print(i)
  #code to do task related to each student's name. 
}
```

```
## [1] "Mary"
## [1] "John"
## [1] "Peter"
## [1] "Berry"
```

<br>

[Back To Contents](#/3)

***

## For Loops (Questions) 

#### Question 3.1

Specify a vector of 1:100 and using a for loop, compute the sum of all numbers in this range that are divisible by 3. 

Hint1: to find the remainder of two numbers can be found with the modulo function in R, e.g 4%%2 = 0, while 4%%3 = 1. 

Hint2: you can specify a variable to keep track of the running sum of variables. 


```r
numbers <- 1:100
running_sum <- 0 
for(i in numbers){
  running_sum <- running_sum + i  #keeping track of the total sum.
}
print(running_sum)
```

```
## [1] 5050
```

<br>

[Back To Contents](#/3)

***

## While Loops

While loops is generally used when you want to achieve a task and is uncertain about the steps you need to take. The sturcture is as follows:

```r
condition <- TRUE
while(condition){ #notice the brackets
  #do some stuff 
  #if the condition is fufilled, change it to FALSE and the while loop stops running. 
  }
```

As an example: 

```r
i=1 ; condition <- TRUE
while(condition){
  print(i) ; i<- i+1
  if(i == 3){
    condition<-FALSE
  }
}
```

```
## [1] 1
## [1] 2
```

Becareful with while loops as you might encounter infinite loops - the loop will run forever since the condition will never be false! 

[Back To Contents](#/3)

***

## While Loops (Question)

#### Question3.2

Using a while loop, find out how many numbers is required to have a running sum that is greater than 500 with numbers that are divisible by three.

Hint:


```r
sum_required <- 500
condition <- TRUE
i <- 1 #start from 1
running_sum <- 0
while(condition){
  #check if i is divisble by three
  #if yes, running_sum <- running_sum+i 
  #check if running_sum exceeds sum_required
  i <- i+1 #add 1 to "i" to start the next interation. 
}
```

<br>

[Back To Contents](#/3)

***

## While Loops (Answer)

#### Question3.2

Answer:


```r
sum_required <- 500
condition <- TRUE
i <- 1 #start from 1
running_sum <- 0
while(condition){
  if(i %% 3 == 0 ){
    running_sum <- running_sum +i
  }
  if(running_sum >= sum_required){
    condition <- FALSE
  }
  i<- i+1
}
print(i)
```

```
## [1] 55
```

<br>

Bonus Challenge: how many numbers in total were used to achieve a sum exceeding 500 with numbers that are 

[Back To Contents](#/3)

***

## While Loop (Bonus Challenge)


```r
sum_required <- 500
condition <- TRUE
i <- 1 #start from 1
running_sum <- 0
counter <- 0 
while(condition){
  if(i %% 3 == 0 ){
    running_sum <- running_sum +i
    counter <- counter+1 #just add in a counter here to see when is this condition triggered. 
  }
  if(running_sum >= sum_required){
    condition <- FALSE
  }
  i<- i+1
}
print(counter)
```

```
## [1] 18
```

<br>

[Back To Contents](#/3)

***

## Loops (cont)

There are two additional functionality that are useful - <b><u> break </b></u> and <b><u> next </b></u>.

The break commands basically stops the loops from running while the next command simply moves on to the next iteration of the loop. 

##### "break" command

```r
for( i in 1:4){
  if(i == 3){break}
  print(i)
}
```

```
## [1] 1
## [1] 2
```

#### "next" command

```r
for( i in 1:4){
  if(i == 3){next}
  print(i)
}
```

```
## [1] 1
## [1] 2
## [1] 4
```

[Back To Contents](#/3)

---&vertical

## Installing packages

R is a widely contributed by people all over the world, there are currently 8992 packagess avaliable on [CRAN](https://cran.r-project.org/) not accounting for other libraries on github. 

<br>

To see the libraries avaliable by [date](https://cran.r-project.org/web/packages/available_packages_by_date.html) or by [name](https://cran.r-project.org/web/packages/available_packages_by_name.html).

<br>

In the next part we will be playing around with dataframes, please run the following codes in your console.


```r
install.packages("dplyr")
install.packages("tidyr")
install.packages("packrat")
```

<br>

[Back To Contents](#/3)

---&vertical

# End! 

<br>
<br>
<br>
[Back To Contents](#/3)




