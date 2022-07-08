# Ursenbach HW 3

Prepare your answers as a **single PDF file**.

1. Consider the “Auto MPG” dataset (available in the Datasets module on Canvas) which “concerns city-cycle fuel consumption in miles per gallon, to be predicted in terms of 3 multivalued discrete and 5 continuous attributes.” The goal is to model mpg given engine displacement and number of cylinders. Answer the following questions.

```r
# import file:
> data = read.csv("autompg.csv")

#inspect data: 
> str(data)
'data.frame':	398 obs. of  9 variables:
 $ mpg         : num  18 15 18 16 17 15 14 14 14 15 ...
 $ cylinders   : int  8 8 8 8 8 8 8 8 8 8 ...
 $ displacement: num  307 350 318 304 302 429 454 440 455 390 ...
 $ horsepower  : int  130 165 150 150 140 198 220 215 225 190 ...
 $ weight      : int  3504 3693 3436 3433 3449 4341 4354 4312 4425 3850 ...
 $ acceleration: num  12 11.5 11 12 10.5 10 9 8.5 10 8.5 ...
 $ model_year  : int  70 70 70 70 70 70 70 70 70 70 ...
 $ origin      : int  1 1 1 1 1 1 1 1 1 1 ...
 $ car_name    : chr  "chevrolet chevelle malibu" "buick skylark 320" "plymouth satellite" "amc rebel sst" ...

> summary(data)
      mpg          cylinders      displacement     horsepower        weight    
 Min.   : 9.00   Min.   :3.000   Min.   : 68.0   Min.   : 46.0   Min.   :1613  
 1st Qu.:17.50   1st Qu.:4.000   1st Qu.:104.2   1st Qu.: 75.0   1st Qu.:2224  
 Median :23.00   Median :4.000   Median :148.5   Median : 93.5   Median :2804  
 Mean   :23.51   Mean   :5.455   Mean   :193.4   Mean   :104.5   Mean   :2970  
 3rd Qu.:29.00   3rd Qu.:8.000   3rd Qu.:262.0   3rd Qu.:126.0   3rd Qu.:3608  
 Max.   :46.60   Max.   :8.000   Max.   :455.0   Max.   :230.0   Max.   :5140  
                                                 NA's   :6                     
  acceleration     model_year        origin        car_name        
 Min.   : 8.00   Min.   :70.00   Min.   :1.000   Length:398        
 1st Qu.:13.82   1st Qu.:73.00   1st Qu.:1.000   Class :character  
 Median :15.50   Median :76.00   Median :1.000   Mode  :character  
 Mean   :15.57   Mean   :76.01   Mean   :1.573                     
 3rd Qu.:17.18   3rd Qu.:79.00   3rd Qu.:2.000                     
 Max.   :24.80   Max.   :82.00   Max.   :3.000
```

1. Load the autompg.csv file and convert cylinders variable to a factor. (code, output of str())
    
    ```r
    > data$cylinders <- as.factor(data$cylinders)
    [1] 8 8 8 8 8 8 8 8 8 8 8 8 8 8 4 6 6 6 4 4 4 4 4 4 6 8 8 8 8 4 4 4 4 6 6 6 6 6
     [39] 8 8 8 8 8 8 8 6 4 6 6 4 4 4 4 4 4 4 4 4 4 4 4 4 8 8 8 8 8 8 8 8 8 3 8 8 8 8
     [77] 4 4 4 4 4 4 4 4 4 8 8 8 8 8 8 8 8 8 8 8 8 6 6 6 6 6 4 8 8 8 8 6 4 4 4 3 4 6
    [115] 4 8 8 4 4 4 4 8 4 6 8 6 6 6 6 4 4 4 4 6 6 6 8 8 8 8 8 4 4 4 4 4 4 4 4 4 4 4
    [153] 6 6 6 6 8 8 8 8 6 6 6 6 6 8 8 4 4 6 4 4 4 4 6 4 6 4 4 4 4 4 4 4 4 4 4 8 8 8
    [191] 8 6 6 6 6 4 4 4 4 6 6 6 6 4 4 4 4 4 8 4 6 6 8 8 8 8 4 4 4 4 4 8 8 8 8 6 6 6
    [229] 6 8 8 8 8 4 4 4 4 4 4 4 4 6 4 3 4 4 4 4 4 8 8 8 6 6 6 4 6 6 6 6 6 6 8 6 8 8
    [267] 4 4 4 4 4 4 4 4 5 6 4 6 4 4 6 6 4 6 6 8 8 8 8 8 8 8 8 4 4 4 4 5 8 4 8 4 4 4
    [305] 4 4 6 6 4 4 4 4 4 4 4 4 6 4 4 4 4 4 4 4 4 4 4 5 4 4 4 4 4 6 3 4 4 4 4 4 4 6
    [343] 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 4 6 6 6 6 8 6 6 4 4 4 4 4 4 4 4 4 4 4 4 4
    [381] 4 4 4 4 4 4 6 6 4 6 4 4 4 4 4 4 4 4
    Levels: 3 4 5 6 8
    > str(data$cylinders)
     Factor w/ 5 levels "3","4","5","6",..: 5 5 5 5 5 5 5 5 5 5 ...
    ```
    
