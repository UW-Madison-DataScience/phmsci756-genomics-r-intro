---
title: "Extra: R Basics continued - factors"
teaching: 20
exercises: 20
source: Rmd
---


::::::::::::::::::::::::::::::::::::::: objectives

- Be able to retrieve (subset), name, or replace, values from a vector
- Be able to use logical operators in a subsetting operation

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- How can I use an object with multiple objects in it?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Vectors

Vectors are probably the
most used commonly used object type in R.
**A vector is a collection of values that are all of the same type (numbers, characters, etc.)**.
One of the most common
ways to create a vector is to use the `c()` function - the "concatenate" or
"combine" function. Inside the function you may enter one or more values; for
multiple values, separate each value with a comma:


```r
# Create the SNP gene name vector

snp_genes <- c("OXTR", "ACTN3", "AR", "OPRM1")
```

Vectors always have a **mode** and a **length**.
You can check these with the `mode()` and `length()` functions respectively.
Another useful function that gives both of these pieces of information is the
`str()` (structure) function.


```r
# Check the mode, length, and structure of 'snp_genes'
mode(snp_genes)
```

```{.output}
[1] "character"
```

```r
length(snp_genes)
```

```{.output}
[1] 4
```

```r
str(snp_genes)
```

```{.output}
 chr [1:4] "OXTR" "ACTN3" "AR" "OPRM1"
```

Vectors are quite important in R. Another data type that we will
work with later in this lesson, data frames, are collections of
vectors. What we learn here about vectors will pay off even more
when we start working with data frames.

## Creating and subsetting vectors

Let's create a few more vectors to play around with:


```r
# Some interesting human SNPs
# while accuracy is important, typos in the data won't hurt you here

snps <- c("rs53576", "rs1815739", "rs6152", "rs1799971")
snp_chromosomes <- c("3", "11", "X", "6")
snp_positions <- c(8762685, 66560624, 67545785, 154039662)
```

Once we have vectors, one thing we may want to do is specifically retrieve one
or more values from our vector. To do so, we use **bracket notation**. We type
the name of the vector followed by square brackets. In those square brackets
we place the index (e.g. a number) in that bracket as follows:


```r
# get the 3rd value in the snp vector
snps[3]
```

```{.output}
[1] "rs6152"
```

In R, every item your vector is indexed, starting from the first item (1)
through to the final number of items in your vector. You can also retrieve a
range of numbers:


```r
# get the 1st through 3rd value in the snp vector

snps[1:3]
```

```{.output}
[1] "rs53576"   "rs1815739" "rs6152"   
```

If you want to retrieve several (but not necessarily sequential) items from
a vector, you pass a **vector of indices**; a vector that has the numbered
positions you wish to retrieve.


```r
# get the 1st, 3rd, and 4th value in the snp vector

snps[c(1, 3, 4)]
```

```{.output}
[1] "rs53576"   "rs6152"    "rs1799971"
```

There are additional (and perhaps less commonly used) ways of subsetting a
vector (see [these
examples](https://thomasleeper.com/Rcourse/Tutorials/vectorindexing.html)).
Also, several of these subsetting expressions can be combined:


```r
# get the 1st through the 3rd value, and 4th value in the snp vector
# yes, this is a little silly in a vector of only 4 values.
snps[c(1:3,4)]
```

```{.output}
[1] "rs53576"   "rs1815739" "rs6152"    "rs1799971"
```

## Adding to, removing, or replacing values in existing vectors

Once you have an existing vector, you may want to add a new item to it. To do
so, you can use the `c()` function again to add your new value:


```r
# add the gene "CYP1A1" and "APOA5" to our list of snp genes
# this overwrites our existing vector
snp_genes <- c(snp_genes, "CYP1A1", "APOA5")
```

We can verify that "snp\_genes" contains the new gene entry


```r
snp_genes
```

```{.output}
[1] "OXTR"   "ACTN3"  "AR"     "OPRM1"  "CYP1A1" "APOA5" 
```

Using a negative index will return a version of a vector with that index's
value removed:


```r
snp_genes[-6]
```

```{.output}
[1] "OXTR"   "ACTN3"  "AR"     "OPRM1"  "CYP1A1"
```

We can remove that value from our vector by overwriting it with this expression:


```r
snp_genes <- snp_genes[-6]
snp_genes
```

```{.output}
[1] "OXTR"   "ACTN3"  "AR"     "OPRM1"  "CYP1A1"
```

We can also explicitly rename or add a value to our index using double bracket notation:


```r
snp_genes[6]<- "APOA5"
snp_genes
```

```{.output}
[1] "OXTR"   "ACTN3"  "AR"     "OPRM1"  "CYP1A1" "APOA5" 
```

:::::::::::::::::::::::::::::::::::::::  challenge

## Exercise: Examining and subsetting vectors

Answer the following questions to test your knowledge of vectors

Which of the following are true of vectors in R?
A) All vectors have a mode **or** a length  
B) All vectors have a mode **and** a length  
C) Vectors may have different lengths  
D) Items within a vector may be of different modes  
E) You can use the `c()` to add one or more items to an existing vector  
F) You can use the `c()` to add a vector to an existing vector

