# 6/7-6/8 Data Wrangling

Data Cleaning/Wrangling

Tidy Data (in R)

# Data Cleaning Wrangling

Try this in R: 

From the iris dataset, calculate the mean
Sepal.Length and mean Sepal.Width for those
flowers with Petal.Length > 3.0

this is pretty hard 

we may only want to focus on part of a data set

they say: 
”80% of Data Science is cleaning the data and the other 20% is complaining about cleaning the data”

### (Quote) Kaggle founder and CEO Anthony Goldbloom:

“... data cleaning is a much higher proportion of
data science than an outsider would expect.
Actually training models is typically a relatively
small proportion (less than 10 percent) of what a
machine learner or data scientist does.”

# Data Wrangling:

transforming data from one form into another
form with the intent of making it more suitable
for later analysis

- also called **data munging**

## Data wrangling in Tidyverse

- in R the only way to subset data is square brackets
- the tidyverse package attempts to fix this
    - tidyr and dplyr packages developed by Hadley
    Wickham
- the “verbs” are like a language of data cleaning, which creates a grammar of data manipulation

## Tidyverse Functions:

 

### filter: remove rows (observations)

- subset observations based on their values
- first argument:
– name of the data frame
- second (and subsequent arguments):
– expressions that filter the data frame

example of using filter:

```r
> filter(mpg, cty > 25)
# A tibble: 8 x 11
  manufacturer model  displ  year   cyl trans drv  
  <chr>        <chr>  <dbl> <int> <int> <chr> <chr>
1 honda        civic    1.6  1999     4 manu~ f    
2 honda        civic    1.8  2008     4 manu~ f    
3 toyota       corol~   1.8  1999     4 manu~ f    
4 toyota       corol~   1.8  2008     4 manu~ f    
5 toyota       corol~   1.8  2008     4 auto~ f    
6 volkswagen   jetta    1.9  1999     4 manu~ f    
7 volkswagen   new b~   1.9  1999     4 manu~ f    
8 volkswagen   new b~   1.9  1999     4 auto~ f    
# ... with 4 more variables: cty <int>, hwy <int>,
#   fl <chr>, class <chr>
```

notice that the mpg data type is “tibble”

this is a play on words with “table”

you can add multiple conditions:

```r
# , is equivelant to &
> filter(mpg, cty > 25, hwy > 300)

# | is used for "or"
> filter(mpg, cty > 25 | hwy > 300)

# The next 2 rows do the same thing
> filter(mpg, manufacturer == "honda" | manufacturer == "toyota")
> filter(mpg, manufacturer %in% c("honda", "toyota"))

# filter is for rows

```

### select: remove columns (variables)

```r
# for columns use select():
> select(mpg, manufacturer, model)
# output:
 
# A tibble: 234 x 2
   manufacturer model     
   <chr>        <chr>     
 1 audi         a4        
 2 audi         a4        
 3 audi         a4        
 4 audi         a4        
 5 audi         a4        
 6 audi         a4        
 7 audi         a4        
 8 audi         a4 quattro
 9 audi         a4 quattro
10 audi         a4 quattro
# ... with 224 more rows

# this gives you every column BUT manufacturer
> select(mpg, -manufacturer)
# A tibble: 234 x 10
   model      displ  year   cyl trans drv     cty   hwy
   <chr>      <dbl> <int> <int> <chr> <chr> <int> <int>
 1 a4           1.8  1999     4 auto~ f        18    29
 2 a4           1.8  1999     4 manu~ f        21    29
 3 a4           2    2008     4 manu~ f        20    31
 4 a4           2    2008     4 auto~ f        21    30
 5 a4           2.8  1999     6 auto~ f        16    26
 6 a4           2.8  1999     6 manu~ f        18    26
 7 a4           3.1  2008     6 auto~ f        18    27
 8 a4 quattro   1.8  1999     4 manu~ 4        18    26
 9 a4 quattro   1.8  1999     4 auto~ 4        16    25
10 a4 quattro   2    2008     4 manu~ 4        20    28
# ... with 224 more rows, and 2 more variables:
#   fl <chr>, class <chr>

# another tool:
> select(mpg, starts_with("m"))
```

### Data Pipelines

- Traditional R uses chained function calls to join together data operations:
    
    ```r
    > select(filter(mpg, cty > 25), manufacturer, model)
    ```
    
- This syntax extends from combinations of
functions in math: f(g(x)),
    - functions are evaluated from inner to outer
