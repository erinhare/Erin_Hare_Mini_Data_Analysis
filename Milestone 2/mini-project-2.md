Mini Data Analysis Milestone 2
================

*To complete this milestone, you can edit [this `.rmd`
file](https://raw.githubusercontent.com/UBC-STAT/stat545.stat.ubc.ca/master/content/mini-project/mini-project-2.Rmd)
directly. Fill in the sections that are commented out with
`<!--- start your work here--->`. When you are done, make sure to knit
to an `.md` file by changing the output in the YAML header to
`github_document`, before submitting a tagged release on canvas.*

# Welcome to your second (and last) milestone in your mini data analysis project!

In Milestone 1, you explored your data, came up with research questions,
and obtained some results by making summary tables and graphs. This
time, we will first explore more in depth the concept of *tidy data.*
Then, you’ll be sharpening some of the results you obtained from your
previous milestone by:

- Manipulating special data types in R: factors and/or dates and times.
- Fitting a model object to your data, and extract a result.
- Reading and writing data as separate files.

**NOTE**: The main purpose of the mini data analysis is to integrate
what you learn in class in an analysis. Although each milestone provides
a framework for you to conduct your analysis, it’s possible that you
might find the instructions too rigid for your data set. If this is the
case, you may deviate from the instructions – just make sure you’re
demonstrating a wide range of tools and techniques taught in this class.

# Instructions

**To complete this milestone**, edit [this very `.Rmd`
file](https://raw.githubusercontent.com/UBC-STAT/stat545.stat.ubc.ca/master/content/mini-project/mini-project-2.Rmd)
directly. Fill in the sections that are tagged with
`<!--- start your work here--->`.

**To submit this milestone**, make sure to knit this `.Rmd` file to an
`.md` file by changing the YAML output settings from
`output: html_document` to `output: github_document`. Commit and push
all of your work to your mini-analysis GitHub repository, and tag a
release on GitHub. Then, submit a link to your tagged release on canvas.

**Points**: This milestone is worth 55 points (compared to the 45 points
of the Milestone 1): 45 for your analysis, and 10 for your entire
mini-analysis GitHub repository. Details follow.

**Research Questions**: In Milestone 1, you chose two research questions
to focus on. Wherever realistic, your work in this milestone should
relate to these research questions whenever we ask for justification
behind your work. In the case that some tasks in this milestone don’t
align well with one of your research questions, feel free to discuss
your results in the context of a different research question.

# Learning Objectives

By the end of this milestone, you should:

- Understand what *tidy* data is, and how to create it using `tidyr`.
- Generate a reproducible and clear report using R Markdown.
- Manipulating special data types in R: factors and/or dates and times.
- Fitting a model object to your data, and extract a result.
- Reading and writing data as separate files.

# Setup

Begin by loading your data and the tidyverse package below:

``` r
library(datateachr) # <- might contain the data you picked!
library(tidyverse)
```

    ## Warning: package 'tidyverse' was built under R version 4.1.3

    ## Warning: package 'ggplot2' was built under R version 4.1.3

    ## Warning: package 'tibble' was built under R version 4.1.3

    ## Warning: package 'tidyr' was built under R version 4.1.3

    ## Warning: package 'dplyr' was built under R version 4.1.3

    ## Warning: package 'stringr' was built under R version 4.1.3

    ## Warning: package 'forcats' was built under R version 4.1.3

# Task 1: Tidy your data (15 points)

In this task, we will do several exercises to reshape our data. The goal
here is to understand how to do this reshaping with the `tidyr` package.

A reminder of the definition of *tidy* data:

- Each row is an **observation**
- Each column is a **variable**
- Each cell is a **value**

*Tidy’ing* data is sometimes necessary because it can simplify
computation. Other times it can be nice to organize data so that it can
be easier to understand when read manually.

### 2.1 (2.5 points)

Based on the definition above, can you identify if your data is tidy or
untidy? Go through all your columns, or if you have \>8 variables, just
pick 8, and explain whether the data is untidy or tidy.

<!--------------------------- Start your work below --------------------------->

``` r
cancer_sample
```

    ## # A tibble: 569 x 32
    ##          ID diagnosis radius_m~1 textu~2 perim~3 area_~4 smoot~5 compa~6 conca~7
    ##       <dbl> <chr>          <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>
    ##  1   842302 M               18.0    10.4   123.    1001   0.118   0.278   0.300 
    ##  2   842517 M               20.6    17.8   133.    1326   0.0847  0.0786  0.0869
    ##  3 84300903 M               19.7    21.2   130     1203   0.110   0.160   0.197 
    ##  4 84348301 M               11.4    20.4    77.6    386.  0.142   0.284   0.241 
    ##  5 84358402 M               20.3    14.3   135.    1297   0.100   0.133   0.198 
    ##  6   843786 M               12.4    15.7    82.6    477.  0.128   0.17    0.158 
    ##  7   844359 M               18.2    20.0   120.    1040   0.0946  0.109   0.113 
    ##  8 84458202 M               13.7    20.8    90.2    578.  0.119   0.164   0.0937
    ##  9   844981 M               13      21.8    87.5    520.  0.127   0.193   0.186 
    ## 10 84501001 M               12.5    24.0    84.0    476.  0.119   0.240   0.227 
    ## # ... with 559 more rows, 23 more variables: concave_points_mean <dbl>,
    ## #   symmetry_mean <dbl>, fractal_dimension_mean <dbl>, radius_se <dbl>,
    ## #   texture_se <dbl>, perimeter_se <dbl>, area_se <dbl>, smoothness_se <dbl>,
    ## #   compactness_se <dbl>, concavity_se <dbl>, concave_points_se <dbl>,
    ## #   symmetry_se <dbl>, fractal_dimension_se <dbl>, radius_worst <dbl>,
    ## #   texture_worst <dbl>, perimeter_worst <dbl>, area_worst <dbl>,
    ## #   smoothness_worst <dbl>, compactness_worst <dbl>, concavity_worst <dbl>, ...

Each cell in the ID column contains each individuals patient ID. Each
cell in the diagnosis column contains an M or B which applies to the
individual patient based on their ID. Each cell in the radius_mean
column contains the mean radius measurement that applies to the patient
based on their ID. Each cell in the radius_se column contains the radius
standard error for each patient based on their ID. Each cell in the
radius_worst column contains the worst radius measurement for each
patient based on their ID. Each cell in the area_mean column contains
the mean area measurement that applies to the patient based on their ID.
Each cell in the area_se column contains the area standard error for
each patient based on their ID. Each cell in the area_worst column
contains the worst area measurement for each patient based on their ID.

Based on reviewing these 8 variables, the data is tidy because each
column is a different variable, each row represents a different patient
using their individual ID, and each cell contains a single measurement
or diagnosis value.
<!----------------------------------------------------------------------------->

### 2.2 (5 points)

Now, if your data is tidy, untidy it! Then, tidy it back to it’s
original state.

If your data is untidy, then tidy it! Then, untidy it back to it’s
original state.

Be sure to explain your reasoning for this task. Show us the “before”
and “after”.

<!--------------------------- Start your work below --------------------------->

The original state of the data is tidy since each row represents an
individual patient based on their unique ID. Each column is a variable
and each cell is an diagnostic or measurement value that applies to the
patient ID.

The following code is used to untidy the data by making the tibble
longer. This results in multiple rows containing the same patient ID
since each row contains a different measurement type so the
“measurement_type” column contains multiple variables.

``` r
untidy_cancer_sample <- cancer_sample %>% pivot_longer(cols = c(-ID, -diagnosis),
                               names_to = "measurement_type",
                               values_to = "measurement")
untidy_cancer_sample
```

    ## # A tibble: 17,070 x 4
    ##        ID diagnosis measurement_type       measurement
    ##     <dbl> <chr>     <chr>                        <dbl>
    ##  1 842302 M         radius_mean                18.0   
    ##  2 842302 M         texture_mean               10.4   
    ##  3 842302 M         perimeter_mean            123.    
    ##  4 842302 M         area_mean                1001     
    ##  5 842302 M         smoothness_mean             0.118 
    ##  6 842302 M         compactness_mean            0.278 
    ##  7 842302 M         concavity_mean              0.300 
    ##  8 842302 M         concave_points_mean         0.147 
    ##  9 842302 M         symmetry_mean               0.242 
    ## 10 842302 M         fractal_dimension_mean      0.0787
    ## # ... with 17,060 more rows

The next code is used to widen the tibble which organizes the data back
into it’s tidy state.

``` r
tidy_cancer_sample <- untidy_cancer_sample %>% pivot_wider(id_cols = c(ID, diagnosis),
                                                           names_from = measurement_type,
                                                           values_from = measurement)
tidy_cancer_sample
```

    ## # A tibble: 569 x 32
    ##          ID diagnosis radius_m~1 textu~2 perim~3 area_~4 smoot~5 compa~6 conca~7
    ##       <dbl> <chr>          <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>
    ##  1   842302 M               18.0    10.4   123.    1001   0.118   0.278   0.300 
    ##  2   842517 M               20.6    17.8   133.    1326   0.0847  0.0786  0.0869
    ##  3 84300903 M               19.7    21.2   130     1203   0.110   0.160   0.197 
    ##  4 84348301 M               11.4    20.4    77.6    386.  0.142   0.284   0.241 
    ##  5 84358402 M               20.3    14.3   135.    1297   0.100   0.133   0.198 
    ##  6   843786 M               12.4    15.7    82.6    477.  0.128   0.17    0.158 
    ##  7   844359 M               18.2    20.0   120.    1040   0.0946  0.109   0.113 
    ##  8 84458202 M               13.7    20.8    90.2    578.  0.119   0.164   0.0937
    ##  9   844981 M               13      21.8    87.5    520.  0.127   0.193   0.186 
    ## 10 84501001 M               12.5    24.0    84.0    476.  0.119   0.240   0.227 
    ## # ... with 559 more rows, 23 more variables: concave_points_mean <dbl>,
    ## #   symmetry_mean <dbl>, fractal_dimension_mean <dbl>, radius_se <dbl>,
    ## #   texture_se <dbl>, perimeter_se <dbl>, area_se <dbl>, smoothness_se <dbl>,
    ## #   compactness_se <dbl>, concavity_se <dbl>, concave_points_se <dbl>,
    ## #   symmetry_se <dbl>, fractal_dimension_se <dbl>, radius_worst <dbl>,
    ## #   texture_worst <dbl>, perimeter_worst <dbl>, area_worst <dbl>,
    ## #   smoothness_worst <dbl>, compactness_worst <dbl>, concavity_worst <dbl>, ...

<!----------------------------------------------------------------------------->

### 2.3 (7.5 points)

Now, you should be more familiar with your data, and also have made
progress in answering your research questions. Based on your interest,
and your analyses, pick 2 of the 4 research questions to continue your
analysis in the next four tasks:

<!-------------------------- Start your work below ---------------------------->

1.  *What proportion of individuals with a malignant tumor diagnosis
    have an area_mean greater than 200?*
2.  *Is the relationship between concave_points_mean and concavity_mean
    the same between B and M diagnosis and what is the relationship?*

<!----------------------------------------------------------------------------->

Explain your decision for choosing the above two research questions.

<!--------------------------- Start your work below --------------------------->

The first question was selected because it can be used in task 2 since
the area_mean variable was divided into three categories in Milestone 1.

The second question was selected because it can be used in task 3 since
the question is asking about the relationship between two variables
which can be viewed in a model.

<!----------------------------------------------------------------------------->

Now, try to choose a version of your data that you think will be
appropriate to answer these 2 questions. Use between 4 and 8 functions
that we’ve covered so far (i.e. by filtering, cleaning, tidy’ing,
dropping irrelevant columns, etc.).

<!--------------------------- Start your work below --------------------------->

Question 1

``` r
cancer_sample_1 <- cancer_sample %>% 
  select(ID, diagnosis, area_mean) %>%
  filter(diagnosis == "M") %>%
  arrange(area_mean) %>%
  mutate(area_mean_category = case_when(area_mean < 800 ~ "small",
                                        area_mean < 1200 ~ "medium",
                                        area_mean < 2502 ~ "large"))
cancer_sample_1
```

    ## # A tibble: 212 x 4
    ##          ID diagnosis area_mean area_mean_category
    ##       <dbl> <chr>         <dbl> <chr>             
    ##  1  9013838 M              362. small             
    ##  2   855563 M              371. small             
    ##  3 84348301 M              386. small             
    ##  4   892189 M              431. small             
    ##  5   869691 M              432  small             
    ##  6   853612 M              441. small             
    ##  7 84501001 M              476. small             
    ##  8   843786 M              477. small             
    ##  9   875263 M              477. small             
    ## 10 85922302 M              499  small             
    ## # ... with 202 more rows

Question 2

``` r
cancer_sample_2 <- select(cancer_sample, c("ID", "diagnosis", "concave_points_mean", "concavity_mean"))
cancer_sample_2
```

    ## # A tibble: 569 x 4
    ##          ID diagnosis concave_points_mean concavity_mean
    ##       <dbl> <chr>                   <dbl>          <dbl>
    ##  1   842302 M                      0.147          0.300 
    ##  2   842517 M                      0.0702         0.0869
    ##  3 84300903 M                      0.128          0.197 
    ##  4 84348301 M                      0.105          0.241 
    ##  5 84358402 M                      0.104          0.198 
    ##  6   843786 M                      0.0809         0.158 
    ##  7   844359 M                      0.074          0.113 
    ##  8 84458202 M                      0.0598         0.0937
    ##  9   844981 M                      0.0935         0.186 
    ## 10 84501001 M                      0.0854         0.227 
    ## # ... with 559 more rows

<!----------------------------------------------------------------------------->

# Task 2: Special Data Types (10)

For this exercise, you’ll be choosing two of the three tasks below –
both tasks that you choose are worth 5 points each.

But first, tasks 1 and 2 below ask you to modify a plot you made in a
previous milestone. The plot you choose should involve plotting across
at least three groups (whether by facetting, or using an aesthetic like
colour). Place this plot below (you’re allowed to modify the plot if
you’d like). If you don’t have such a plot, you’ll need to make one.
Place the code for your plot below.

<!-------------------------- Start your work below ---------------------------->

``` r
cancer_sample_1 %>%
  ggplot(aes(area_mean_category)) +
  geom_bar()
```

![](mini-project-2_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

``` r
cancer_sample_1 %>%
  ggplot(aes(area_mean_category, area_mean)) +
  geom_boxplot()
```

![](mini-project-2_files/figure-gfm/unnamed-chunk-7-2.png)<!-- -->
<!----------------------------------------------------------------------------->

Now, choose two of the following tasks.

1.  Produce a new plot that reorders a factor in your original plot,
    using the `forcats` package (3 points). Then, in a sentence or two,
    briefly explain why you chose this ordering (1 point here for
    demonstrating understanding of the reordering, and 1 point for
    demonstrating some justification for the reordering, which could be
    subtle or speculative.)

2.  Produce a new plot that groups some factor levels together into an
    “other” category (or something similar), using the `forcats` package
    (3 points). Then, in a sentence or two, briefly explain why you
    chose this grouping (1 point here for demonstrating understanding of
    the grouping, and 1 point for demonstrating some justification for
    the grouping, which could be subtle or speculative.)

3.  If your data has some sort of time-based column like a date (but
    something more granular than just a year):

    1.  Make a new column that uses a function from the `lubridate` or
        `tsibble` package to modify your original time-based column. (3
        points)

        - Note that you might first have to *make* a time-based column
          using a function like `ymd()`, but this doesn’t count.
        - Examples of something you might do here: extract the day of
          the year from a date, or extract the weekday, or let 24 hours
          elapse on your dates.

    2.  Then, in a sentence or two, explain how your new column might be
        useful in exploring a research question. (1 point for
        demonstrating understanding of the function you used, and 1
        point for your justification, which could be subtle or
        speculative).

        - For example, you could say something like “Investigating the
          day of the week might be insightful because penguins don’t
          work on weekends, and so may respond differently”.

<!-------------------------- Start your work below ---------------------------->

**Task Number**: 1

``` r
cancer_sample_1 %>%
  mutate(area_mean_category = fct_inorder(area_mean_category)) %>%
  ggplot(aes(area_mean_category)) +
  geom_bar()
```

![](mini-project-2_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

The original ordering of the bars was large, medium, small and has been
reordered to small, medium, large since it makes more sense visually to
view the mean area from smallest to largest categories going from left
to right.
<!----------------------------------------------------------------------------->

<!-------------------------- Start your work below ---------------------------->

**Task Number**: 2

``` r
cancer_sample_1$area_mean_category <- as.factor(cancer_sample_1$area_mean_category)
cancer_sample_1 %>%
  mutate(area_mean_category = fct_other(area_mean_category, keep = c("large"))) %>%
  ggplot(aes(area_mean_category, area_mean)) +
  geom_boxplot()
```

![](mini-project-2_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

The original boxplot contained three categories (small, medium, and
large). The “small” and “medium” categories have been grouped into an
“other” category since the first research question is interested in
individuals with an area_mean greater than 200 which are those in the
large category. The question is not interested in individuals in the
small and medium category so it is appropriate to group them into an
“other” category.
<!----------------------------------------------------------------------------->

# Task 3: Modelling

## 2.0 (no points)

Pick a research question, and pick a variable of interest (we’ll call it
“Y”) that’s relevant to the research question. Indicate these.

<!-------------------------- Start your work below ---------------------------->

**Research Question**: Is the relationship between concave_points_mean
and concavity_mean the same between B and M diagnosis and what is the
relationship?

**Variable of interest**: concave_points_mean

<!----------------------------------------------------------------------------->

## 2.1 (5 points)

Fit a model or run a hypothesis test that provides insight on this
variable with respect to the research question. Store the model object
as a variable, and print its output to screen. We’ll omit having to
justify your choice, because we don’t expect you to know about model
specifics in STAT 545.

- **Note**: It’s OK if you don’t know how these models/tests work. Here
  are some examples of things you can do here, but the sky’s the limit.

  - You could fit a model that makes predictions on Y using another
    variable, by using the `lm()` function.
  - You could test whether the mean of Y equals 0 using `t.test()`, or
    maybe the mean across two groups are different using `t.test()`, or
    maybe the mean across multiple groups are different using `anova()`
    (you may have to pivot your data for the latter two).
  - You could use `lm()` to test for significance of regression.

<!-------------------------- Start your work below ---------------------------->

``` r
concave_points_mean_lm <- lm(concave_points_mean ~ concavity_mean, cancer_sample_2)
concave_points_mean_lm
```

    ## 
    ## Call:
    ## lm(formula = concave_points_mean ~ concavity_mean, data = cancer_sample_2)
    ## 
    ## Coefficients:
    ##    (Intercept)  concavity_mean  
    ##       0.009095        0.448478

<!----------------------------------------------------------------------------->

## 2.2 (5 points)

Produce something relevant from your fitted model: either predictions on
Y, or a single value like a regression coefficient or a p-value.

- Be sure to indicate in writing what you chose to produce.
- Your code should either output a tibble (in which case you should
  indicate the column that contains the thing you’re looking for), or
  the thing you’re looking for itself.
- Obtain your results using the `broom` package if possible. If your
  model is not compatible with the broom function you’re needing, then
  you can obtain your results by some other means, but first indicate
  which broom function is not compatible.

<!-------------------------- Start your work below ---------------------------->

The following code is used to produce the p-value which is found in
column 5 “p.value”. The concavity_mean predictor variable is
statistically significant since the p-value is less than 0.05.

``` r
library(broom)
```

    ## Warning: package 'broom' was built under R version 4.1.3

``` r
broom::tidy(concave_points_mean_lm)
```

    ## # A tibble: 2 x 5
    ##   term           estimate std.error statistic   p.value
    ##   <chr>             <dbl>     <dbl>     <dbl>     <dbl>
    ## 1 (Intercept)     0.00909  0.000948      9.60 2.60e- 20
    ## 2 concavity_mean  0.448    0.00794      56.5  6.79e-235

<!----------------------------------------------------------------------------->

# Task 4: Reading and writing data

Get set up for this exercise by making a folder called `output` in the
top level of your project folder / repository. You’ll be saving things
there.

## 3.1 (5 points)

Take a summary table that you made from Milestone 1 (Task 4.2), and
write it as a csv file in your `output` folder. Use the `here::here()`
function.

- **Robustness criteria**: You should be able to move your Mini Project
  repository / project folder to some other location on your computer,
  or move this very Rmd file to another location within your project
  repository / folder, and your code should still work.
- **Reproducibility criteria**: You should be able to delete the csv
  file, and remake it simply by knitting this Rmd file.

<!-------------------------- Start your work below ---------------------------->

``` r
dir.create(here::here("output"))
```

    ## Warning in dir.create(here::here("output")): 'C:\Users\ehare\Documents\UBC\STAT
    ## 545A\Erin_Hare_Mini_Data_Analysis\output' already exists

``` r
write.csv(cancer_sample %>% group_by(diagnosis) %>% summarise(area_worst = range(area_worst, na.rm = TRUE)), here::here("output", "area_worst_range.csv"))
```

    ## `summarise()` has grouped output by 'diagnosis'. You can override using the
    ## `.groups` argument.

<!----------------------------------------------------------------------------->

## 3.2 (5 points)

Write your model object from Task 3 to an R binary file (an RDS), and
load it again. Be sure to save the binary file in your `output` folder.
Use the functions `saveRDS()` and `readRDS()`.

- The same robustness and reproducibility criteria as in 3.1 apply here.

<!-------------------------- Start your work below ---------------------------->

``` r
library(here)
```

    ## Warning: package 'here' was built under R version 4.1.3

    ## here() starts at C:/Users/ehare/Documents/UBC/STAT 545A/Erin_Hare_Mini_Data_Analysis

``` r
saveRDS(concave_points_mean_lm, file = here("output", "concave_points_mean_lm.rds"))
readRDS(here("output", "concave_points_mean_lm.rds"))
```

    ## 
    ## Call:
    ## lm(formula = concave_points_mean ~ concavity_mean, data = cancer_sample_2)
    ## 
    ## Coefficients:
    ##    (Intercept)  concavity_mean  
    ##       0.009095        0.448478

<!----------------------------------------------------------------------------->

# Tidy Repository

Now that this is your last milestone, your entire project repository
should be organized. Here are the criteria we’re looking for.

## Main README (3 points)

There should be a file named `README.md` at the top level of your
repository. Its contents should automatically appear when you visit the
repository on GitHub.

Minimum contents of the README file:

- In a sentence or two, explains what this repository is, so that
  future-you or someone else stumbling on your repository can be
  oriented to the repository.
- In a sentence or two (or more??), briefly explains how to engage with
  the repository. You can assume the person reading knows the material
  from STAT 545A. Basically, if a visitor to your repository wants to
  explore your project, what should they know?

Once you get in the habit of making README files, and seeing more README
files in other projects, you’ll wonder how you ever got by without them!
They are tremendously helpful.

## File and Folder structure (3 points)

You should have at least four folders in the top level of your
repository: one for each milestone, and one output folder. If there are
any other folders, these are explained in the main README.

Each milestone document is contained in its respective folder, and
nowhere else.

Every level-1 folder (that is, the ones stored in the top level, like
“Milestone1” and “output”) has a `README` file, explaining in a sentence
or two what is in the folder, in plain language (it’s enough to say
something like “This folder contains the source for Milestone 1”).

## Output (2 points)

All output is recent and relevant:

- All Rmd files have been `knit`ted to their output, and all data files
  saved from Task 4 above appear in the `output` folder.
- All of these output files are up-to-date – that is, they haven’t
  fallen behind after the source (Rmd) files have been updated.
- There should be no relic output files. For example, if you were
  knitting an Rmd to html, but then changed the output to be only a
  markdown file, then the html file is a relic and should be deleted.

Our recommendation: delete all output files, and re-knit each
milestone’s Rmd file, so that everything is up to date and relevant.

PS: there’s a way where you can run all project code using a single
command, instead of clicking “knit” three times. More on this in STAT
545B!

## Error-free code (1 point)

This Milestone 1 document knits error-free, and the Milestone 2 document
knits error-free.

## Tagged release (1 point)

You’ve tagged a release for Milestone 1, and you’ve tagged a release for
Milestone 2.

### Attribution

Thanks to Victor Yuan for mostly putting this together.
