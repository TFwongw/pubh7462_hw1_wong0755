pubh7462\_hw1\_RMD
================
Tsz Fung Wong
January 28,2022

-   [Question 1](#question-1)
-   [Q2](#q2)
    -   [Description of Penguins
        Dataset](#description-of-penguins-dataset)
    -   [Variables Meaning](#variables-meaning)
    -   [Observation from the plots](#observation-from-the-plots)

# Question 1

``` r
q1data = tibble(x = rnorm(1000,0,1), y = rnorm(1000, 1, 2))
q1data = q1data %>% 
  mutate(sum_indicator = ifelse(q1data$x + q1data$y > 0.5, TRUE, FALSE)) %>%
  mutate(indicatorTRUE = forcats::fct_recode(factor(sum_indicator),"Yes" = "TRUE" ,"No" = "FALSE"))
q1data$indicatorTRUE = forcats::fct_relevel(q1data$indicatorTRUE, "Yes")
ggplot(q1data, aes(x, y, color = factor(indicatorTRUE))) + geom_point() +
  labs(title="Random Normal Samples", x ="X ~ N(0, 1)", y ="Y ~ N(1, 2)") +
  scale_color_discrete("X + Y > 0.5", q1data$indicatorTRUE)
```

<img src="pubh7462_hw1_wong0755_RMD_files/figure-gfm/unnamed-chunk-1-1.png" width="90%" style="display: block; margin: auto;" />

# Q2

## Description of Penguins Dataset

There are 344 observations of penguines, each is described using 8
variables. The dataset contains some missing entries denoted by NA.

## Variables Meaning

The first column contains species information for the penguins
classified the penguines into three species, namely Adélie, Chinstrap
and Gentoo. The second column contains geographic information about the
penguins, it describe the island in Palmer Archipelago, Antarctica that
the penguines belongs to (Biscoe, Dream or Torgersen). Followed by
biological statistics about the penguins, bill length, bill depth,
flipper length are ordinal variables in milimeters, body mass is another
ordinal variable in grams. Sex for the penguines is also included and is
classified into female and male. The final variable is the study year
record, takes value either in 2007, 2008 or 2009.

``` r
penguin.df <- read_rds("./data/penguin.RDS")
flipper_bill_length = ggplot(na.omit(penguin.df), aes(bill_length_mm, flipper_length_mm, color = species)) + geom_point() + 
  labs(title="Bill length verses Flipper length", x ="Flipper length(mm)", y ="Bill length(mm)") +
  scale_color_discrete("Species",penguin.df$species)
flipper_bill_length
```

<img src="pubh7462_hw1_wong0755_RMD_files/figure-gfm/unnamed-chunk-2-1.png" width="90%" style="display: block; margin: auto;" />

``` r
flipper_bill_length + facet_wrap(~ sex)
```

<img src="pubh7462_hw1_wong0755_RMD_files/figure-gfm/unnamed-chunk-2-2.png" width="90%" style="display: block; margin: auto;" />

## Observation from the plots

It seems that throughout the three species of the penguins, all shows
positive correlation between length of flipper and bill. However, when
the plots are separated by sex, there is no evident trend that the
length of flipper and bill are correlated. The seemingly possible trend
in the first plot is owing to the gender difference between male and
female penguins, which male tends to have a longer flipper and bill
compared to female ones of the same species.