- Con: gets confusing to keep track of "the
output of this function is the input to the next
one"
- An alternative syntax emerged long ago from
Unix terminal programming:
    - 
        
        ```r
        > find . –iname '*.pdf' | grep –v 'figure' | sort –n
        ```
        
- The idea of "pipes" and "redirection" in shell
scripting is that the commands can be read from
left to right where the pipe | indicates:
    - output of left command is the input to the right
    command
- **This syntax makes multi-step chains easier to see**
    
    

EX:

```r
# these are equivelant
> select(filter(mpg, cty > 25), manufacturer, mpg)
> mpg %>% filter(cty > 25) %>% select(manufacturer, model)
```

[6/7 CLASSWORK 1:](6%207-6%208%20Data%20Wrangling%2000639c29d2b74b98aba0a0b06da1bb1f/6%207%20CLASSWORK%201%209a9e390e08d342ebb6b6e3c86993671c.md)

### arrange: sort the observations

- changes the order of rows (sorting)
- Parameters:
– column names or expressions to order/sort by
– additional columns used to break ties in the
values of preceding columns
- Ascending order by default
– Descending order: desc(cty) or -cty

ex: 

```r
> mpg %>% arrange(cty, hwy)
# A tibble: 234 x 11
   manufacturer model  displ  year   cyl trans drv     cty
   <chr>        <chr>  <dbl> <int> <int> <chr> <chr> <int>
 1 dodge        dakot~   4.7  2008     8 auto~ 4         9
 2 dodge        duran~   4.7  2008     8 auto~ 4         9
 3 dodge        ram 1~   4.7  2008     8 auto~ 4         9
 4 dodge        ram 1~   4.7  2008     8 manu~ 4         9
 5 jeep         grand~   4.7  2008     8 auto~ 4         9
 6 chevrolet    k1500~   5.3  2008     8 auto~ 4        11
 7 jeep         grand~   6.1  2008     8 auto~ 4        11
 8 chevrolet    c1500~   5.3  2008     8 auto~ r        11
 9 chevrolet    k1500~   5.7  1999     8 auto~ 4        11
10 dodge        dakot~   5.2  1999     8 auto~ 4        11
# ... with 224 more rows, and 3 more variables:
#   hwy <int>, fl <chr>, class <chr>
```

[6/7 Classwork 2:](6%207-6%208%20Data%20Wrangling%2000639c29d2b74b98aba0a0b06da1bb1f/6%207%20Classwork%202%207fad1bd628a34c41be82016a5780bd93.md)

### mutate: add or modify variables

- add new columns that are functions of
existing columns
- always adds new columns at the end of the
dataset

```r
> mpg %>% mutate(mileage = (cty+hwy)/2)
# A tibble: 234 x 12
   manufacturer model  displ  year   cyl trans drv     cty
   <chr>        <chr>  <dbl> <int> <int> <chr> <chr> <int>
 1 audi         a4       1.8  1999     4 auto~ f        18
 2 audi         a4       1.8  1999     4 manu~ f        21
 3 audi         a4       2    2008     4 manu~ f        20
 4 audi         a4       2    2008     4 auto~ f        21
 5 audi         a4       2.8  1999     6 auto~ f        16
 6 audi         a4       2.8  1999     6 manu~ f        18
 7 audi         a4       3.1  2008     6 auto~ f        18
 8 audi         a4 qu~   1.8  1999     4 manu~ 4        18
 9 audi         a4 qu~   1.8  1999     4 auto~ 4        16
10 audi         a4 qu~   2    2008     4 manu~ 4        20
# ... with 224 more rows, and 4 more variables:
#   hwy <int>, fl <chr>, class <chr>, mileage <dbl>

# if you ad view() at the end it shows you the resulting table
> mpg %>% mutate(mileage = (cty+hwy)/2) %>% view()
```

### summarize: collapse multiple values into a
single value

- Collapses a data frame to a single row
- • E.g.:
– By summing or taking the mean of a column
    
    ```r
    > airquality %>% summarise(mean(Wind))
      mean(Wind)
    1   9.957516
    
    > airquality %>% summarise(n())
      n()
    1 153
    
    > mpg %>% summarise(mean(cty), mean(hwy))
    # A tibble: 1 x 2
      `mean(cty)` `mean(hwy)`
            <dbl>       <dbl>
    1        16.9        23.4
    
    # note the column names. It's better practice to rename the columns:
    # ex:
    
    > mpg %>% summarise(CtyMean = mean(cty), HwyMean = mean(hwy))
    # A tibble: 1 x 2
      CtyMean HwyMean
        <dbl>   <dbl>
    1    16.9    23.4
    ```
    
    – Note: n() is a function that just counts the rows
    
    - Note: 
    