2. Which is the dependent variable? Which are the independent variable(s)?
    
    ```r
    MPG is the dependent variable. 
    
    Cylindars, Displacement, horsepower, weight, acceleration, model_year, origin, car_name are all independant
    
    Horsepower COULD be a dependent variable
    ```
    
3. Plot mpg vs. displacement (code, plot)
    
    ```r
    > ggplot(data, aes(x = displacement, y = mpg)) + geom_point()
    
    ```
    
    ![Untitled](Ursenbach%20HW%203%20e3f1827332bf4d56891825b2bcbdfc98/Untitled.png)
    
4. Create a linear model called mod_displ of mpg vs. displacement (only one independent variable). What is the R2 value? (code, output of summary(mod_displ), R2 value)
    
    ```r
    > mod_displ <- lm(mpg~displacement, data = data)
    > summary(mod_displ)
    
    Call:
    lm(formula = mpg ~ displacement, data = data)
    
    Residuals:
         Min       1Q   Median       3Q      Max 
    -12.9550  -3.0569  -0.4928   2.3277  18.6192 
    
    Coefficients:
                  Estimate Std. Error t value Pr(>|t|)    
    (Intercept)  35.174750   0.491824   71.52   <2e-16 ***
    displacement -0.060282   0.002239  -26.93   <2e-16 ***
    ---
    Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
    
    Residual standard error: 4.651 on 396 degrees of freedom
    Multiple R-squared:  0.6467,	Adjusted R-squared:  0.6459 
    F-statistic:   725 on 1 and 396 DF,  p-value: < 2.2e-16
    
    # the r^2 value is .6467
    ```
    
5. Plot a distribution of the residuals from mod_displ (code, plot)
    
    ```r
    > mod_displ_resid <- resid(mod_displ)
    ```
    
    ![Untitled](Ursenbach%20HW%203%20e3f1827332bf4d56891825b2bcbdfc98/Untitled%201.png)
    
6. Predict the mpg of three cars with engine displacements 50 cu in, 100 cu in, and 500 cu in each. Which prediction has the tightest bounds? (code, output)
    
    ```r
    > mod_displ
    
    Call:
    lm(formula = mpg ~ displacement, data = data)
    
    Coefficients:
     (Intercept)  displacement  
        35.17475      -0.06028
    
    # 50: 
    > -0.06028*50+35.17475
    [1] 32.16075
    # 100:
    > -0.06028*100+35.17475
    [1] 29.14675
    # 500: 
    > -0.06028*500+35.17475
    [1] 5.03475
    
    > ggplot(data, aes(x = displacement, y = mpg)) + geom_point() + geom_smooth(method = "lm")
    `geom_smooth()` using formula 'y ~ x'
    ```
    
    ![Untitled](Ursenbach%20HW%203%20e3f1827332bf4d56891825b2bcbdfc98/Untitled%202.png)
    
7. Create a linear model called mod_displ_cyl of mpg vs. displacement and cylinders.

```r
> mod_displ_cyl <- lm(mpg~displacement+cylinders, data)
```

1. Give R code, output of summary(mod_displ_cyl)
    
    ```r
    > summary(mod_displ_cyl)
    
    Call:
    lm(formula = mpg ~ displacement + cylinders, data = data)
    
    Residuals:
         Min       1Q   Median       3Q      Max 
    -10.6865  -2.6859  -0.3578   2.1592  20.3641 
    
    Coefficients:
                  Estimate Std. Error t value Pr(>|t|)    
    (Intercept)  24.434454   2.262674  10.799  < 2e-16 ***
    displacement -0.053579   0.006925  -7.737 8.73e-14 ***
    cylinders4   10.735065   2.242713   4.787 2.41e-06 ***
    cylinders5   10.701120   3.407320   3.141  0.00181 ** 
    cylinders6    7.239065   2.473200   2.927  0.00362 ** 
    cylinders8    9.013815   2.935682   3.070  0.00229 ** 
    ---
    Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
    
    Residual standard error: 4.413 on 392 degrees of freedom
    Multiple R-squared:  0.6853,	Adjusted R-squared:  0.6813 
    F-statistic: 170.7 on 5 and 392 DF,  p-value: < 2.2e-16
    ```
    
