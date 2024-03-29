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

### Visualising data
#### Tweaks to ggplot2 theme
```
theme(plot.margin = unit(rep(0.5, 4), "cm"),
      panel.grid.major.x = element_blank(),
      panel.grid.minor = element_blank(),
      axis.line.x = element_line(),
      plot.title = element_text(size = 18, face = "bold"),
      plot.subtitle = element_text(size = 14, margin = margin(b = 20)),
      plot.caption = element_text(hjust = 0, margin = margin(t = 20)))
```

#### Round percentages
`scales::label_percent(accuracy = 1L)`

### Dates

|Symbol |Description |Example | 
|:--- |:--- |:---|
|%d	|day as a number (0-31)	|15|
|%a	|abbreviated weekday	|Tue|
|%A	|unabbreviated weekday	|Tuesday|
|%m	|month (00-12)	|07|
|%b	|abbreviated month	|Jul|
|%B	|unabbreviated month	|July|
|%y	|2-digit year	|23|
|%Y	|4-digit year	|2023|