```r
> iris %>% filter(Petal.Length > 3, Petal.Width > 1) %>% summarize(MeanPL = mean(Petal.Length), MeanPW = mean(Petal.Width))
    MeanPL   MeanPW
1 5.023913 1.733696
```

### group_by: divide datset into subgroups

- Divides data into non-overlapping groups
- Divide dataset according to one or more
categorical variables
    
    ```r
    cars_by_manuf <- group_by(manufacturer)
    ```
    
    – Original dataset had one group (the whole data)
    – Transformed dataset has one group for every
    unique manufacturer
    

### group_by + summarize

• Together, collapses a data frame to one row
per group
• similar to R base’s aggregate()

```r
> mpg %>% group_by(manufacturer) %>% summarize(mean(cty))
# A tibble: 15 x 2
   manufacturer `mean(cty)`
   <chr>              <dbl>
 1 audi                17.6
 2 chevrolet           15  
 3 dodge               13.1
 4 ford                14  
 5 honda               24.4
 6 hyundai             18.6
 7 jeep                13.5
 8 land rover          11.5
 9 lincoln             11.3
10 mercury             13.2
11 nissan              18.1
12 pontiac             17  
13 subaru              19.3
14 toyota              18.5
15 volkswagen          20.9

> mpg %>% group_by(manufacturer) %>% summarize(mean(cty), mean(hwy))
# A tibble: 15 x 3
   manufacturer `mean(cty)` `mean(hwy)`
   <chr>              <dbl>       <dbl>
 1 audi                17.6        26.4
 2 chevrolet           15          21.9
 3 dodge               13.1        17.9
 4 ford                14          19.4
 5 honda               24.4        32.6
 6 hyundai             18.6        26.9
 7 jeep                13.5        17.6
 8 land rover          11.5        16.5
 9 lincoln             11.3        17  
10 mercury             13.2        18  
11 nissan              18.1        24.6
12 pontiac             17          26.4
13 subaru              19.3        25.6
14 toyota              18.5        24.9
15 volkswagen          20.9        29.2
```

How has city mileage changed over the years?

```r
> mpg %>% group_by(year) %>% summarize(mean(cty), mean(hwy))
# A tibble: 2 x 3
   year `mean(cty)` `mean(hwy)`
  <int>       <dbl>       <dbl>
1  1999        17.0        23.4
2  2008        16.7        23.5

```

How has the cty mileage changed over the
years for every manufacturer?

```r
> mpg %>% group_by(year, manufacturer) %>% summarize(mean(cty), mean(hwy))
`summarise()` has grouped output by 'year'. You can
override using the `.groups` argument.
# A tibble: 30 x 4
# Groups:   year [2]
    year manufacturer `mean(cty)` `mean(hwy)`
   <int> <chr>              <dbl>       <dbl>
 1  1999 audi                17.1        26.1
 2  1999 chevrolet           15.1        21.6
 3  1999 dodge               13.4        18.4
 4  1999 ford                13.9        18.6
 5  1999 honda               24.8        31.6
 6  1999 hyundai             18.3        26.7
 7  1999 jeep                14.5        18.5
 8  1999 land rover          11          15  
 9  1999 lincoln             11          16.5
10  1999 mercury             13.5        17  
# ... with 20 more rows

```

### join: Combine datasets on matching variables

Combine two tables based on their common variables
• Two tables are called
– Left table
– Right table
• Steps to combine tables:
– Identify common variables
– Create a new table with variables from BOTH tables (including the common variables)
– Add values from rows according to the specific type of join

### join types

- inner_join()
– retain (only) observations where this is a match in both datasets (left and right)
• left_join()
– Keep all rows in left-hand dataset, add values from right-hand dataset where there is a match.
– For non-matching observations, fill in NA
• right_join()
– Keep all rows in right-hand dataset, add values from left-hand dataset where there is a match.
– For non-matching observations, fill in NA
• full_join()
– Combine observations from both datasets based on matching key and fill in NA for non-matches.

![Untitled](6%207-6%208%20Data%20Wrangling%2000639c29d2b74b98aba0a0b06da1bb1f/Untitled.png)