:::::::::::::::  solution

## Solution

A) False - Vectors have both of these properties  
B) True  
C) True  
D) False - Vectors have only one mode (e.g. numeric, character); all items in  
a vector must be of this mode.
E) True  
F) True  



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

## Logical Subsetting

There is one last set of cool subsetting capabilities we want to introduce. It is possible within R to retrieve items in a vector based on a logical evaluation or numerical comparison. For example, let's say we wanted get all of the SNPs in our vector of SNP positions that were greater than 100,000,000. We could index using the '>' (greater than) logical operator:


```r
snp_positions[snp_positions > 100000000]
```

```{.output}
[1] 154039662
```

In the square brackets you place the name of the vector followed by the comparison operator and (in this case) a numeric value. Some of the most common logical operators you will use in R are:

| Operator            | Description                                                                                                                                                                                                                                 |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| \<                   | less than                                                                                                                                                                                                                                   |
| \<=                  | less than or equal to                                                                                                                                                                                                                       |
| \>                   | greater than                                                                                                                                                                                                                                |
| \>=                  | greater than or equal to                                                                                                                                                                                                                    |
| \==                  | exactly equal to                                                                                                                                                                                                                            |
| !=                  | not equal to                                                                                                                                                                                                                                |
| !x                  | not x                                                                                                                                                                                                                                       |
| a \| b               | a or b                                                                                                                                                                                                                                      |
| a \& b               | a and b                                                                                                                                                                                                                                     |

:::::::::::::::::::::::::::::::::::::::::  callout

## The magic of programming

The reason why the expression `snp_positions[snp_positions > 100000000]` works
can be better understood if you examine what the expression "snp\_positions > 100000000"
evaluates to:


```r
snp_positions > 100000000
```

```{.output}
[1] FALSE FALSE FALSE  TRUE
```

The output above is a logical vector, the 4th element of which is TRUE. When
you pass a logical vector as an index, R will return the true values:


```r
snp_positions[c(FALSE, FALSE, FALSE, TRUE)]
```

```{.output}
[1] 154039662
```

If you have never coded before, this type of situation starts to expose the
"magic" of programming. We mentioned before that in the bracket notation you
take your named vector followed by brackets which contain an index:
**named\_vector[index]**. The "magic" is that the index needs to *evaluate to*
a number. So, even if it does not appear to be an integer (e.g. 1, 2, 3), as
long as R can evaluate it, we will get a result. That our expression
`snp_positions[snp_positions > 100000000]` evaluates to a number can be seen
in the following situation. If you wanted to know which **index** (1, 2, 3, or
4\) in our vector of SNP positions was the one that was greater than
100,000,000?

We can use the `which()` function to return the indices of any item that
evaluates as TRUE in our comparison:


```r
which(snp_positions > 100000000)
```

```{.output}
[1] 4
```

**Why this is important**

Often in programming we will not know what inputs
and values will be used when our code is executed. Rather than put in a
pre-determined value (e.g 100000000) we can use an object that can take on
whatever value we need. So for example:


```r
snp_marker_cutoff <- 100000000
snp_positions[snp_positions > snp_marker_cutoff]
```

```{.output}
[1] 154039662
```

Ultimately, it's putting together flexible, reusable code like this that gets
at the "magic" of programming!


::::::::::::::::::::::::::::::::::::::::::::::::::

## A few final vector tricks

Finally, there are a few other common retrieve or replace operations you may
want to know about. First, you can check to see if any of the values of your
vector are missing (i.e. are `NA`, that stands for `not avaliable`). Missing data will get a more detailed treatment later,
but the `is.NA()` function will return a logical vector, with TRUE for any NA
value:


```r
# current value of 'snp_genes':
# chr [1:7] "OXTR" "ACTN3" "AR" "OPRM1" "CYP1A1" NA "APOA5"

is.na(snp_genes)
```

```{.output}
[1] FALSE FALSE FALSE FALSE FALSE FALSE
```

Sometimes, you may wish to find out if a specific value (or several values) is
present a vector. You can do this using the comparison operator `%in%`, which
will return TRUE for any value in your collection that is in
the vector you are searching:


```r
# current value of 'snp_genes':
# chr [1:7] "OXTR" "ACTN3" "AR" "OPRM1" "CYP1A1" NA "APOA5"

# test to see if "ACTN3" or "APO5A" is in the snp_genes vector
# if you are looking for more than one value, you must pass this as a vector

c("ACTN3","APOA5") %in% snp_genes
```

