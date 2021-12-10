# R cheatsheet

### Missing values

#### count number of missing values in each column
`df %>% map_dbl(~sum(is.na(.)))`

#### unique values in categorical variables
`map(select_if(df, is.character), unique)`
