# R language preparation for data analysis and visualization

## Types of basic data types in R

### 1. Numeric

```R
x <- 1
```

### 2. Character

```R
x <- "Hello"
```

### 3. Logical

```R
x <- TRUE
```

### 4. Integer

```R
x <- 1L
```

### 5. Complex

```R
x <- 1 + 2i
```

### 6. Raw

```R
x <- charToRaw("Hello")
# [1] 48 65 6c 6c 6f
```

## Data structures in R

### 1. Vector

- A vector is a collection of elements of the same type.

```R
x <- c(1, 2, 3, 4, 5)
# [1] 1 2 3 4 5
```

### 2. Matrix

- A matrix is a collection of elements of the same type arranged into a fixed number of rows and columns.

```R
x <- matrix(1:9, nrow = 3, ncol = 3)
#      [,1] [,2] [,3]
# [1,]    1    4    7
# [2,]    2    5    8
# [3,]    3    6    9
```

### 3. Array

- An array is a collection of elements of the same type arranged into a fixed number of dimensions.

```R
x <- array(1:12, dim = c(2, 3, 2))
# , , 1
#      [,1] [,2] [,3]
# [1,]    1    3    5
# [2,]    2    4    6
# , , 2
#      [,1] [,2] [,3]
# [1,]    7    9   11
# [2,]    8   10   12
```

### 4. List

- A list is a collection of elements of different types.

```R
x <- list(1:5, "Hello", TRUE)
# [[1]]
# [1] 1 2 3 4 5
#
# [[2]]
# [1] "Hello"
#
# [[3]]
# [1] TRUE
```

### 5. Data frame

- A data frame is a collection of elements of different types arranged into rows and columns.

```R
x <- data.frame(a = 1:3, b = c("A", "B", "C"))
#   a b
# 1 1 A
# 2 2 B
# 3 3 C
```

### 6. Factor

- A factor is a vector that represents categorical data.

```R
x <- factor(c("A", "B", "A", "C", "B"))
# [1] A B A C B
# Levels: A B C
```

## Control structures in R

### 1. If-else

```R
x <- 5
if (x > 0) {
  print("Positive")
} else {
  print("Negative")
}
# [1] "Positive"
```

### 2. For loop

```R
for (i in 1:5) {
  print(i)
}
# [1] 1
# [1] 2
# [1] 3
# [1] 4
# [1] 5
```

### 3. While loop

```R
x <- 1
while (x <= 5) {
  print(x)
  x <- x + 1
}
# [1] 1
# [1] 2
# [1] 3
# [1] 4
# [1] 5
```

### 4. Repeat loop

```R
x <- 1
repeat {
  print(x)
  x <- x + 1
  if (x > 5) {
    break
  }
}
# [1] 1
# [1] 2
# [1] 3
# [1] 4
# [1] 5
```

### 5. Break statement

```R
for (i in 1:5) {
  if (i == 3) {
    break
  }
  print(i)
}
# [1] 1
# [1] 2
```

### 6. Next statement

- The next statement is used to skip the current iteration of a loop. 

```R
for (i in 1:5) {
  if (i == 3) {
    next
  }
  print(i)
}
# [1] 1
# [1] 2
# [1] 4
# [1] 5
```

## Functions in R

### 1. Function definition

```R
add <- function(x, y) {
  return(x + y)
}
```

### 2. Function call

```R
add(2, 3)
# [1] 5
```

### 3. Function with default arguments

```R
add <- function(x, y = 1) {
  return(x + y)
}
```

### 4. Function with variable number of arguments

```R
add <- function(...) {
  args <- list(...)
  return(sum(args))
}
```

### 5. Function with named arguments

```R
add <- function(x, y) {
  return(x + y)
}
add(y = 3, x = 2)
# [1] 5
```

## Packages in R

- A package is a collection of functions, data sets, and documentation that extends the capabilities of base R.

### 1. Installing a package

```R
install.packages("ggplot2")
```

### 2. Loading a package

```R
library(ggplot2)
```

### 3. Using a function from a package

```R
ggplot(data = mtcars, aes(x = mpg, y = wt)) + geom_point()
```

## Merging data in R

### 1. Merging data frames by rows

```R
df1 <- data.frame(a = 1:3, b = c("A", "B", "C"))
df2 <- data.frame(a = 4:6, b = c("D", "E", "F"))
df3 <- rbind(df1, df2)
#   a b
# 1 1 A
# 2 2 B
# 3 3 C
# 4 4 D
# 5 5 E
# 6 6 F
```