```{.output}
[1] TRUE TRUE
```

:::::::::::::::::::::::::::::::::::::::  challenge

## Review Exercise 1

What data modes are the following vectors?
a. `snps`  
b. `snp_chromosomes`  
c. `snp_positions`

:::::::::::::::  solution

## Solution


```r
mode(snps)
```

```{.output}
[1] "character"
```

```r
mode(snp_chromosomes)
```

```{.output}
[1] "character"
```

```r
mode(snp_positions)
```

```{.output}
[1] "numeric"
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Review Exercise 2

Add the following values to the specified vectors:
a. To the `snps` vector add: "rs662799"  
b. To the `snp_chromosomes` vector add: 11  
c. To the `snp_positions` vector add: 	116792991

:::::::::::::::  solution

## Solution


```r
snps <- c(snps, "rs662799")
snps
```

```{.output}
[1] "rs53576"   "rs1815739" "rs6152"    "rs1799971" "rs662799" 
```

```r
snp_chromosomes <- c(snp_chromosomes, "11") # did you use quotes?
snp_chromosomes
```

```{.output}
[1] "3"  "11" "X"  "6"  "11"
```

```r
snp_positions <- c(snp_positions, 116792991)
snp_positions
```

```{.output}
[1]   8762685  66560624  67545785 154039662 116792991
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Review Exercise 3

Make the following change to the `snp_genes` vector:

Hint: Your vector should look like this in 'Environment':
`chr [1:7] "OXTR" "ACTN3" "AR" "OPRM1" "CYP1A1" NA "APOA5"`. If not
recreate the vector by running this expression:
`snp_genes <- c("OXTR", "ACTN3", "AR", "OPRM1", "CYP1A1", NA, "APOA5")`

a. Create a new version of `snp_genes` that does not contain CYP1A1 and then  
b. Add 2 NA values to the end of `snp_genes`

:::::::::::::::  solution

## Solution


```r
snp_genes <- snp_genes[-5]
snp_genes <- c(snp_genes, NA, NA)
snp_genes
```

```{.output}
[1] "OXTR"  "ACTN3" "AR"    "OPRM1" "APOA5" NA      NA     
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Review Exercise 4

Using indexing, create a new vector named `combined` that contains:

- The the 1st value in `snp_genes`
- The 1st value in `snps`
- The 1st value in `snp_chromosomes`
- The 1st value in `snp_positions`

:::::::::::::::  solution

## Solution


```r
combined <- c(snp_genes[1], snps[1], snp_chromosomes[1], snp_positions[1])
combined
```

```{.output}
[1] "OXTR"    "rs53576" "3"       "8762685"
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Review Exercise 5

What type of data is `combined`?

:::::::::::::::  solution

## Solution


```r
typeof(combined)
```

```{.output}
[1] "character"
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::  callout

## Lists

Lists are quite useful in R, but we won't be using them in the genomics lessons.
That said, you may come across lists in the way that some bioinformatics
programs may store and/or return data to you. One of the key attributes of a
list is that, unlike a vector, a list may contain data of more than one mode.
Learn more about creating and using lists using this [nice
tutorial](https://r4ds.had.co.nz/vectors.html#lists). In this one example, we will create
a named list and show you how to retrieve items from the list.


```r
# Create a named list using the 'list' function and our SNP examples
# Note, for easy reading we have placed each item in the list on a separate line
# Nothing special about this, you can do this for any multiline commands
# To run this command, make sure the entire command (all 4 lines) are highlighted
# before running
# Note also, as we are doing all this inside the list() function use of the
# '=' sign is good style
snp_data <- list(genes = snp_genes,
                 refference_snp = snps,
                 chromosome = snp_chromosomes,
                 position = snp_positions)
# Examine the structure of the list
str(snp_data)
```

```{.output}
List of 4
 $ genes         : chr [1:7] "OXTR" "ACTN3" "AR" "OPRM1" ...
 $ refference_snp: chr [1:5] "rs53576" "rs1815739" "rs6152" "rs1799971" ...
 $ chromosome    : chr [1:5] "3" "11" "X" "6" ...
 $ position      : num [1:5] 8.76e+06 6.66e+07 6.75e+07 1.54e+08 1.17e+08
```

To get all the values for the `position` object in the list, we use the `$` notation:


```r
# return all the values of position object

snp_data$position
```

```{.output}
[1]   8762685  66560624  67545785 154039662 116792991
```

To get the first value in the `position` object, use the `[]` notation to index:


```r
# return first value of the position object

snp_data$position[1]
```

```{.output}
[1] 8762685
```
:::::::::::::::::::::::::::::::::::::::::




:::::::::::::::::::::::::::::::::::::::: keypoints

- Working with vectors effectively prepares you for understanding how data are organized in R.

::::::::::::::::::::::::::::::::::::::::::::::::::








