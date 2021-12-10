# R cheatsheet

### Missing values

#### count number of missing values in each column
`df %>% map_dbl(~sum(is.na(.)))`

#### show unique values in categorical variables
`map(select_if(df, is.character), unique)`

#### convert selected values to NA
`df %>% mutate(col1 = na_if(col1, "Unknown"))`      
`df %>% mutate_at(vars(col1, col2), na_if, "Unknown")`