### 2. Merging data frames by columns

```R
df1 <- data.frame(a = 1:3, b = c("A", "B", "C"))
df2 <- data.frame(c = 4:6, d = c("D", "E", "F"))
df3 <- cbind(df1, df2)
#   a b c d
# 1 1 A 4 D
# 2 2 B 5 E
# 3 3 C 6 F
```

### 3. Merging data frames by common columns

```R
df1 <- data.frame(a = 1:3, b = c("A", "B", "C"))
df2 <- data.frame(a = 2:4, c = c("D", "E", "F"))
df3 <- merge(df1, df2, by = "a")
#   a b c
# 1 2 B D
# 2 3 C E
```

## Reading and writing data in R

### 1. Reading data from a CSV file

```R
df <- read.csv("data.csv")
```

### 2. Writing data to a CSV file

```R
write.csv(df, "data.csv", row.names = FALSE)
```

### 3. Reading data from an Excel file

```R
library(readxl)
df <- read_excel("data.xlsx")
```

### 4. Writing data to an Excel file

```R
library(writexl)
write_xlsx(df, "data.xlsx")
```

## Adding a new column to a data frame in R

```R
df <- data.frame(a = 1:3, b = c("A", "B", "C"))
df$c <- c("X", "Y", "Z")

df[["d"]] <- c("P", "Q", "R")

df <- cbind(df, e = c("M", "N", "O"))

df <- transform(df, f = c("G", "H", "I"))

df <- within(df, g <- c("J", "K", "L"))

df <- data.frame(df, h = c("S", "T", "U"))

df <- df %>% mutate(i = c("V", "W", "X"))

df <- df %>% add_column(j = c("Y", "Z", "A"))

df <- df %>% bind_cols(k = c("B", "C", "D"))
```

## Removing a column from a data frame in R

```R
df <- data.frame(a = 1:3, b = c("A", "B", "C"), c = c("X", "Y", "Z"))

df$c <- NULL

df <- select(df, -c)

df <- df %>% select(-c)

df <- df[, -which(names(df) == "c")]

df <- subset(df, select = -c)
```

## Assigning values to a variable in R

```R

# Assignment operator
x <- 5
# [1] 5

# Right assignment operator
5 -> x
# [1] 5

# Left assignment operator
x <- 5 -> y
# x = 5
# y = 5

# Assigning multiple values
x <- y <- 5
# x = 5
# y = 5

# Assigning value using = operator

x = 5
# [1] 5

# global assignment operators, <<- and ->>

x <<- 5
# [1] 5

5 ->> x
# [1] 5
# global assignment operators are used to assign values to variables in the global environment.

```

## Aggregating data in R

### 1. Summarizing data by group

```R
df <- data.frame(group = c("A", "B", "A", "B"), value = c(1, 2, 3, 4))
summary <- aggregate(value ~ group, data = df, FUN = sum)
#   group value
# 1     A     4
# 2     B     6
```

### 2. Summarizing data by multiple groups

```R
df <- data.frame(group1 = c("A", "B", "A", "B"), group2 = c("X", "Y", "X", "Y"), value = c(1, 2, 3, 4))
summary <- aggregate(value ~ group1 + group2, data = df, FUN = sum)
#   group1 group2 value
# 1      A      X     4
# 2      B      Y     6
```

### 3. Summarizing data by group using dplyr

```R
library(dplyr)
df <- data.frame(group = c("A", "B", "A", "B"), value = c(1, 2, 3, 4))
summary <- df %>% group_by(group) %>% summarise(value = sum(value))
# # A tibble: 2 x 2
#   group value
#   <chr> <dbl>
# 1 A         4
# 2 B         6
```

## Joining data in R

### 1. Inner join

```R
df1 <- data.frame(a = 1:3, b = c("A", "B", "C"))
df2 <- data.frame(a = 2:4, c = c("D", "E", "F"))
df3 <- inner_join(df1, df2, by = "a")
#   a b c
# 1 2 B D
# 2 3 C E
```

### 2. Left join

```R
df1 <- data.frame(a = 1:3, b = c("A", "B", "C"))
df2 <- data.frame(a = 2:4, c = c("D", "E", "F"))
df3 <- left_join(df1, df2, by = "a")
#   a b    c
# 1 1 A <NA>
# 2 2 B    D
# 3 3 C    E
```

### 3. Right join

```R
df1 <- data.frame(a = 1:3, b = c("A", "B", "C"))
df2 <- data.frame(a = 2:4, c = c("D", "E", "F"))
df3 <- right_join(df1, df2, by = "a")
#   a    b c
# 1 2    B D
# 2 3    C E
# 3 4 <NA> F
```

