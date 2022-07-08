# CPSC 375 Summer 2022 Homework 2 (needs to be updated)

## Homework 2

Team: Jacob Levi Ursenbach

Prepare your answers as a **single PDF file**.

**Group work**: You may work in groups of 1-3. Include all group member names in the PDF file. Only one person in the group should submit to Canvas.

**Due**: check on Canvas.

## **1.** Explore and identify any “interesting” dataset from [https://www.data.gov/](https://www.data.gov/) …

the home of the US government’s Open Data initiative. Browse the different topics and pick any dataset that (1) looks interesting to you, and (2) is in tabular format (e.g., a CSV file, or multiple zipped CSV files). For this dataset, provide the following information:

1. Provide the URL to the data page
    
    ```r
    # "downloadURL": "https://studentaid.ed.gov/sites/default/files/fsawg/datacenter/library/SummarybySchoolType.xls"
    
    ```
    
2. Briefly describe the dataset (e.g., where did the data come from, why was it collected)
    
    ```r
    # This data was collected by the department of education, 
    # to record student aid grant dispursements by school type over a 10 year period
    ```
    
3. Briefly describe the format of the data (you do not have to include any R code for this question):
    1. What is the file format(s)?
        
        ```r
        # The files were provided in a .xml format, for use with microsoft excel 
        ```
        
    2. Number of tables
        
        ```r
        # There were 12 tables, each representing a fiscal year
        ```
        
    3. Number of rows/columns in the tables
        
        ```r
        # each table consisted of 2 columns and 5 rows
        ```
        
    4. Any other relevant information
        
        ```r
        # Fiscal year 2021 has incomplete information as the fiscal year is incomplete.
        Proprietary schools are for profit schools
        
        ```
        
4. What could be some interesting information that could be extracted from this dataset? Describe in a few sentences.
    
    ```r
    # This data could be most useful when combined with other datasets. You’ll see for example that public institutions take roughly 48-51% of the loan and grant dispursement volume.  If you combine this with an outside dataset you can see that this percentage is skewed, as much more than 50% of students in the USA are pursuing higher education. 
    
    # Another interesting fact was that the percentage of grant and loan volume going to for profit schools has consistently dropped over the last 12 years, from 23 to rougly 1- percent. 
    
    # Again, none of this is that useful unless combined with other data sets.
    ```
    

## **2.** Load the nycflights13 library

(will have to install the nycflights13 package first) which contains flight arrival and departure data in a table called flights. Apply the tidyverse’s data wrangling verbs to answer these questions. For each question, **give only the (one line as a data pipeline) R code beginning with flights %>% …**.

