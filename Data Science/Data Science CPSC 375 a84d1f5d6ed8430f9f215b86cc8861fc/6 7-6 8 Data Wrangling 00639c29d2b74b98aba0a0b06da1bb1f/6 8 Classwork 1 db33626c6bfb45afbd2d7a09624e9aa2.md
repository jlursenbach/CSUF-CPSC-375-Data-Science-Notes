# 6/8 Classwork 1

![Untitled](6%208%20Classwork%201%20db33626c6bfb45afbd2d7a09624e9aa2/Untitled.png)

# Calculate the different joins for these two tables.

SETTING UP TABLES:

```r
> band_members_4rows <- band_members %>%
+     add_row(name="Paul", band="Wings")

> band_members_4rows
# A tibble: 4 x 2
  name  band   
  <chr> <chr>  
1 Mick  Stones 
2 John  Beatles
3 Paul  Beatles
4 Paul  Wings

> band_instruments_4rows <- band_instruments %>%
+     add_row(name="Paul", plays="vocals")

> band_instruments_4rows
# A tibble: 4 x 2
  name  plays 
  <chr> <chr> 
1 John  guitar
2 Paul  bass  
3 Keith guitar
4 Paul  vocals
```

## First, do them by hand:

### inner_join:

– retain (only) observations where this is a match in both datasets (left and right)

| Name | Band | Plays |
| --- | --- | --- |
| John  | Beatles  | guitar |
| Paul  | Beatles  | bass |
| Paul  | Beatles  | vocals |
| Paul  | Wings  | bass |
| Paul  | Wings  | vocals |

### left_join:

– Keep all rows in left-hand dataset, add values from right-hand dataset where there is a match.
– For non-matching observations, fill in NA

| Name | Band | Plays |
| --- | --- | --- |
| 1 Mick  | Stones  | NA |
| John  | Beatles  | guitar |
| Paul  | Beatles  | bass |
| Paul  | Beatles  | vocals |
| Paul  | Wings  | bass |
| Paul  | Wings  | vocals |

### right_join:

– Keep all rows in right-hand dataset, add values from left-hand dataset where there is a match.
– For non-matching observations, fill in NA

| Name | Band | Plays |
| --- | --- | --- |
| John  | Beatles  | guitar |
| Paul  | Beatles  | bass |
| Paul  | Beatles  | vocals |
| Paul  | Wings  | bass |
| Paul  | Wings  | vocals |
| Keith  | NA  | guitar |

### full_join:

– Combine observations from both datasets based on matching key and fill in NA for non-matches.

| Name | Band | Plays |
| --- | --- | --- |
| 1 Mick  | Stones  | NA |
| John  | Beatles  | guitar |
| Paul  | Beatles  | bass |
| Paul  | Beatles  | vocals |
| Paul  | Wings  | bass |
| Paul  | Wings  | vocals |
| Keith  | NA  | guitar |

## Second, confirm your results with code:

### inner_join:

```r
> band_members_4rows %>% inner_join(band_instruments_4rows)
Joining, by = "name"
# A tibble: 5 x 3
  name  band    plays 
  <chr> <chr>   <chr> 
1 John  Beatles guitar
2 Paul  Beatles bass  
3 Paul  Beatles vocals
4 Paul  Wings   bass  
5 Paul  Wings   vocals
```

### left_join:

```r
> band_members_4rows %>% left_join(band_instruments_4rows)
Joining, by = "name"
# A tibble: 6 x 3
  name  band    plays 
  <chr> <chr>   <chr> 
1 Mick  Stones  NA    
2 John  Beatles guitar
3 Paul  Beatles bass  
4 Paul  Beatles vocals
5 Paul  Wings   bass  
6 Paul  Wings   vocals
```

### right_join:

```r
> band_members_4rows %>% right_join(band_instruments_4rows)
Joining, by = "name"
# A tibble: 6 x 3
  name  band    plays 
  <chr> <chr>   <chr> 
1 John  Beatles guitar
2 Paul  Beatles bass  
3 Paul  Beatles vocals
4 Paul  Wings   bass  
5 Paul  Wings   vocals
6 Keith NA      guitar
```

### full_join:

```r
> band_members_4rows %>% full_join(band_instruments_4rows)
Joining, by = "name"
# A tibble: 7 x 3
  name  band    plays 
  <chr> <chr>   <chr> 
1 Mick  Stones  NA    
2 John  Beatles guitar
3 Paul  Beatles bass  
4 Paul  Beatles vocals
5 Paul  Wings   bass  
6 Paul  Wings   vocals
7 Keith NA      guitar
```