### 4. Full join

```R
df1 <- data.frame(a = 1:3, b = c("A", "B", "C"))
df2 <- data.frame(a = 2:4, c = c("D", "E", "F"))
df3 <- full_join(df1, df2, by = "a")
#   a    b    c
# 1 1    A <NA>
# 2 2    B    D
# 3 3    C    E
# 4 4 <NA>    F
```

### 5. Merge join

```R
df1 <- data.frame(a = 1:3, b = c("A", "B", "C"))
df2 <- data.frame(a = 2:4, c = c("D", "E", "F"))
df3 <- merge(df1, df2, by = "a", all = TRUE)
#   a    b    c
# 1 1    A <NA>
# 2 2    B    D
# 3 3    C    E
# 4 4 <NA>    F
```

- merge() function is used to merge two data frames by common columns. The all argument is set to TRUE to perform a full join. The by argument specifies the common column to merge on. merge() function can act as an inner, left, right, or full join based on the all argument. 
- the arguments are all, all.x, all.y, by, by.x, by.y, suffixes, and sort. 

```R
# Regular join (inner join)
df3 <- merge(df1, df2, by = "a")

# Left join
df3 <- merge(df1, df2, by = "a", all.x = TRUE)

# Right join
df3 <- merge(df1, df2, by = "a", all.y = TRUE)

# Full join
df3 <- merge(df1, df2, by = "a", all = TRUE)

# Join on multiple columns
df3 <- merge(df1, df2, by = c("a", "b"))

# Custom suffixes for duplicate columns
df3 <- merge(df1, df2, by = "a", suffixes = c("_df1", "_df2"))

# Sort the result by a column
df3 <- merge(df1, df2, by = "a", sort = TRUE)
```

## How to chain several operations together in R?

- The pipe operator `%>%` is used to chain several operations together in R. It is part of the magrittr package and is used to pass the result of one function to the next function as an argument. 

```R
library(dplyr)

df <- data.frame(a = 1:3, b = c("A", "B", "C"))

df <- df %>% mutate(c = a + 1) %>% filter(c > 2) %>% select(a, b)

# The above code is equivalent to the following code:

df <- select(filter(mutate(df, c = a + 1), c > 2), a, b)

# The pipe operator can be used with any function that takes the data frame as the first argument. 

df <- df %>% group_by(b) %>% summarise(mean(a))

# The pipe operator can also be used with user-defined functions.

add_one <- function(x) {
  return(x + 1)
}

df <- df %>% mutate(c = add_one(a))

# The pipe operator can be used to chain multiple operations together in a single line of code, making the code more readable and concise.
```

## What types of data plots can be created in R?

Being data visualization one of the strong sides of the R programming languages, we can create all types of data plots in R:
In R, you can create various types of data plots for visualization purposes. Some common types of data plots include:

- Bar plot: Use the `barplot()` function to display numerical values of categorical data. )
- Line plot: Use the `plot()` function to show the progression of a variable over time.
- Scatter plot: Use the `plot()` function with two variables to visualize their relationship.
- Area plot: Use the `plot()` function with the `type = "area"` argument to create an area plot.
- Pie chart: Use the `pie()` function to represent the proportion of each category in categorical data.
- Box plot: Use the `boxplot()` function to display the distribution and summary statistics of a dataset.

For more advanced data plots, you can consider:

- Violin plot: Use the `vioplot()` function to show the distribution shape and summary statistics.
- Heatmap: Use the `heatmap()` function to visualize the magnitude of numeric data points.
- Treemap: Use the `treemap()` function to display numerical values of categorical data as part of a whole.
- Dendrogram: Use the `plot()` function with hierarchical clustering algorithms to show data hierarchy.
- Bubble plot: Use the `plot()` function with three variables to represent relationships.
- Hexbin plot: Use the `hexbinplot()` function to visualize relationships in large datasets.
- Word cloud: Use the `wordcloud()` function to display word frequencies in a text.
- Choropleth map: Use the `choroplethr` package to create thematic maps based on geospatial data.
- Circular packing chart: Use the `circlize` package to visualize hierarchical data in a circular layout.

Remember to install and load any required packages before using their functions.

## What is vector recycling in R?

- Vector recycling is a feature in R that allows you to perform operations on vectors of different lengths. When you perform an operation on two vectors of different lengths, R automatically recycles the shorter vector to match the length of the longer vector. This recycling process repeats the shorter vector until it matches the length of the longer vector.