```r
# Setup:
> install.packages("nycflights13")
> library(tidyverse)
> fl <- nycflights13::flights
# examining dataset
> summary(fl)
      year          month             day           dep_time    sched_dep_time
 Min.   :2013   Min.   : 1.000   Min.   : 1.00   Min.   :   1   Min.   : 106  
 1st Qu.:2013   1st Qu.: 4.000   1st Qu.: 8.00   1st Qu.: 907   1st Qu.: 906  
 Median :2013   Median : 7.000   Median :16.00   Median :1401   Median :1359  
 Mean   :2013   Mean   : 6.549   Mean   :15.71   Mean   :1349   Mean   :1344  
 3rd Qu.:2013   3rd Qu.:10.000   3rd Qu.:23.00   3rd Qu.:1744   3rd Qu.:1729  
 Max.   :2013   Max.   :12.000   Max.   :31.00   Max.   :2400   Max.   :2359  
                                                 NA's   :8255                 
   dep_delay          arr_time    sched_arr_time   arr_delay       
 Min.   : -43.00   Min.   :   1   Min.   :   1   Min.   : -86.000  
 1st Qu.:  -5.00   1st Qu.:1104   1st Qu.:1124   1st Qu.: -17.000  
 Median :  -2.00   Median :1535   Median :1556   Median :  -5.000  
 Mean   :  12.64   Mean   :1502   Mean   :1536   Mean   :   6.895  
 3rd Qu.:  11.00   3rd Qu.:1940   3rd Qu.:1945   3rd Qu.:  14.000  
 Max.   :1301.00   Max.   :2400   Max.   :2359   Max.   :1272.000  
 NA's   :8255      NA's   :8713                  NA's   :9430      
   carrier              flight       tailnum             origin         
 Length:336776      Min.   :   1   Length:336776      Length:336776     
 Class :character   1st Qu.: 553   Class :character   Class :character  
 Mode  :character   Median :1496   Mode  :character   Mode  :character  
                    Mean   :1972                                        
                    3rd Qu.:3465                                        
                    Max.   :8500                                        
                                                                        
     dest              air_time        distance         hour           minute     
 Length:336776      Min.   : 20.0   Min.   :  17   Min.   : 1.00   Min.   : 0.00  
 Class :character   1st Qu.: 82.0   1st Qu.: 502   1st Qu.: 9.00   1st Qu.: 8.00  
 Mode  :character   Median :129.0   Median : 872   Median :13.00   Median :29.00  
                    Mean   :150.7   Mean   :1040   Mean   :13.18   Mean   :26.23  
                    3rd Qu.:192.0   3rd Qu.:1389   3rd Qu.:17.00   3rd Qu.:44.00  
                    Max.   :695.0   Max.   :4983   Max.   :23.00   Max.   :59.00  
                    NA's   :9430                                                  
   time_hour                  
 Min.   :2013-01-01 05:00:00  
 1st Qu.:2013-04-04 13:00:00  
 Median :2013-07-03 10:00:00  
 Mean   :2013-07-03 05:22:54  
 3rd Qu.:2013-10-01 07:00:00  
 Max.   :2013-12-31 23:00:00
> nrow(fl)
[1] 336776
> ncol(fl)
[1] 19
> names(fl)
 [1] "year"           "month"          "day"            "dep_time"      
 [5] "sched_dep_time" "dep_delay"      "arr_time"       "sched_arr_time"
 [9] "arr_delay"      "carrier"        "flight"         "tailnum"       
[13] "origin"         "dest"           "air_time"       "distance"      
[17] "hour"           "minute"         "time_hour"
> str(fl)
tibble [336,776 x 19] (S3: tbl_df/tbl/data.frame)
 $ year          : int [1:336776] 2013 2013 2013 2013 2013 2013 2013 2013 2013 2013 ...
 $ month         : int [1:336776] 1 1 1 1 1 1 1 1 1 1 ...
 $ day           : int [1:336776] 1 1 1 1 1 1 1 1 1 1 ...
 $ dep_time      : int [1:336776] 517 533 542 544 554 554 555 557 557 558 ...
 $ sched_dep_time: int [1:336776] 515 529 540 545 600 558 600 600 600 600 ...
 $ dep_delay     : num [1:336776] 2 4 2 -1 -6 -4 -5 -3 -3 -2 ...
 $ arr_time      : int [1:336776] 830 850 923 1004 812 740 913 709 838 753 ...
 $ sched_arr_time: int [1:336776] 819 830 850 1022 837 728 854 723 846 745 ...
 $ arr_delay     : num [1:336776] 11 20 33 -18 -25 12 19 -14 -8 8 ...
 $ carrier       : chr [1:336776] "UA" "UA" "AA" "B6" ...
 $ flight        : int [1:336776] 1545 1714 1141 725 461 1696 507 5708 79 301 ...
 $ tailnum       : chr [1:336776] "N14228" "N24211" "N619AA" "N804JB" ...
 $ origin        : chr [1:336776] "EWR" "LGA" "JFK" "JFK" ...
 $ dest          : chr [1:336776] "IAH" "IAH" "MIA" "BQN" ...
 $ air_time      : num [1:336776] 227 227 160 183 116 150 158 53 140 138 ...
 $ distance      : num [1:336776] 1400 1416 1089 1576 762 ...
 $ hour          : num [1:336776] 5 5 5 5 6 5 6 6 6 6 ...
 $ minute        : num [1:336776] 15 29 40 45 0 58 0 0 0 0 ...
 $ time_hour     : POSIXct[1:336776], format: "2013-01-01 05:00:00" "2013-01-01 05:00:00" ...

```