```r
> band_members
# A tibble: 3 x 2
  name  band   
  <chr> <chr>  
1 Mick  Stones 
2 John  Beatles
3 Paul  Beatles
> band_instruments
# A tibble: 3 x 2
  name  plays 
  <chr> <chr> 
1 John  guitar
2 Paul  bass  
3 Keith guitar

# inner_join
> band_members %>% inner_join(band_instruments)
Joining, by = "name"
# A tibble: 2 x 3
  name  band    plays 
  <chr> <chr>   <chr> 
1 John  Beatles guitar
2 Paul  Beatles bass

# left_join
> band_members %>% left_join(band_instruments)
Joining, by = "name"
# A tibble: 3 x 3
  name  band    plays 
  <chr> <chr>   <chr> 
1 Mick  Stones  NA    
2 John  Beatles guitar
3 Paul  Beatles bass

# right_join
> band_members %>% right_join(band_instruments)
Joining, by = "name"
# A tibble: 3 x 3
  name  band    plays 
  <chr> <chr>   <chr> 
1 John  Beatles guitar
2 Paul  Beatles bass  
3 Keith NA      guitar

# full_join
> band_members %>% full_join(band_instruments)
Joining, by = "name"
# A tibble: 4 x 3
  name  band    plays 
  <chr> <chr>   <chr> 
1 Mick  Stones  NA    
2 John  Beatles guitar
3 Paul  Beatles bass  
4 Keith NA      guitar
```

[6/8 Classwork 1](6%207-6%208%20Data%20Wrangling%2000639c29d2b74b98aba0a0b06da1bb1f/6%208%20Classwork%201%20db33626c6bfb45afbd2d7a09624e9aa2.md)

If columns have different names for same type of variable: 

```r
> band_members
# A tibble: 3 x 2
  name  band   
  <chr> <chr>  
1 Mick  Stones 
2 John  Beatles
3 Paul  Beatles
> band_instruments2
# A tibble: 3 x 2
  artist plays 
  <chr>  <chr> 
1 John   guitar
2 Paul   bass  
3 Keith  guitar

> band_members %>% inner_join(band_instruments2, by = c(name = "artist") ) 
# A tibble: 2 x 3
  name  band    plays 
  <chr> <chr>   <chr> 
1 John  Beatles guitar
2 Paul  Beatles bass
```

### filter join types:

Create a new table with variables from only
LEFT table (including the common variables)

- semi_join()
    - return all rows from LEFT where there are
    matching values in RIGHT, keeping just columns
    from LEFT
    
    ```r
    > band_members %>% semi_join(band_instruments)
    Joining, by = "name"
    # A tibble: 2 x 2
      name  band   
      <chr> <chr>  
    1 John  Beatles
    ```
    
- anti_join():
    - return all rows from LEFT where there are not
    matching values in RIGHT, keeping just columns
    from LEFT.
    
    ```r
    > band_members %>% anti_join(band_instruments)
    Joining, by = "name"
    # A tibble: 1 x 2
      name  band  
      <chr> <chr> 
    1 Mick  Stones
    ```
    

### Special values to watch out for:

- NA: missing
    - na.rm=TRUE available in many functions
- NULL:
    - Often used when something is undefined
- Inf: infinite
- NaN: Not a number.
    - Result of an invalid computation, e.g., log(-1)
- Warnings:
    - If R mentions a warning in data wrangling, make sure you've handled it or know its origin.
    

## **Data structure semantics**

### rename: change the names of one or more
variables

### ungroup: Remove grouping from data operations

### recode: change the values of a discrete variable
(especially factor)

### slice: subset rows based on numeric order

### distinct: Keep observations that are non-
redundant (cf. unique)

[6/7 Classwork 3:](6%207-6%208%20Data%20Wrangling%2000639c29d2b74b98aba0a0b06da1bb1f/6%207%20Classwork%203%20b3f98ad3a6564cef8bee52751770da90.md)

[6/8 Classwork 3](6%207-6%208%20Data%20Wrangling%2000639c29d2b74b98aba0a0b06da1bb1f/6%208%20Classwork%203%202a08560b8197453e8825098b478b85e9.md)

[6/8 Classwork 4](6%207-6%208%20Data%20Wrangling%2000639c29d2b74b98aba0a0b06da1bb1f/6%208%20Classwork%204%208534a1325f5c4995b517abd6cec3fc73.md)