```R
# Example of vector recycling in R
x <- c(1, 2, 3)
y <- c(4, 5)

# When adding two vectors of different lengths, R recycles the shorter vector
z <- x + y
# [1] 5 7 7

# The shorter vector y is recycled to match the length of the longer vector x
# The recycling process repeats the shorter vector y as follows:
# 4 5 4
# 1 2 3
# -----
# 5 7 7

# Vector recycling is a useful feature in R that simplifies operations on vectors of different lengths.
```

## What is the difference between the `==` and `===` operators in R?

- In R, the `==` operator is used for value equality comparison, while the `===` operator is used for object identity comparison. The `==` operator checks if the values of two objects are equal, while the `===` operator checks if the two objects are the same object in memory.

```R
# Example of the == operator in R
x <- 5
y <- 5
x == y
# [1] TRUE

# The == operator checks if the values of x and y are equal

# Example of the === operator in R
x <- 5
y <- 5
x === y
# [1] FALSE

# The === operator checks if x and y are the same object in memory

# The === operator is not available in base R, but you can use the identical() function to achieve the same result

identical(x, y)

# The identical() function checks if two objects are exactly the same, including their attributes and memory location.
```


## How to create a new column in a data frame in R based on other columns?

- You can create a new column in a data frame in R based on other columns using the `$` operator, the `transform()` function, or the `mutate()` function from the `dplyr` package.


### transform() function
```R
df <- data.frame(col_1 = c(1, 3, 5, 7),  col_2 = c(8, 6, 4, 2))
print(df)
​
# Adding the column col_3 to the data frame df
df <- transform(df, col_3 = ifelse(col_1 < col_2, col_1 + col_2, col_1 * col_2))
print(df)

'''
col_1 col_2
1     1     8
2     3     6
3     5     4
4     7     2
  col_1 col_2 col_3
1     1     8     9
2     3     6     9
3     5     4    20
4     7     2    14
'''

# The transform() function creates a new column col_3 in the data frame df based on the values of col_1 and col_2.

# Using the mutate() function from the dplyr package
library(dplyr)
df <- data.frame(col_1 = c(1, 3, 5, 7), col_2 = c(8, 6, 4, 2))
print(df)

# Adding the column col_3 to the data frame df
df <- df %>% mutate(col_3 = ifelse(col_1 < col_2, col_1 + col_2, col_1 * col_2))
print(df)

'''
col_1 col_2 col_3
1     1     8     9
2     3     6     9
3     5     4    20
4     7     2    14
'''

# The mutate() function from the dplyr package is used to create a new column col_3 in the data frame df based on the values of col_1 and col_2.



#using the with() function to create a new column based on other columns in a data frame in R.

df <- data.frame(col_1 = c(1, 3, 5, 7), col_2 = c(8, 6, 4, 2))
print(df)

# Adding the column col_3 to the data frame df
df$col_3 <- with(df, ifelse(col_1 < col_2, col_1 + col_2, col_1 * col_2))
print(df)

'''
col_1 col_2 col_3
1     1     8     9
2     3     6     9
3     5     4    20
4     7     2    14
'''

# The with() function is used to create a new column col_3 in the data frame df based on the values of col_1 and col_2.

### Using the apply() function

df <- data.frame(col_1 = c(1, 3, 5, 7), col_2 = c(8, 6, 4, 2))
print(df)

# Adding the column col_3 to the data frame df
df$col_3 <- apply(df, 1, function(x) ifelse(x[1] < x[2], x[1] + x[2], x[1] * x[2]))
print(df)

'''
col_1 col_2 col_3
1     1     8     9
2     3     6     9
3     5     4    20
4     7     2    14
'''

# The apply() function is used to apply a function to each row of the data frame df. In this case, the function checks if col_1 is less than col_2 and calculates the value of col_3 accordingly.

```

## What is the use of the switch() function in R?

- The `switch()` function in R is used to select one of several alternatives based on a specified condition. It is similar to a series of `if-else` statements but is more concise and easier to read when there are multiple conditions to check.