1. List data only for flights that departed on February 12, 2013.
    
    ```r
    > flights %>% filter(carrier == "UA" | carrier == "AA" | carrier == "DL")
    # this code gives the same output: 
    > flights %>% filter(carrier == c("UA", "AA", "DL"))
    
    # A tibble: 139,504 x 19
        year month   day dep_time sched_dep_time
       <int> <int> <int>    <int>          <int>
     1  2013     1     1      517            515
     2  2013     1     1      533            529
     3  2013     1     1      542            540
     4  2013     1     1      554            600
     5  2013     1     1      554            558
     6  2013     1     1      558            600
     7  2013     1     1      558            600
     8  2013     1     1      558            600
     9  2013     1     1      559            600
    10  2013     1     1      559            600
    # ... with 139,494 more rows, and 14 more
    #   variables: dep_delay <dbl>, arr_time <int>,
    #   sched_arr_time <int>, arr_delay <dbl>,
    #   carrier <chr>, flight <int>, tailnum <chr>,
    #   origin <chr>, dest <chr>, air_time <dbl>,
    #   distance <dbl>, hour <dbl>, minute <dbl>,
    #   time_hour <dttm>
    ```
    
2. List data only for flights that were delayed (both arrival and departure) by more than 2 hours.
    
    ```r
    > flights %>% filter(dep_delay > 2, arr_delay > 2)
    # A tibble: 84,307 x 19
        year month   day dep_time sched_dep_time
       <int> <int> <int>    <int>          <int>
     1  2013     1     1      533            529
     2  2013     1     1      608            600
     3  2013     1     1      611            600
     4  2013     1     1      613            610
     5  2013     1     1      623            610
     6  2013     1     1      632            608
     7  2013     1     1      709            700
     8  2013     1     1      732            645
     9  2013     1     1      743            730
    10  2013     1     1      743            730
    # ... with 84,297 more rows, and 14 more variables:
    #   dep_delay <dbl>, arr_time <int>,
    #   sched_arr_time <int>, arr_delay <dbl>,
    #   carrier <chr>, flight <int>, tailnum <chr>,
    #   origin <chr>, dest <chr>, air_time <dbl>,
    #   distance <dbl>, hour <dbl>, minute <dbl>,
    #   time_hour <dttm>
    ```
    
3. List data only for flights that were delayed (either arrival or departure) by more than 2 hours.
    
    ```r
    > flights %>% filter(dep_delay > 2 | arr_delay > 2)
    # A tibble: 152,938 x 19
        year month   day dep_time sched_dep_time
       <int> <int> <int>    <int>          <int>
     1  2013     1     1      517            515
     2  2013     1     1      533            529
     3  2013     1     1      542            540
     4  2013     1     1      554            558
     5  2013     1     1      555            600
     6  2013     1     1      558            600
     7  2013     1     1      558            600
     8  2013     1     1      559            600
     9  2013     1     1      600            600
    10  2013     1     1      602            605
    # ... with 152,928 more rows, and 14 more
    #   variables: dep_delay <dbl>, arr_time <int>,
    #   sched_arr_time <int>, arr_delay <dbl>,
    #   carrier <chr>, flight <int>, tailnum <chr>,
    #   origin <chr>, dest <chr>, air_time <dbl>,
    #   distance <dbl>, hour <dbl>, minute <dbl>,
    #   time_hour <dttm>
    ```
    
