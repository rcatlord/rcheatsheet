# R cheatsheet

### Tidying data

#### pivot_wider
`pivot_wider(names_from = year, values_from = percent) `

#### pivot_longer
`pivot_longer(-name, names_to = "year", values_to = "n") `

### Reading Excel spreadsheets via a URL
```
library(httr) ; library(readxl)
tmp <- tempfile(fileext = ".xlsx")
GET(url = "https://.xlsx", write_disk(tmp))
df <- read_xlsx(tmp, sheet = "Sheet 1") 
```

### Missing values

#### count number of missing values in each column
`df %>% map_dbl(~sum(is.na(.)))`

#### count unique values in every column
`df %>% map_int(n_distinct)`

#### show unique values in categorical variables
`map(select_if(df, is.character), unique)`

#### convert selected values to NA
`df %>% mutate(col1 = na_if(col1, "Unknown"))`      
`df %>% mutate_at(vars(col1, col2), na_if, "Unknown")`

#### convert string to NA across all columns
`mutate(across(everything(), na_if, ".."))`

#### mutate and move new column
`penguins %>% 
  mutate(id = row_number(), .before = contains("_"))`

### Dates
#### Format date
`as.Date(paste0("15_", "Jan_1998"), format = "%d_%b_%Y")`

### Standardise values
`df %>% mutate(col1 = scale(col1))`
