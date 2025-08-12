---
title: 'Getting started with R'
published: 2025-08-01
draft: false
description: 'A beginner-friendly guide to installing R, exploring the basics, and running your first data analysis.'
tags: ['R', 'data science', 'programming']
---

R is a programming language designed for statistical computing and data visualization. It’s widely used in data science, research, and academia. This guide walks you through installing R, exploring its basics, and performing a simple analysis.

## Installing R

### 1. Install R

Download R from the Comprehensive R Archive Network (CRAN):  
[https://cran.r-project.org](https://cran.r-project.org)

Choose the installer for your operating system and follow the prompts.

### 2. Install RStudio (Recommended)

RStudio is a popular integrated development environment (IDE) for R. Download it here:  
[https://posit.co/download/rstudio-desktop/](https://posit.co/download/rstudio-desktop/)

## Running R

You can run R:

- In the RStudio console
- Directly in the terminal by typing `R`
- In scripts saved as `.R` files

## Basic Syntax

```r
# Assign variables
x <- 5
y <- 10

# Print output
print(x + y)

# Create a vector
numbers <- c(1, 2, 3, 4, 5)

# Get the mean
mean(numbers)
```

## Data Structures

- **Vector**: One-dimensional array of elements of the same type.
- **Matrix**: Two-dimensional array.
- **Data Frame**: Table-like structure (similar to a spreadsheet).
- **List**: Collection of elements of different types.

Example of a data frame:

```r
data <- data.frame(
    name = c("Alice", "Bob"),
    age = c(25, 30)
)

print(data)
```

## Installing and Loading Packages

Packages extend R’s functionality.

```r
install.packages("ggplot2")
library(ggplot2)
```

## Plotting Data

```r
library(ggplot2)

df <- data.frame(
    x = 1:10,
    y = c(2, 3, 5, 7, 11, 13, 17, 19, 23, 29)
)

ggplot(df, aes(x = x, y = y)) +
    geom_point() +
    geom_line() +
    labs(title = "Simple Plot", x = "X values", y = "Y values")
```

## Reading Data from a CSV

```r
data <- read.csv("data.csv")
head(data)
```

## Performing a Simple Analysis

```r
summary(data)
cor(data$x, data$y)
```

## Tips for Learning R

- Practice with built-in datasets (`mtcars`, `iris`).
- Learn vectorized operations instead of loops when possible.
- Explore R’s extensive package ecosystem for specialized analysis.

## Final Thoughts

R is an excellent choice for statistics and visualization. Once you’re comfortable with the basics, explore tidyverse packages for modern, streamlined data analysis.