4. List data only for flights that were operated by United, American, or Delta.
    
    ```r
    > flights %>% filter(carrier == "UA" | carrier == "AA" | carrier == "DL")
    # this code gives the same output: 
    > flights %>% filter(carrier == c("UA", "AA", "DL"))
    
    # A tibble: 139,504 x 19
        year month   day dep_time sched_dep_time
       <int> <int> <int>    <int>          <int>
     1  2013     1     1      517            515
     2  2013     1     1      533            529
     3  2013     1     1      542            540
     4  2013     1     1      554            600
     5  2013     1     1      554            558
     6  2013     1     1      558            600
     7  2013     1     1      558            600
     8  2013     1     1      558            600
     9  2013     1     1      559            600
    10  2013     1     1      559            600
    # ... with 139,494 more rows, and 14 more
    #   variables: dep_delay <dbl>, arr_time <int>,
    #   sched_arr_time <int>, arr_delay <dbl>,
    #   carrier <chr>, flight <int>, tailnum <chr>,
    #   origin <chr>, dest <chr>, air_time <dbl>,
    #   distance <dbl>, hour <dbl>, minute <dbl>,
    #   time_hour <dttm>
    ```
    
5. Sort data in order of fastest flights (air_time).
    
    ```r
    > flights %>% arrange(air_time)
    # A tibble: 336,776 x 19
        year month   day dep_time sched_dep_time
       <int> <int> <int>    <int>          <int>
     1  2013     1    16     1355           1315
     2  2013     4    13      537            527
     3  2013    12     6      922            851
     4  2013     2     3     2153           2129
     5  2013     2     5     1303           1315
     6  2013     2    12     2123           2130
     7  2013     3     2     1450           1500
     8  2013     3     8     2026           1935
     9  2013     3    18     1456           1329
    10  2013     3    19     2226           2145
    # ... with 336,766 more rows, and 14 more
    #   variables: dep_delay <dbl>, arr_time <int>,
    #   sched_arr_time <int>, arr_delay <dbl>,
    #   carrier <chr>, flight <int>, tailnum <chr>,
    #   origin <chr>, dest <chr>, air_time <dbl>,
    #   distance <dbl>, hour <dbl>, minute <dbl>,
    #   time_hour <dttm>
    ```
    
6. Sort data in order of longest duration flights (air_time).
    
    ```r
    > flights %>% arrange(air_time)
    # A tibble: 336,776 x 19
        year month   day dep_time sched_dep_time
       <int> <int> <int>    <int>          <int>
     1  2013     1    16     1355           1315
     2  2013     4    13      537            527
     3  2013    12     6      922            851
     4  2013     2     3     2153           2129
     5  2013     2     5     1303           1315
     6  2013     2    12     2123           2130
     7  2013     3     2     1450           1500
     8  2013     3     8     2026           1935
     9  2013     3    18     1456           1329
    10  2013     3    19     2226           2145
    # ... with 336,766 more rows, and 14 more
    #   variables: dep_delay <dbl>, arr_time <int>,
    #   sched_arr_time <int>, arr_delay <dbl>,
    #   carrier <chr>, flight <int>, tailnum <chr>,
    #   origin <chr>, dest <chr>, air_time <dbl>,
    #   distance <dbl>, hour <dbl>, minute <dbl>,
    #   time_hour <dttm>
    ```
    
7. Show only the origin and destination of flights sorted by longest flights.
    
    ```r
    > flights %>% arrange(-air_time) %>% select(origin, dest)
    # A tibble: 336,776 x 2
       origin dest 
       <chr>  <chr>
     1 EWR    HNL  
     2 JFK    HNL  
     3 JFK    HNL  
     4 JFK    HNL  
     5 JFK    HNL  
     6 JFK    HNL  
     7 EWR    HNL  
     8 JFK    HNL  
     9 JFK    HNL  
    10 EWR    HNL  
    # ... with 336,766 more rows
    ```
    
