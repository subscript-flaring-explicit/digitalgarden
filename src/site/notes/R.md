---
{"dg-publish":true,"dg-permalink":"programming/r","permalink":"/programming/r/","dgHomeLink":false,"dgPassFrontmatter":false}
---


# Variables

-   assign variables `<-`
    -   x equals 42
        -   `x <- 42`
    -   add variables
        -   `x <- a + b`
            -   a and b have to be numbers, otherwise there will be an error `non-numeric argument to binary operator`
-   Basic data types
        #R/datatypes
	-   Decimal values like `4.5` are called **numerics**
	-   Whole numbers like `4` are called **integers**. Integers are also numerics.
	-   Boolean values ( `TRUE` or `FALSE` ) are called **logical**.
	-   Text (or string) values are called **characters**.

- basic operations
	- modulo
		- remainder of division
		- symbol: `%%`
		- example: `28 %% 6 = 4`

---

# Vectors

-   creating a vector
        #R/datatypes  
	-   `c()` function
		-   example: `c(a,b,c)`
-   naming vectors
	-   `names()`
		-   `names(some_vector) <- c("Name", "Profession")`
			-   print
				-   ```Name     Profession 
				"John Doe" "poker player"```
	-   names of other vector can be also assigned to a different vector at the same time
		-   `names(roulette_vector) <- names(poker_vector)`

## operations on vectors
-   sum vectors
	-   `c(1, 2, 3) + c(4, 5, 6)`
		-   `sum()`
                -   It calculates the sum of all elements of a vector
-  average of all elements in the vector
	  - `mean()` 
		  - [https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/mean](https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/mean)
-   logical
	-   check if vector_one is greater than vector_two
		-   `vector_one > vector_two`
		-   it will print either `TRUE` or `FALSE`

## vector selection
-   single element
	-   ```poker_vector[1] ## it will print out first element of the vector```
                -   first element has index 1!
-   slicing
	- single elements
		-   `poker selection[c(1,5)]`
		  - the first and fifth element of `poker_vector`
	- range of elements
			- `poker_selection[2:4]` -> select element from 2 to 4
				-   the same as `poker_selection[c(2,3,4)]`
	- based on criteria
		- greater than 0
			- step 1. - create selection vector
				- `selection_vector <- poker_vector > 0`
			- step 2. subset the original vector with selection vector
				- `poker_winning_days <- poker_vector[selection_vector]`

---

# Matrix
#R/datatypes 
## description
- In R, a matrix is a collection of **elements of the same data type** (numeric, character, or logical) arranged **into a fixed number of rows and columns**

## function
- `matrix()` function
	- `matrix(1:9, byrow = TRUE, nrow = 3)`
		- first element (1:9) -> **values**, collection of elements that R will arrange into the rows and columns of the matrix
		- `byrow` indicates that the matrix is filled by the rows, alternatively you can use `byrow = FALSE`
		- The third argument `nrow` indicates that the matrix should have three rows.
## columns
- column names
	- change column names
		- `colnames(matrix)`
- column values
	- add column
		- `cbind()`
			- example:
			  `cbind(matrix1, matrix2, column1)`
			- function which merges matrices and/or vectors together by column
			- remember -> `column bind`
	- sum of values in all columns
		- `colSums(matrix)`

## rows
- row names
	- change row names
		- `rownames(matrix)`
- sums of values in all rows
	- `rowSums(matrix)`
- adding columns
	- `rbind()`
		- example:
		  rbind(matrix1, matrix2, row1)
		- remember: row bind

## slicing
- by row and column number
	- `matrix[1:2, 3:4]`
- only by column
	- `matrix[,2]`
- only by row
	- `matrix[2,]`

## operations
- multiply values
	- `matrix * 2`
- divide matrices
	- `visitors <- all_wars_matrix/ticket_prices_matrix`
		- every value in `all_wars_matrix` will be divided by values in `ticket_prices_matrix`


---

