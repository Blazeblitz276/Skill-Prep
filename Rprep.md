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