8. Add a new variable that indicates the total delay (both departure and arrival delay).
    
    ```r
    > flights %>% mutate(TotalDelay = dep_delay+arr_delay)
    # A tibble: 336,776 x 20
        year month   day dep_time sched_dep_time
       <int> <int> <int>    <int>          <int>
     1  2013     1     1      517            515
     2  2013     1     1      533            529
     3  2013     1     1      542            540
     4  2013     1     1      544            545
     5  2013     1     1      554            600
     6  2013     1     1      554            558
     7  2013     1     1      555            600
     8  2013     1     1      557            600
     9  2013     1     1      557            600
    10  2013     1     1      558            600
    # ... with 336,766 more rows, and 15 more
    #   variables: dep_delay <dbl>, arr_time <int>,
    #   sched_arr_time <int>, arr_delay <dbl>,
    #   carrier <chr>, flight <int>, tailnum <chr>,
    #   origin <chr>, dest <chr>, air_time <dbl>,
    #   distance <dbl>, hour <dbl>, minute <dbl>,
    #   time_hour <dttm>, TotalDelay <dbl>
    
    # ---------------------------------------------------------
    # showing the new column:
    > flights %>% mutate(TotalDelay = dep_delay+arr_delay) %>% select(TotalDelay)
    # A tibble: 336,776 x 1
       TotalDelay
            <dbl>
     1         13
     2         24
     3         35
     4        -19
     5        -31
     6          8
     7         14
     8        -17
     9        -11
    10          6
    # ... with 336,766 more rows
    ```
    
9. Show only the origin and destination of flights sorted by descending order of total delay.
    
    ```r
    > flights %>% mutate(TotalDelay = dep_delay+arr_delay) %>% arrange(TotalDelay) %>% select(origin,dest)
    # A tibble: 336,776 x 2
       origin dest 
       <chr>  <chr>
     1 EWR    SFO  
     2 JFK    SFO  
     3 LGA    MSY  
     4 JFK    PHX  
     5 JFK    MKE  
     6 EWR    SFO  
     7 EWR    SEA  
     8 JFK    MCI  
     9 LGA    DEN  
    10 LGA    DSM  
    # ... with 336,766 more rows
    ```
    
10. Show only the origin and destination of 10 most delayed flights [Hint: there are multiple ways of solving this. Some additional functions that you will find useful are head(), slice(), min_rank().]
    
    ```r
    > flights %>% mutate(TotalDelay = dep_delay+arr_delay) %>% arrange(TotalDelay) %>% select(origin,dest) %>% slice(1:10)
    # A tibble: 10 x 2
       origin dest 
       <chr>  <chr>
     1 EWR    SFO  
     2 JFK    SFO  
     3 LGA    MSY  
     4 JFK    PHX  
     5 JFK    MKE  
     6 EWR    SFO  
     7 EWR    SEA  
     8 JFK    MCI  
     9 LGA    DEN  
    10 LGA    DSM
    ```
    
11. Show the average total delay for all flights
    
    ```r
    > flights %>% mutate(TotalDelay = dep_delay+arr_delay) %>% group_by(origin) %>% summarize(mean(TotalDelay, na.rm = TRUE))
    # A tibble: 3 x 2
      origin `mean(TotalDelay, na.rm = TRUE)`
      <chr>                             <dbl>
    1 EWR                                24.1
    2 JFK                                17.6
    3 LGA                                16.1
    ```
    
12. Show the average total delay for every departure city.
    
    ```r
    > flights %>% mutate(TotalDelay = dep_delay+arr_delay) %>% group_by(origin, dest) %>% summarize(mean(TotalDelay, na.rm = TRUE))
    `summarise()` has grouped output by 'origin'. You
    can override using the `.groups` argument.
    # A tibble: 224 x 3
    # Groups:   origin [3]
       origin dest  `mean(TotalDelay, na.rm = TRUE)`
       <chr>  <chr>                            <dbl>
     1 EWR    ALB                               37.8
     2 EWR    ANC                               10.4
     3 EWR    ATL                               28.6
     4 EWR    AUS                               11  
     5 EWR    AVL                               17.4
     6 EWR    BDL                               24.8
     7 EWR    BNA                               30.3
     8 EWR    BOS                               17.3
     9 EWR    BQN                               34.5
    10 EWR    BTV                               30.0
    # ... with 214 more rows
    
    ```
    
13. Show the average total delay for every departure-arrival city pair.
    
    ```r
    
    ```
    