2. How many dummy (i.e., 0-1) variables were created in the model? What are they called?
    
    ```r
    4 variables: 
    cylinders4   10.735065   2.242713   4.787 2.41e-06 ***
    cylinders5   10.701120   3.407320   3.141  0.00181 ** 
    cylinders6    7.239065   2.473200   2.927  0.00362 ** 
    cylinders8    9.013815   2.935682   3.070  0.00229 ** 
    ```
    
3. Is this a better fit than mod_displ? Why or why not?
    
    ```r
    # Yes it is better. It takes into account independent variables taht are affecting the mpg. If they weren't affecting it it wouldn't be better. 
    
    # also the r^2 is 68, when the previous one was 64. 
    ```
    
4. Give the model equations relating mpg with displacement and cylinders.
    
    ```r
    mpg = -0.05358(displacement) + 10.73507(cyl4)+10.70112(cyl5)+10.70112(cyl6)+9.01381(cyl8)+24.43445
    ```
    
5. Plot mpg vs. displacement and overlay the best fit model. (code, plot) [Hint: A shortcut: plot the predictions; use add_predictions() and geom_line() and use the color aesthetic for cylinders]
    
    ```r
    > ggplotRegression <- function (fit) {
    +     
    +     require(ggplot2)
    +     
    +     ggplot(fit$model, aes_string(x = names(fit$model)[2], y = names(fit$model)[1])) + 
    +         geom_point() +
    +         stat_smooth(method = "lm", col = "red") +
    +         labs(title = paste("Adj R2 = ",signif(summary(fit)$adj.r.squared, 5),
    +                            "Intercept =",signif(fit$coef[[1]],5 ),
    +                            " Slope =",signif(fit$coef[[2]], 5),
    +                            " P =",signif(summary(fit)$coef[2,4], 5)))
    + }
    > ggplotRegression(lm(mpg~displacement+cylinders, data))
    ```
    
    ![Untitled](Ursenbach%20HW%203%20e3f1827332bf4d56891825b2bcbdfc98/Untitled%203.png)
    
6. Create a new transformed variable logdispl=log(displacement). Create a linear model called mod_logdispl of mpg vs. logdispl.
    
    ```r
    > data$logdispl <- log(data$displacement)
    > mod_logdispl <- lm(mpg~logdispl, data)
    ```
    
    1. Give R code, output of summary(mod_logdispl)
        
        ```r
        > summary(mod_logdispl)
        
        Call:
        lm(formula = mpg ~ logdispl, data = data)
        
        Residuals:
             Min       1Q   Median       3Q      Max 
        -16.1743  -2.5461  -0.4326   2.1949  19.9107 
        
        Coefficients:
                    Estimate Std. Error t value Pr(>|t|)    
        (Intercept)  85.9507     2.1329   40.30   <2e-16 ***
        logdispl    -12.1870     0.4141  -29.43   <2e-16 ***
        ---
        Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
        
        Residual standard error: 4.384 on 396 degrees of freedom
        Multiple R-squared:  0.6862,	Adjusted R-squared:  0.6854 
        F-statistic: 866.1 on 1 and 396 DF,  p-value: < 2.2e-16
        ```
        
    2. Is this a better fit than mod_displ_cyl? Why or why not?
        
        ```r
        # the r^2 is pretty close, although the F-statistis is quite a bit higher though. Is hsould be a better fit?
        ```
        
    3. Plot mpg vs. logdispl and overlay the best fit model as a straight line. (code, plot)
        
        ```r
        > ggplotRegression(mod_logdispl)
        
        ```
        
        ![Untitled](Ursenbach%20HW%203%20e3f1827332bf4d56891825b2bcbdfc98/Untitled%204.png)
        
    4. Give the model equation relating mpg with displacement
        
        ```r
        > mod_logdispl
        
        Call:
        lm(formula = mpg ~ logdispl, data = data)
        
        Coefficients:
        (Intercept)     logdispl  
              85.95       -12.19
        # mpg = -12.19(logdispl) + 85.95
        ```
        
    5. Plot mpg vs. displacement and overlay the best fit model as a curve. (code, plot) [ Hint: plot the predictions; use add_predictions() and geom_line() ]
        
        ```r
        > ggplot(df, aes(x = displacement, y = mpg)) + geom_point() + geom_line(mapping = aes(x=displacement, y = pred, color = "red"))
        
        ```
        
        ![Untitled](Ursenbach%20HW%203%20e3f1827332bf4d56891825b2bcbdfc98/Untitled%205.png)