# Factors
#R/datatypes

## definition
- term factor refers to a statistical data type used to store categorical variables
	- difference between a categorical variable and a continuous variable is that a categorical variable can belong to a **limited number of categories**
	- example of categorical variable: sex -> either Male or Female

## use
- `factor()` function
	- `factor(temperature_vector, order = TRUE, levels = c("Low", "Medium", "High")`
		- levels can also be defined later using `levels()` function -> see [[#levels]]
	- when characters type is passed, R uses alphabetical order A to Z
- steps
	1. create a vector that contains all the observations that belong to a limited number of categories
		- `sex_vector <- c("Male","Female","Female","Male","Male")`
			- there are two **factor levels** - Male and Female
	1. pass values of a factor vector using `factor()` function
		- `factor_sex_vector <- factor(sex_vector)`

## levels
- `levels(factor_vector) <- c("name1", "name2",...)`
- function can also be used to ==remap== levels -> `F, M` becomes `Female, Male`
	- >! be careful about the order with which the original levels occur
		- usually the order is alphabetical, so `F, M`



---

# data frame
- get summary of the data
	- `summary()`
- function [`head()`](http://www.rdocumentation.org/packages/utils/functions/head) enables you to show the first observations of a data frame. 
- function [`tail()`](http://www.rdocumentation.org/packages/utils/functions/head) prints out the last observations in your dataset.
- function [`str()`](http://www.rdocumentation.org/packages/utils/functions/str) shows you the structure of your dataset
	- output
		- variable name
		- variable type
		- variable values

## creating dataframe
- construct a data frame with the [`data.frame()`](https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/data.frame) function
	- As arguments, you pass the vectors from before: they will become the different columns of your data frame

## slicing dataframe
- `planets_df[rings_vector, ]`
	- select rows of `planets_df` and all columns
- [`subset()`](http://www.rdocumentation.org/packages/base/functions/subset) function
	- `subset(my_df, subset = some_condition)`
		- my_df = dataset for which you want a subset
		- some_condition = necessary information and conditions to select the correct subset
		- example
			- `subset(planets_df, subset = rings)`
			- `subset(planets_df, subset = diameter < 1)`

## create dataframe from file

### CSV to dataframe
1. Set or change the working directory
	- `getwd()`
		- returns an absolute file-path representing the current working directory of the R process
	- `setwd(dir)`
		- set the working directory to `dir`
2. Read the CSV file
	- `read.csv(file, header = TRUE, sep = “,”, quote = “\””, dec = “.”, fill = TRUE, comment.char = “”, …)`
		-   _**file:**_ the name of the file which the data are to be read from. (includes file format `.csv`)
		-   _**header:**_ a logical value indicating whether the file contains the names of the variables as its first line. If missing, the value is determined from the file format: header is set to TRUE if and only if the first row contains one fewer field than the number of columns.
		-   _**sep:**_ the field separator character. Values on each line of the file are separated by this character. If sep = “” (the default for read.table) the separator is ‘white space’, that is one or more spaces, tabs, newlines or carriage returns.
		-   _**quote:**_ the set of quoting characters.
		-   _**dec:**_ the character used in the file for decimal points.
		-   _**fill:**_ logical. If TRUE then in case the rows have unequal length, blank fields are implicitly added.
		-   _**comment.char:**_ character: a character vector of length one containing a single character or an empty string.
		-   _**… :**_  Further arguments to be passed.
	- example
		```R
		sdata <- read.csv("SampleData.csv", header = TRUE, sep = ",")
		```
	- useful commands

#### useful functions
- `View(dataframe)`
	- view dataframe formed with .csv file
- ``subset()`
	- `subset(sdata, sdata$speed == max(sdata$speed))`
		- 


## Select columns
- `planets_df$diameter` - select `diameter` column in `planets_df`

## Sorting data

- [`order()`](http://www.rdocumentation.org/packages/base/functions/order) is a function that gives you the ranked position of each element when it is applied on a variable
	- prints the order of values in a dataset
		- can be consequently used to reshuffle values in a dataset
		- ## Examples
			- `a` -> values with no order
			- `a[order(a)]` -> values in order
			- `planets_df[positions, ]`
				- where: `positions <- order(planets_df$diameter)`


---

# Summary

- vectors
	- one dimensional array
	- numeric, character or logical values

- matrices
	- two dimensional array
	- numeric, character or logical values
	- elements all have ==the same data type==.

- data frames
	- two-dimensional objects
	- numeric, character or logical values
	- Within a column all elements have the same data type, but different ==columns can be of different data type==.

---

# List

- can gather variety of objects under one name
- ordered way
- these objects can be turnt into matrices, vectors, dataframes or even other lists
- you could say it is super data type -> can store any piece of information

## creating

- `list()` function

- `my_list <- list(comp1, comp2)`
	- elements in the list are called its ==components==
	- components can be of type \`matrices, vectors, lists, dataframe\` types

- you can use custom names for the lists using vector
	```R
	
	my_list <- list(your_comp1, your_comp2)
	
	names(my_list) <- c("name1", "name2")
	
	```

## creating a names list
- `shining_list <- list(moviename = mov, actors = act, reviews = rev)`

## selecting elements from a list
- use either `[[ ]]` or `$`
	- `shining_list[["reviews"]]`
	- `shining_list$reviews`
		- short name (one given with [[#creating a names list]]) or full name

---

# Relational operators

## Equality
- equality `==`
	- `TRUE == TRUE` -> TRUE
	- `"hello" == "goodbye"` -> FALSE
	- `3 == 2` -> FALSE
	- `TRUE == 1` -> TRUE

## Inequality
- inequality operator `!=`
	- `"hello" != "goodbye"` -> TRUE
	- `3 != 2` -> TRUE
- `<` and `>`
	- `3 > 5`
		- FALSE
	- `3 < 5`
		- TRUE
	- `"Hello" > "Goodbye"`
		- TRUE
		- because of the alphabetical order, H comes before G
- `<=` and `>=`
	- `3 >= 5`
		- FALSE
	- `3 <= 5`
		- TRUE

## comparison for vectors
- comparison is made by comparing every single element to the other

Example
- `facebook <- c(1,2,3,4)`
- `linkedin <- c(4,3,2,1)`
- compare
	- `facebook >= linkedin`
	- `FALSE, FALSE, TRUE, TRUE`

## Logical operators
- ⚠️logical operators can be used on vectors⚠️

### AND operator `&`
- logical conjunction
- `x > 5 & x < 15`

### OR operator `|`
- one logical value should equal `TRUE` to the operation to equal `TRUE`
- `FALSE | TRUE` -> TRUE
- `TRUE | TRUE` -> TRUE

### NOT operator `!`
- `!TRUE` -> FALSE
- `!FALSE` -> TRUE
- `!(x>5)` -> `x <= 5`

### Double sign operators `&&` and `||`
- `&` vs `&&`
	- `&&` only compares the first elements in the matrix
- `|` vs `||`
	- `||` only compares the first elements in the matrix

### Evauluate how many `TRUE` are in a matrix
- use `sum()` function, using the knowledge that
	-  `TRUE == 1` -> TRUE - see [[#Equality]]

---

# Conditional statements

## If statement
- needs explicit condition
```R
if(condition) {
	expression
}
```

- example:
```R
if(x < 0) {
	print("x is a negative number")
}
```

## Else statement
- does not need explicit condition

```R
if(condition) {
	expression1
} else {
	expression2
}
```


## Else if statement
- multiple ifs
- `else if` keyword
```R
if(condition) {
	expression1
} else if(condition2) {
	expression2
} else {
	expression3
}
```

## While loop
- similar to if statement
- code will be executed as long as the condition is TRUE
	```R
	while(condition) {
		expression1
	}
	```

- increment values
	```R
	while(ctr <= 7) {
		print(paste("ctr is set to", ctr))
		ctr <- ctr + 1
	}
	```

- `break` statement
	- breaks the loop from executing
	```R
	while(ctr <= 7) {
		if(ctr %% 5 == 0) {
			break
		}
		print(paste("ctr is set to", ctr))
		ctr <- ctr + 1
	}
	```

- example use of `break`
	```R
	# Initialize the speed variable
	speed <- 88
	
	while (speed > 30) {
	  print(paste("Your speed is", speed))
	  
	  # Break the while loop when speed exceeds 80
	  if (speed > 80) {
	    break
	  }
	  
	  if (speed > 48) {
	    print("Slow down big time!")
	    speed <- speed - 11
	  } else {
	    print("Slow down!")
	    speed <- speed - 6
	  }
	}
	```



## For loop
- run code for every element in a "list" of elements
	- repeats itself until all elements are iterated over
- basic structure of for loop
	```R
	for(var in seq) {
		expression
	}
	```
- example of for loop
	```R
	cities <- c("New York", "Paris", "London", "Tokyo", "Rio de Janeiro", "Cape Town")
	
	for(city in cities) {
		print(city)
	}
	```
- `break` statement in a for loop
	```R
		cities <- c("New York", "Paris", "London", "Tokyo", "Rio de Janeiro", "Cape Town")
		
		for(city in cities) {
			if(nchar(city) == 6) {
				break
			}
			print(city)
		}
	```
- `next` statement in a for loop
	- skips the element that matches the condition
	```R
			cities <- c("New York", "Paris", "London", "Tokyo", "Rio de Janeiro", "Cape Town")
			
			for(city in cities) {
				if(nchar(city) == 6) {
					skip
				}
				print(city)
			}
	```
- iterate over index
	- ⚠️when looping over a list you need a double square brackets⚠️
		- `print(primes_list[[i]])`
```R
for(i in 1:length(cities)) {
	print(paste(cities[i], "is on position", i, "in the cities vector."))

```

## Loop over a matrix
- also called nested loop
```R
for (var1 in seq1) {
  for (var2 in seq2) {
    expr
  }
}
```

- given a matrix `ttt`
	- iterate over rows with `1:nrow(ttt)`
	- iterate over columns with `1:ncol(ttt)`

- print content and position of every cell in a matrix
```R
# define the double for loop
for (x in 1:nrow(ttt)) {
  for (y in 1:ncol(ttt)) {
    print(paste("On row", x, "and column", y, "the board contains", ttt[x,y]))
  }
}
```

---

# Functions

- ## docs on function
	- `help(function_name)`
	- `?function_name`

- args()
	- tells me what arguments a function wants, what values are default

- black box principle
	- input -> black box -> output
	- c(1,5,6,7) -> sd() -> 2.629956

## assign function
- functions are assigned the same way variables are in R
	- `sd_of_sample <- sd(sample)`

## [`strsplit()`](https://www.rdocumentation.org/packages/base/functions/strsplit) function
- split up into a vector that contains separate letters

## `sd(x, na.rm = FALSE)`
- argument matching
- `na.rm`
	- should N/A values be removed?
	- logical value
		- TRUE/FALSE

## list() function

## print() function

## mean(x, trim, na.rm) function
- average of `x`
	- you can calculate average element-wise for two or more vectors using `x = vector1 + vector2`
- `trim`
	- it chops off a fraction (equal to `trim`) of the vector you pass as argument `x`

- `abs(x)` function
	- absolute value of `x`

# Functions inside functions

- basic example
	```R
	speed <- 31
	print(paste("Your speed is", speed))
	```


# Writing your own functions

- example - in `arg1`, `arg2` out - `return` or last value
```R
my_fun <- function(arg1, arg2) {
	body
}
```

- example 2 - `return` keyword
```R
triple <- function(x) {
	y <- 3*x
	return(y)
}
```