## **3.** Consider the two tables shown below called *bands* and *instruments*.

bands:

| name | lastname | band | year |
| --- | --- | --- | --- |
| Mick | Jagger | Stones | 1962 |
| John | Lennon | Beatles | 1960 |
| Paul | McCartney | Beatles | 1960 |
| Paul | McCartney | Wings | 1971 |

instruments:

| artist | artistname | plays | model |
| --- | --- | --- | --- |
| John | Lennon | guitar | Gibson |
| Paul | McCartney | bass | Hofner |
| Keith | Richards | guitar | Fender |
| Paul | McCartney | bass | Hofner |

Draw the output table from the following operations (you should be able to calculate the output by hand though you may use R to check your answers).

checking answers with r: 
Creating tables:

```r
> bands <- data.frame(name=c("Mick","John","Paul","Paul"), lastname=c("Jagger","Lennon","McCartney","McCartney"),band=c("Stones","Beatles","Beatles","Wings"),year=c("1962","1960","1960","1971"))
> instruments <- data.frame(artist=c("John","Paul","Keith","Paul"),artistname=c("Lennon","McCartney","Richards","McCartney"),plays=c("guitar","bass","guitar","bass"),model=c("Gibson","Hofner","Fender","Hofner"))
> bands
  name  lastname    band year
1 Mick    Jagger  Stones 1962
2 John    Lennon Beatles 1960
3 Paul McCartney Beatles 1960
4 Paul McCartney   Wings 1971
> instruments
  artist artistname  plays  model
1   John     Lennon guitar Gibson
2   Paul  McCartney   bass Hofner
3  Keith   Richards guitar Fender
4   Paul  McCartney   bass Hofner
```

