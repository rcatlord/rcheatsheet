# R cheatsheet

### Missing values

#### count number of missing values in each column
`df %>% map_dbl(~sum(is.na(.)))`

#### show unique values in categorical variables
`map(select_if(df, is.character), unique)`

#### convert selected values to NA
`df %>% mutate(col1 = na_if(col1, "Unknown"))`      
`df %>% mutate_at(vars(col1, col2), na_if, "Unknown")`

### Test for normality
```
# Histogram with a density curve
hist(df$col1, probability = T)
lines(density(df$col1), col = 2)

# Q-Q plot
# Points should be close to the line to be considered normally distributed
qqnorm(df$col1, pch = 19)
qqline(df$col1)

# Shapiro-Wilk test
# If p> 0.05, normality can be assumed
shapiro.test(df$col1)
```

## Standardise values
`df %>% mutate(col1 = scale(col1))`
