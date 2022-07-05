---
{"dg-publish":true,"dg-permalink":"programming/r","permalink":"/programming/r/","dgHomeLink":true,"dgPassFrontmatter":false}
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
		- levels can also be defined later using `levels()` function -> see [[R#levels|#levels]]
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
		- usually the order is alphabetical, so F, M



---

# Other

-   #R 
    -   remainder of division
        -   modulo operator - `%%`
            -   `28 %% 6 = 4`

---