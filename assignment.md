Option A – Strings and functional programming in R
================

# Exercise 1: Analyze the Most Common Words in a Book

Source of the book: “Pride & Prejudice” by Jane Austen, available in the
janeaustenr package

``` r
# Load required libraries
library(janeaustenr)
library(tidytext)
library(dplyr)
```

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
library(ggplot2)

# Load the text of "Pride & Prejudice" from the janeaustenr package
data <- austen_books() %>%
  filter(book == "Pride & Prejudice") %>%  # Filter for the specific book
  unnest_tokens(word, text)  # Split the text into individual words

# Load stop_words dataset
data("stop_words", package = "tidytext")

# Remove stop words using a predefined list
data_clean <- data %>%
  anti_join(stop_words, by = "word")  # Ensure the join is by the 'word' column

# Count word frequencies
word_freq <- data_clean %>%
  count(word, sort = TRUE) %>%  # Count the occurrences of each word
  filter(n > 100)  # Filter words that appear more than 100 times

# Create a bar plot of the most common words
ggplot(word_freq, aes(x = reorder(word, n), y = n)) +
  geom_bar(stat = "identity") +  # Create a bar chart
  coord_flip() +  # Flip coordinates for better readability
  labs(title = "Most Common Words in 'Pride & Prejudice'",
       x = "Words",
       y = "Frequency") +
  theme_minimal()  # Use a clean and simple theme
```

![](assignment_files/figure-gfm/unnamed-chunk-1-1.png)<!-- -->

# Exercise 2: Custom Pig Latin Function

``` r
#' Convert words to a customized version of Pig Latin
#'
#' This function converts input words into a customized version of Pig Latin. 
#' The transformation rules are as follows:
#' 
#' - For words that start with a vowel (a, e, i, o, u), the word remains unchanged, and a suffix (default: "xyz") is appended to the end.
#' - For words that start with a consonant, the first letter is moved to the end of the word, and the suffix is appended.
#' 
#' @param word A character vector of words to convert.
#' @param suffix A string to append to the rearranged word. Default is "xyz".
#' @return A character vector of words in the customized Pig Latin format.
#' @examples
#' # Example with default suffix
#' custom_pig_latin("hello")  # Returns "ellohxyz"
#' custom_pig_latin(c("apple", "banana"))  # Returns c("applexyz", "ananabxyz")
#'
#' # Example with custom suffix
#' custom_pig_latin(c("hello", "apple"), suffix = "abc")  # Returns c("ellohabc", "appleabc")
#'
#' # Handling invalid input
#' \dontrun{
#' custom_pig_latin(123)  # Throws an error
#' }
#' @export
custom_pig_latin <- function(word, suffix = "xyz") {
  # Check if the input is a character vector
  if (!is.character(word)) stop("Input must be a character vector")
  
  # Apply Pig Latin transformation to each word
  result <- sapply(word, function(w) {
    # Check if the word starts with a vowel
    if (grepl("^[aeiouAEIOU]", w)) {
      paste0(w, suffix)  # Add the suffix to the original word
    } else {
      # Move the first letter to the end and add the suffix
      paste0(substr(w, 2, nchar(w)), substr(w, 1, 1), suffix)
    }
  })
  
  # Ensure the result is unnamed
  unname(result)
}

# Example usage
custom_pig_latin(c("hello", "apple", "string"))  # Should output Pig Latin transformations
```

    ## [1] "ellohxyz"  "applexyz"  "tringsxyz"

``` r
# Write tests for the Pig Latin function
library(testthat)
```

    ## 
    ## Attaching package: 'testthat'

    ## The following object is masked from 'package:dplyr':
    ## 
    ##     matches

``` r
test_that("Pig Latin conversion for consonant-starting word works correctly", {
  # Calculation:
  # "hello" starts with a consonant ('h'), so move 'h' to the end and append the default suffix "xyz".
  # Result: "ellohxyz"
  expect_equal(custom_pig_latin("hello"), "ellohxyz")
})
```

    ## Test passed 🎊

``` r
test_that("Pig Latin conversion for vowel-starting word works correctly", {
  # Calculation:
  # "apple" starts with a vowel ('a'), so keep the word unchanged and append the default suffix "xyz".
  # Result: "applexyz"
  expect_equal(custom_pig_latin("apple"), "applexyz")
})
```

    ## Test passed 🎉

``` r
test_that("Pig Latin function handles invalid input correctly", {
  # Calculation:
  # The input is numeric (123), which is not a character vector. The function should throw an error.
  # Expected error message: "Input must be a character vector"
  expect_error(custom_pig_latin(123), "Input must be a character vector")
})
```

    ## Test passed 😸
