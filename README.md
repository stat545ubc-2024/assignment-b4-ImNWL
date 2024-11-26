# Project Title: Strings and Functional Programming in R

## Overview

  This project explores functional programming and string manipulation techniques in R through two exercises:

  1. **Analyzing Word Frequencies in "Pride & Prejudice"**
      This exercise demonstrates data manipulation, visualization, and the removal of stop words using tidytext, dplyr, and ggplot2.
  2. **Custom Pig Latin Transformation**
      This exercise involves creating a customizable Pig Latin converter function and accompanying unit tests to ensure correctness.

## Repository Structure

  - `README.md`: Provides an overview and instructions for using the project.
  - `assignment.Rmd`: Contains the detailed code for both exercises.
- `assignment.md`: Markdown file generated from the R Markdown file.

## Prerequisites

  Make sure the following R packages are installed:

  - `janeaustenr`
  - `tidytext`
  - `dplyr`
  - `ggplot2`
  - `testthat`

  Install any missing packages using:

  ```R
  install.packages(c("janeaustenr", "tidytext", "dplyr", "ggplot2", "testthat"))
  ```

## Exercise Details

### Exercise 1: Most Common Words in *Pride & Prejudice*

  1. Load the book's text using the `janeaustenr` package.
  2. Clean the data:
     - Tokenize text into words.
     - Remove stop words (e.g., "the", "and") using the `stop_words` dataset.
  3. Analyze the word frequencies and visualize the most frequent words with `ggplot2`.

  **Output**: A bar plot showcasing the most common words in the book.

### Exercise 2: Custom Pig Latin Function

  1. Functionality:

     - Converts words to Pig Latin with custom suffixes.
     - Vowel-starting words remain unchanged (suffix appended).
     - Consonant-starting words move the first letter to the end (suffix appended).
     
  2. **Unit Testing**: Tests ensure correct functionality and validate error handling for invalid inputs.

  **Output**:

  - Pig Latin transformations of words.
  - Automated test results.

## Contributing

  To contribute:

  1. Fork the repository and create a new branch.
  2. Make changes and write tests for any new functionality.
  3. Submit a pull request for review.