```R

# Example of the switch() function in R

# Using the switch() function to select a day of the week based on a numeric value
day_number <- 3
day <- switch(day_number,
              "Sunday",
              "Monday",
              "Tuesday",
              "Wednesday",
              "Thursday",
              "Friday",
              "Saturday")
print(day)
# [1] "Tuesday"

# The switch() function selects the day of the week based on the value of day_number

'''
If the expression evaluates to a number, the switch() function returns the item from the list based on positional matching (i.e., its index is equal to the number the expression evaluates to). If the number is greater than the number of items in the list, the switch() function returns NULL.
'''

# Using the switch() function with a default value
day_number <- 8
day <- switch(day_number,
              "Sunday",
              "Monday",
              "Tuesday",
              "Wednesday",
              "Thursday",
              "Friday",
              "Saturday",
              "Invalid day")
print(day)
# [1] "Invalid day"

# If the expression evaluates to a character string, the switch() function returns the value based on its name:

day_name <- "Wednesday"
day_number <- switch(day_name,
                     "Sunday" = 1,
                     "Monday" = 2,
                     "Tuesday" = 3,
                     "Wednesday" = 4,
                     "Thursday" = 5,
                     "Friday" = 6,
                     "Saturday" = 7)
print(day_number)
# [1] 4

# The switch() function is a useful tool for selecting one of several alternatives based on a specified condition in R.

```

## What is the difference between the functions apply(), lapply(), sapply(), and tapply()?

- In R, the `apply()`, `lapply()`, `sapply()`, and `tapply()` functions are used to apply a function to elements of a list, vector, or data frame. Each function has specific characteristics and is used for different purposes.

### apply() function

- The `apply()` function is used to apply a function to the rows or columns of a matrix or data frame. It is a more general version of the `lapply()` function and can be used with arrays and matrices.

```R
# Example of the apply() function in R
matrix_data <- matrix(1:9, nrow = 3, ncol = 3)
print(matrix_data)

# Applying the sum function to the rows of the matrix
row_sums <- apply(matrix_data, 1, sum)
print(row_sums)
# [1] 12 15 18

# Applying the mean function to the columns of the matrix
col_means <- apply(matrix_data, 2, mean)
print(col_means)
# [1] 2 5 8
```

### lapply() function

- The `lapply()` function is used to apply a function to each element of a list or vector. It returns a list as output, with each element corresponding to the result of applying the function to the corresponding element of the input list or vector.

```R
# Example of the lapply() function in R
list_data <- list(a = 1:3, b = 4:6, c = 7:9)
print(list_data)

# Applying the sum function to each element of the list
sum_list <- lapply(list_data, sum)
print(sum_list)
# $a
# [1] 6
#
# $b
# [1] 15
#
# $c
# [1] 24
```

### sapply() function

- The `sapply()` function is a simplified version of the `lapply()` function that returns a vector or matrix as output instead of a list. It tries to simplify the output to the most appropriate data structure.

```R
# Example of the sapply() function in R
list_data <- list(a = 1:3, b = 4:6, c = 7:9)
print(list_data)

# Applying the sum function to each element of the list
sum_vector <- sapply(list_data, sum)
print(sum_vector)
# a  b  c
# 6 15 24
```

### tapply() function

- The `tapply()` function is used to apply a function to subsets of a vector or data frame split by one or more factors. It is used for applying functions to groups of data based on a factor variable.

```R
# Example of the tapply() function in R
data <- data.frame(group = c("A", "B", "A", "B"), value = c(1, 2, 3, 4))
print(data)

# Applying the sum function to the values grouped by the group variable
sum_by_group <- tapply(data$value, data$group, sum)
print(sum_by_group)

# A B
# 4 6
```

- In summary, the `apply()` function is used for applying a function to rows or columns of a matrix or data frame, the `lapply()` function is used for applying a function to each element of a list or vector, the `sapply()` function is a simplified version of `lapply()` that returns a vector or matrix, and the `tapply()` function is used for applying a function to subsets of data based on a factor variable.

## What packages are used for machine learning in R?

- **caret—for** -  various classification and regression algorithms.
- **e1071—for** -  support vector machines (SVM), naive Bayes classifier, bagged clustering, fuzzy clustering, and k-nearest neighbors (KNN).
- **kernlab—provides** -  kernel-based methods for classification, regression, and clustering algorithms.
- **randomForest—for** -  random forest classification and regression algorithms.
- **xgboost—for** -  gradient boosting, linear regression, and decision tree algorithms.
- **rpart—for** -  recursive partitioning in classification, regression, and survival trees.
- **glmnet—for** -  lasso and elastic-net regularization methods applied to linear regression, logistic regression, and multinomial regression algorithms.
- **nnet—for** -  neural networks and multinomial log-linear algorithms.
- **tensorflow—the** -  R interface to TensorFlow, for deep neural networks and numerical computation using data flow graphs.
- **Keras—the** -  R interface to Keras, for deep neural networks.
