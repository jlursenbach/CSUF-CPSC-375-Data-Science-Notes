# Data Science Covid Project

## Project Requirements

[https://lh4.googleusercontent.com/gFeIdmjPTeLKqe7NUDHK4iurdr_cA9lfMJuDV1s6c7PCaQVhWFJC33foMj-rGQHzr_I6X8c7PC7YMboVWgzFBdiyWNjQgEO3MS48CJpTS4C9B5MK1nKMdox51q0zfbhHWoJezoy5yfdSVUIGmw](https://lh4.googleusercontent.com/gFeIdmjPTeLKqe7NUDHK4iurdr_cA9lfMJuDV1s6c7PCaQVhWFJC33foMj-rGQHzr_I6X8c7PC7YMboVWgzFBdiyWNjQgEO3MS48CJpTS4C9B5MK1nKMdox51q0zfbhHWoJezoy5yfdSVUIGmw)

Image from: [https://fortune.com/2021/09/22/covid-vaccine-rate-world-us-latest-update-coronavirus-vaccines/](https://fortune.com/2021/09/22/covid-vaccine-rate-world-us-latest-update-coronavirus-vaccines/)

COVID vaccination rates vary a great deal between countries. There are several reasons, including economics (richer countries tend to have higher rates) and demographics (countries prioritize recipients by age). The goal of this project is to use linear regression to model the vaccination rates in different countries in terms of their GDP (a measure of economic output) and demographics.

## Datasets

1. [time_series_covid19_vaccine_doses_admin_global.csv](https://raw.githubusercontent.com/govex/COVID-19/master/data_tables/vaccine_data/global_data/time_series_covid19_vaccine_doses_admin_global.csv)
    1. This file contains the number of vaccine doses given every day in different countries. Note that you can read the “raw” CSV file from a URL directly, like so:
        
        ```r
        read.csv("[https://raw.githubusercontent.com/govex/COVID-19/master/data_tables/vaccine_data/global_data/time_series_covid19_vaccine_doses_admin_global.csv](https://raw.githubusercontent.com/govex/COVID-19/master/data_tables/vaccine_data/global_data/time_series_covid19_vaccine_doses_admin_global.csv)")
        ```
        
2. GDP data in API_NY.GDP.MKTP.CD_DS2_en_csv_v2_3011433.csv
    1. This file (available in the Datasets module on Canvas) contains the GDP of different countries in different years. You will use only the GDP from *the most recent year for a country*.
3. demographics.csv
    1. This gives the proportion of a country’s population in different age groups and some other demographic data such as mortality rates and expected lifetime.

## Hints

There are two major steps in this project:

### **Data preparation/wrangling** to get all the data into **one table** that can be used for linear modeling

1. reading the data files using read_csv()
2. Removing unneeded rows (e.g., countries like Brazil and India report Province_State-level data that is not needed as we are studying only country-level rates) and columns.
3. tidying tables, as needed. For example, the vaccination data is not tidy.
4. Calculate the vaccination rate: vaccinations/population
5. Since the most important factor affecting vaccination rate is the number of days since vaccination began (vaccination rate always increases), calculate a variable that is: number of days since first non-zero vaccination number. This variable will be important for modeling.
6. Discard data that is not needed. For example, only the GDP of the most recent year is necessary.
7. You can ignore sex-related differences in demographics in this project, so add the male/female population numbers together.
8. Merge all tables (Hint: Join using the 3-letter ISO code for a country)

At the end of these steps, the data should be in one table, in a format ready for linear regression (similar to what is shown below):

![Untitled](Data%20Science%20Covid%20Project%208bdc31914df04f5387cbf35a8994bbff/Untitled.png)

### **Linear modeling the Covid vaccination rate**

Make a list of all predictor variables that are available. The challenge is to identify which combination of these predictors will give the best predictive model. You should also try transforming some of the variables (e.g., transforming population counts to proportion of total population). Run linear regression with **at least 5 different combinations of predictor variables.**

> Note: ***each day*** becomes one data point, i.e., the vaccination rate is calculated for each day for each country. The number of vaccinations should *not* be used as an independent variable as this is essentially what you are predicting.
> 

## Submission:

Due: Wednesday 6/29. Please submit:

### A short report describing your data wrangling steps and the different combinations of predictor variables you tried, and any variable transforms. [A PDF file]

- The report should include the following plots:
    1. a scatterplot of only the most recent vaccination rate for every country and the number of days since first vaccination, like:
        
        [https://lh4.googleusercontent.com/FjxFVCBxlrmFfsnTXe0etS40ZZM6g9M50UbPqQ_zS6TjaKfcmdiqn5-jOIAaDF-sYOfc69Cygytaau5ejKY-H4FdMmfmzE1ujIZc16-4P0-G8YaK_L1VMPrFgwXyf1j1Sb4BUvle_O74SBYHng](https://lh4.googleusercontent.com/FjxFVCBxlrmFfsnTXe0etS40ZZM6g9M50UbPqQ_zS6TjaKfcmdiqn5-jOIAaDF-sYOfc69Cygytaau5ejKY-H4FdMmfmzE1ujIZc16-4P0-G8YaK_L1VMPrFgwXyf1j1Sb4BUvle_O74SBYHng)
        
    2. a summary bar graph with the R2 values on the y-axis and a corresponding model name on the x-axis (include all the different models you tried). It will look somewhat like this:
        
        [https://lh6.googleusercontent.com/zn8ibCB81LqJvSf1Y9NIhmis_V5jyBr2RPtQuZbDRs5bycFDVHZeIRsJfH0JQwUa_ezkdQAchU8xOASv4MuVtTNxPr2DLIMQdiBjtIE_ETqGLlFqSkNhXcNTtwZRcY4bHXEuvQ-heF8_mavTyQ](https://lh6.googleusercontent.com/zn8ibCB81LqJvSf1Y9NIhmis_V5jyBr2RPtQuZbDRs5bycFDVHZeIRsJfH0JQwUa_ezkdQAchU8xOASv4MuVtTNxPr2DLIMQdiBjtIE_ETqGLlFqSkNhXcNTtwZRcY4bHXEuvQ-heF8_mavTyQ)
        
    - There should be a conclusion that describes in words the implication of your most accurate model.

### A listing of your R code in one file [.R file]

## Project checklist/grading rubric

### Data wrangling

1. Code to load and wrangle vaccinations data
    
    ```r
    > global <- read_csv("[https://raw.githubusercontent.com/govex/COVID-19/master/data_tables/vaccine_data/global_data/time_series_covid19_vaccine_doses_admin_global.csv](https://raw.githubusercontent.com/govex/COVID-19/master/data_tables/vaccine_data/global_data/time_series_covid19_vaccine_doses_admin_global.csv)")
    > dataSet1 <- global %>% select(-c(1,2,4,5,6,7,9,10,11))
    > dataSet1 <- dataSet1 %>% pivot_longer(4:559, names_to = "Year-Month-Day", values_to="vaccinations", values_drop_na = TRUE)
    > dataSet1 <- dataSet1 %>% mutate(vacRate = vaccinations/Population)> dataSet1 %>% filter(vaccinations 
    > 0) %>% group_by(Country_Region) %>% mutate(daysSinceStart= row_number())
    ```
    
2. Code to load and wrangle hospital beds data
    
    ```r
    > GDP <- read_csv("API_NY.GDP.MKTP.CD_DS2_en_csv_v2_3011433.csv")
    ```
    
3. Code to load and wrangle demographics data>
    
    ```r
    demographics <- read_csv("demographics.csv")
    ```
    
4. Code to join datasets to one table
    
    ```r
    
    ```
    

### Modeling

1. Tried at least 5 different combinations of variables for modeling
2. Tried some variable transformations
3. Code that correctly implements the model

### Written report

1. Brief descriptions of the data wrangling steps
2. Brief description of how variables were chosen for data modeling
3. Description of variable transformations
4. A scatterplot of most recent vaccination rates for different countries
5. A plot that shows the R2 values of the different models
6. A conclusion – what does your modeling say about vaccination rates (e.g., what are the significant factors and what are not)
7. Clarity of the report (e.g., appropriate section headings)
8. Group member names

### Code

1. Style: readability, use of tidyverse, unnecessary use of complex functions.
2. Code has adequate comments
3. Note: include only the final code, i.e., do not submit just the RStudio history

# Konnor’s Attempt

1. **Data preparation/wrangling** to get all the data into **one table** that can be used for linear modeling
    1. reading the data files using read_csv()
    
    ```r
    # Set working Directory
    setwd("~/Downloads/CPSC 375 Project 1")
    
    # read vaccination data in
    vaccines <- read_csv("https://raw.githubusercontent.com/govex/COVID-19/master/data_tables/vaccine_data/global_data/time_series_covid19_vaccine_doses_admin_global.csv")
    
    # read GDP data in
    gdp <- read_csv("gdp.csv")
    
    # read demographic data in. *Note* file was renamed for simplicity
    demo <- read_csv("demographics.csv")
    ```
    
2. Removing unneeded rows (e.g., countries like Brazil and India report Province_State-level data that is not needed as we are studying only country-level rates) and columns.
    
    ```r
    # removing province states and places with 0 population
    vaccines <- vaccines %>% filter(Population >= 0, is.na(Province_State))
    
    # removing unnecessary columns
    vaccines <- vaccines %>% select(-Admin2, -FIPS, -Province_State, -UID, -iso2,-code3, -Lat, -Long_, -Combined_Key)
    
    # removing unnecessary columns
    demo <- demo %>% select(-`Series Name`)
    ```
    
3. tidying tables, as needed. For example, the vaccination data is not tidy.
    
    ```r
    # tidying vaccine table to show iso3, country, population, date of vaccine, shots.
    vaccines <- vaccines %>% pivot_longer(-c(Country_Region, Population, iso3), names_to = "date", values_to = "shots") %>% view()
    
    # removing any days where any given country didnt start vaccinating yet
    
    vaccines <- vaccines %>% filter(shots > 0) %>% view()
    
    # pivot_wider to get all demo data tidy
    
    demo <- demo %>% pivot_wider(names_from = `Series Code`, values_from = YR2015)
    ```
    
4. Calculate the vaccination rate: vaccinations/population
    
    ```r
    # add vaccination rate to vaccine table
    
    vaccines <- vaccines %>% mutate(vacRate = shots/Population) %>% view()
    ```
    
5. Since the most important factor affecting vaccination rate is the number of days since vaccination began (vaccination rate always increases), calculate a variable that is: number of days since first non-zero vaccination number. This variable will be important for modeling.
    
    ```r
    # add daysSinceStart column.
    
    vaccines <- vaccines %>% group_by(Country_Region) %>% mutate(daysSinceStart = 1:n()) %>% view()
    ```
    
6. Discard data that is not needed. For example, only the GDP of the most recent year is necessary.
    
    ```r
    # selecting only 2020 and removing NAs
    gdp <- gdp %>% select(c(2,65)) %>% drop_na() %>% view()
    
    #removing unneeded columns and NAs from demo
    demo <- demo %>% select(-1) %>% drop_na() %>% view()
    
    #removing date since we are using since start method, and dropping NAs
    vaccines <- vaccines %>% select(-date) %>% drop_na() %>% view()
    
    ```
    
7. You can ignore sex-related differences in demographics in this project, so add the male/female population numbers together.
    
    ```r
    # combine male and female demos into TOTL column, and dropped the gendered
    cleaneddemo <- demo %>% mutate(SP.POP.80UP.TOTL=SP.POP.80UP.FE+SP.POP.80UP.MA) %>% mutate(SP.POP.1564.IN.TOTL=SP.POP.1564.MA.IN+SP.POP.1564.FE.IN) %>% mutate(SP.POP.0014.IN.TOTL=SP.POP.0014.MA.IN+SP.POP.0014.FE.IN) %>% mutate(SP.DYN.AMRT.TOTL=SP.DYN.AMRT.MA+SP.DYN.AMRT.FE) %>% mutate(SP.POP.TOTL.IN.TOTL=SP.POP.TOTL.FE.IN+SP.POP.TOTL.MA.IN) %>% mutate(SP.POP.65UP.IN.TOTL=SP.POP.65UP.FE.IN+SP.POP.65UP.MA.IN) %>% select(-c(5:16)) %>% view()
    ```
    
8. Merge all tables (Hint: Join using the 3-letter ISO code for a country)
    
    ```r
    #renames 2020 to GDP
    gdp <- gdp %>% rename("GDP" = `2020`)
    
    #renames `Country Code` to iso3 for merge. Could have done iso3 -> country code but wanted to match example in directions
    gdp <- gdp %>% rename("iso3" = `Country Code`)
    cleaneddemo <- cleaneddemo %>% rename("iso3" = `Country Code`) 
    
    #the merge
    cleaneddataset <- vaccines %>% inner_join(gdp) %>% inner_join(cleaneddemo)
    ```
    

### Modeling

clean_data :

[droppedna.csv](Data%20Science%20Covid%20Project%208bdc31914df04f5387cbf35a8994bbff/droppedna.csv)

```r
> str(clean_data)
'data.frame':	55550 obs. of  16 variables:
 $ iso3               : chr  "AFG" "AFG" "AFG" ...
 $ Country_Region     : chr  "Afghanistan" "Afghanistan" "Afghanistan"...
 $ Population         : int  38928341 38928341 38928341...
 $ shots              : num  8200 8200 8200...
 $ vacRate            : num  0.000211 0.000211 0.000211...
 $ daysSinceStart     : int  1 2 3 ...
 $ GDP                : num  1.98e+10 1.98e+10 1.98e+10...
 $ SP.DYN.LE00.IN     : num  63.4 63.4 63.4...
 $ SP.URB.TOTL        : int  8535606 8535606 8535606 ...
 $ SP.POP.TOTL        : int  34413603 34413603 34413603...
 $ SP.POP.80UP.TOTL   : int  85552 85552 85552...
 $ SP.POP.1564.IN.TOTL: int  18116800 18116800 18116800...
 $ SP.POP.0014.IN.TOTL: int  15443807 15443807 15443807...
 $ SP.DYN.AMRT.TOTL   : num  455 455 455 455 455 ...
 $ SP.POP.TOTL.IN.TOTL: int  34413603 34413603 34413603...
 $ SP.POP.65UP.IN.TOTL: int  852996 852996 852996...
```

Static variables:

Country/Region

population

GDP

(What are these?)
sp.dyn.le00.in - life expectancy at birth, total years 

sp.pop.totl - population, total

%%% sp.pop.80up.totl - population ages 80 and up, total

%%% sp.pop.0014.in.totl - population ages 0-14, total

sp.pop.totl.in.totl - male and female population, total

sp.pop.65up.in.totl - population ages 65 and up, total

- we should convert these static values into percentages
- we should group by country and

Changing Variables:

Shots

vacRate

Days Since Start

variable model choices:

x axis GDP: 

per gdp 

graph general vaccination for days since start:

graph the sp. variables

for lowest 10 gdp countries:

for highest 10 gdp countries:

for slowest vaccination rate change:

for highest vaccination rate change:

1. Tried at least 5 different combinations of variables for modeling
2. Tried some variable transformations
3. Code that correctly implements the model

### Written report

1. Brief descriptions of the data wrangling steps
2. Brief description of how variables were chosen for data modeling
3. Description of variable transformations
4. A scatterplot of most recent vaccination rates for different countries
5. A plot that shows the R2 values of the different models
6. A conclusion – what does your modeling say about vaccination rates (e.g., what are the significant factors and what are not)
7. Clarity of the report (e.g., appropriate section headings)
8. Group member names

### Code

1. Style: readability, use of tidyverse, unnecessary use of complex functions.
2. Code has adequate comments
3. Note: include only the final code, i.e., do not submit just the RStudio history

# Jacob’s Attempt

# Cesar’s Attempt

> lifeExpectancy <- lm(formula = vacRate~GDP+SP.DYN.LE00.IN, data=clean_data)
summary(lifeExpectancy)
> 
- Call:
lm(formula = vacRate ~ GDP + [SP.DYN.LE00.IN](http://sp.dyn.le00.in/), data = clean_data)
- Residuals:
Min       1Q   Median       3Q      Max
-1.29899 -0.48354 -0.01506  0.43339  2.02035
- Coefficients:
Estimate Std. Error t value Pr(>|t|)
(Intercept) -2.524e+00 2.804e-02 -90.02 <2e-16 ***
GDP 1.232e-14 1.032e-15 11.93 <2e-16 ***
[SP.DYN.LE00.IN](http://sp.dyn.le00.in/) 4.531e-02 3.814e-04 118.79 <2e-16 ***
- Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
- Residual standard error: 0.6224 on 55547 degrees of freedom
Multiple R-squared:  0.2122,	Adjusted R-squared:  0.2122
F-statistic:  7483 on 2 and 55547 DF,  p-value: < 2.2e-16

> urbanPopulation <- lm(formula = vacRate~SP.URB.TOTL, data=clean_data)
summary(urbanPopulation)
> 
- Call:
lm(formula = vacRate ~ SP.URB.TOTL, data = clean_data)
- Residuals:
Min      1Q  Median      3Q     Max
-1.1666 -0.6567 -0.1434  0.5334  2.3045
- Coefficients:
Estimate Std. Error t value Pr(>|t|)
(Intercept) 7.957e-01 3.131e-03 254.15 <2e-16 ***
SP.URB.TOTL 4.888e-10 3.235e-11 15.11 <2e-16 ***
- Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
- Residual standard error: 0.6998 on 55548 degrees of freedom
Multiple R-squared:  0.004095,	Adjusted R-squared:  0.004077
F-statistic: 228.4 on 1 and 55548 DF,  p-value: < 2.2e-16

> olderThan80 <- lm(formula = vacRate~SP.POP.80UP.TOTL, data=clean_data)
summary(olderThan80)
> 
- Call:
lm(formula = vacRate ~ SP.POP.80UP.TOTL, data = clean_data)
- Residuals:
Min      1Q  Median      3Q     Max
-1.4017 -0.6495 -0.1416  0.5272  2.3103
- Coefficients:
Estimate Std. Error t value Pr(>|t|)
(Intercept) 7.842e-01 3.120e-03 251.35 <2e-16 ***
SP.POP.80UP.TOTL 2.936e-08 1.103e-09 26.61 <2e-16 ***
- Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
- Residual standard error: 0.6968 on 55548 degrees of freedom
Multiple R-squared:  0.01259,	Adjusted R-squared:  0.01257
F-statistic:   708 on 1 and 55548 DF,  p-value: < 2.2e-16

> totalPopulation <- lm(formula = vacRate~SP.POP.TOTL, data=clean_data)
summary(totalPopulation)
> 
- Call:
lm(formula = vacRate ~ SP.POP.TOTL, data = clean_data)
- Residuals:
Min      1Q  Median      3Q     Max
-0.9470 -0.6602 -0.1459  0.5371  2.3012
- Coefficients:
Estimate Std. Error t value Pr(>|t|)
(Intercept) 8.047e-01 3.107e-03 259.035 < 2e-16 ***
SP.POP.TOTL 1.046e-10 1.565e-11 6.682 2.39e-11 ***
- Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
- Residual standard error: 0.701 on 55548 degrees of freedom
Multiple R-squared:  0.000803,	Adjusted R-squared:  0.000785
F-statistic: 44.64 on 1 and 55548 DF,  p-value: 2.387e-11

> ages15to64total <- lm(formula = vacRate~SP.POP.1564.IN.TOTL, data=clean_data)
summary(ages15to64total)
> 
- Call:
lm(formula = vacRate ~ SP.POP.1564.IN.TOTL, data = clean_data)
- Residuals:
Min      1Q  Median      3Q     Max
-0.9953 -0.6593 -0.1451  0.5369  2.3021
- Coefficients:
Estimate Std. Error t value Pr(>|t|)
(Intercept) 8.033e-01 3.096e-03 259.478 <2e-16 ***
SP.POP.1564.IN.TOTL 1.940e-10 2.254e-11 8.604 <2e-16 ***
- Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
- Residual standard error: 0.7008 on 55548 degrees of freedom
Multiple R-squared:  0.001331,	Adjusted R-squared:  0.001313
F-statistic: 74.03 on 1 and 55548 DF,  p-value: < 2.2e-16

> ages0to14total <- lm(formula = vacRate~SP.POP.0014.IN.TOTL, data=clean_data)
summary(ages0to14total)
> 
- Call:
lm(formula = vacRate ~ SP.POP.0014.IN.TOTL, data = clean_data)
- Residuals:
Min      1Q  Median      3Q     Max
-0.8141 -0.6636 -0.1449  0.5405  2.2945
- Coefficients:
Estimate Std. Error t value Pr(>|t|)
(Intercept) 8.142e-01 3.124e-03 260.60 < 2e-16 ***
SP.POP.0014.IN.TOTL -2.425e-10 6.589e-11 -3.68 0.000233 ***
- Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
- Residual standard error: 0.7012 on 55548 degrees of freedom
Multiple R-squared:  0.0002437,	Adjusted R-squared:  0.0002258
F-statistic: 13.54 on 1 and 55548 DF,  p-value: 0.0002334