1. bands %>% inner_join(instruments) [Hint: this is a trick question!]
    
    ```r
    > q1 <- bands %>% inner_join(instruments)
    Error in `inner_join()`:
    ! `by` must be supplied when `x` and `y` have no common variables.
    i use by = character()` to perform a cross-join.
    ```
    
    1. columns don’t have common variables
2. bands %>% inner_join(instruments, by=c(name="artist"))
    
    ```r
    > q2 <- bands %>% inner_join(instruments, by=c(name="artist"))
    > q2
      name  lastname    band year artistname  plays  model
    1 John    Lennon Beatles 1960     Lennon guitar Gibson
    2 Paul McCartney Beatles 1960  McCartney   bass Hofner
    3 Paul McCartney Beatles 1960  McCartney   bass Hofner
    4 Paul McCartney   Wings 1971  McCartney   bass Hofner
    5 Paul McCartney   Wings 1971  McCartney   bass Hofner
    ```
    
3. bands %>% inner_join(instruments, by=c(name="artist", lastname="artistname"))
    
    ```r
    > q3 <- bands %>% inner_join(instruments, by=c(name="artist", lastname="artistname"))
    > q3
      name  lastname    band year  plays  model
    1 John    Lennon Beatles 1960 guitar Gibson
    2 Paul McCartney Beatles 1960   bass Hofner
    3 Paul McCartney Beatles 1960   bass Hofner
    4 Paul McCartney   Wings 1971   bass Hofner
    5 Paul McCartney   Wings 1971   bass Hofner
    ```
    
4. bands %>% left_join(instruments, by=c(name="artist", lastname="artistname"))
    
    ```r
    > q4 <- bands %>% left_join(instruments, by=c(name="artist", lastname="artistname"))
    > q4
      name  lastname    band year  plays  model
    1 Mick    Jagger  Stones 1962   <NA>   <NA>
    2 John    Lennon Beatles 1960 guitar Gibson
    3 Paul McCartney Beatles 1960   bass Hofner
    4 Paul McCartney Beatles 1960   bass Hofner
    5 Paul McCartney   Wings 1971   bass Hofner
    6 Paul McCartney   Wings 1971   bass Hofner
    ```
    
5. bands %>% inner_join(instruments, by=c(name="artist", lastname="artistname", year="plays"))
    
    ```r
    > q5 <- bands %>% inner_join(instruments, by=c(name="artist", lastname="artistname", year="plays"))
    > q5
    [1] name     lastname band     year     model   
    <0 rows> (or 0-length row.names)
    ```
    

## **4.** Consider the billboard dataset that is supplied with the tidyverse which shows the Billboard top 100 song rankings in the year 2000.

Apply the tidyverse’s data wrangling verbs to answer these questions. For each question, **give only the code**.

1. Show for each track, how many weeks it spent on the chart

2. List tracks in decreasing order of number of weeks spent on the chart

3. Show for each track, its top rank

4. List tracks in increasing order of its top rank

5. Show for each artist, its top rank

6. List artists in increasing order of their top rank

7. List tracks that only spent one week in the charts

8. List tracks that only spent one week in the charts along with its artist

**Hint**: First, convert to a tidy table. Show code for this step. All the above questions can then be answered with a single data pipeline.

## **5.** Consider the .csv file in the Datasets module on Canvas,

“insurance_premiums.csv,” which contains the Average Annual Single Premium per Enrolled Employee For Employer-Based Health Insurance

| Location | 2013__Employee_Contribution | 2013__Employer_Contribution | ... | 2018__Employee_Contribution | 2018__Employer_Contribution |
| --- | --- | --- | --- | --- | --- |
| United States | 1170 | 4401 | ... | 1427 | 5288 |
| Alabama | 1379 | 3825 | ... | 1453 | 4636 |
| Alaska | 1078 | 6291 | ... | 1154 | 7278 |

The first few rows are shown above.

1. The data is not “tidy”. In 2-3 sentences, explain why.

```r
Years repeat multiple times, wile employee and employer contribution  has en split into many columns. You should combine the data, so that all of it sits in a more sussinct and organized manner. 
```

The goal is to convert this dataset to the tidy format shown below. You will solve this in two different ways in (b) and (c)

| Location | Year | Employee_Contribution | Employer_Contribution |
| --- | --- | --- | --- |
| United States | 2013 | 1170 | 4401 |
| United States | 2014 | 1234 | 4598 |
| United States | 2015 | 1255 | 4708 |
| United States | 2016 | 1325 | 4776 |
| United States | 2017 | 1415 | 4953 |
| United States | 2018 | 1427 | 5288 |
| Alabama | 2013 | 1379 | 3825 |
| Alabama | 2014 | 1362 | 4164 |
| Alabama | 2015 | 1228 | 4505 |
| Alabama | 2016 | 1510 | 4026 |
| Alabama | 2017 | 1593 | 4482 |
| Alabama | 2018 | 1453 | 4636 |
1. **Approach 1:** Pivot and separate the two sets of columns (Employee_Contribution, Employer_Contribution) and create two temporary tables. Then join the two tables. Specifically, do the following steps. *Show your code for each step and any summary output from the code.*
    1. Read the .csv file using **read_csv** (NOT read.csv) and store it in a table.
    2. Select only the *Location* column and the columns containing the word *Employee*
    3. Pivot the data in the *Employee* columns into a pair of names_to and values_to columns called *Year* and *Employee_Contribution*
    4. The Year column has values such as 2013__Employee_Contribution. It should contain only the year (e.g., 2013). Use separate() to separate the values into the year component and discard the remaining portion. [Hint: use “__” as the separator. Specifying NA in the into parameter discards the variable.]
    5. Store the result of the above pipeline in a table.
    6. Repeat the above steps for the “Employer” columns and store the result in another table.
    7. Join the two tables. Check that the resulting table matches the desired tidy format.
2. **Approach 2:** Pivot **all** columns into **two** names_to columns, then pivot again! Specifically, do the following steps. *Show your code for each step.*
    1. Read the .csv file using **read_csv** (NOT read.csv) and store it in a table.
    2. Pivot_longer *all* columns (except Location) into *two* names_to columns. This requires a names_sep to be specified. Read the help for pivot_longer().
    3. Pivot_wider a pair of columns from the previous step. Check that the resulting table matches the desired tidy format.