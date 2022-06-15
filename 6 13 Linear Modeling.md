# 6/13 Linear Modeling

[Linear regression.pptx](6%2013%20Linear%20Modeling%20a610cf705bff420c8061be737f4644c9/Linear_regression.pptx)

### Textbook Sections:

- [B1] R for Data Science, Garrett Grolemund and Hadley Wickhamhttps://r4ds.had.co.nz/
    - ch 22-24

![Untitled](6%2013%20Linear%20Modeling%20a610cf705bff420c8061be737f4644c9/Untitled.png)

## What is a Math Model?

- 

Model
Representation of a phenomenon
Mathematical model
Numerically describe relationship between variables

## Regression Model

- Relationship between one dependent variable and explanatory variable(s)
- Dependent variable is continuous
- One equation describes the relationship

## Steps to modeling

- Define a family of models
    - Specify the generic pattern of relationship between variables
    - E.g., Linear, Quadratic, …
- Fit the model to the data
    - Identify the “best” model from the family of models
    - Give values to the model parameters

## Types of Regression Models

- Simple
    - linear
    - non-linear
- Multiple
    - linear
    - non-linear

![Untitled](6%2013%20Linear%20Modeling%20a610cf705bff420c8061be737f4644c9/Untitled%201.png)

# Linear Regression Model

### Classwork .5

- Consider the problem of estimating Height given Weight and Age
    - What are some linear models for this?
    - What are some nonlinear models for this?

## Linear Equations:

can only use summation of variable multiplied by constant

cannot multiply variables with eachother

![Untitled](6%2013%20Linear%20Modeling%20a610cf705bff420c8061be737f4644c9/Untitled%202.png)

## Linear Regression Model

- Relationship between variables is a Linear Function

![Untitled](6%2013%20Linear%20Modeling%20a610cf705bff420c8061be737f4644c9/Untitled%203.png)

[Classwork 1](6%2013%20Linear%20Modeling%20a610cf705bff420c8061be737f4644c9/Classwork%201%20d69ce09df3204fa4ab5528e8a6610a70.md)

## Least Squares (LS)

Best Fit
Minimize the difference between Actual Y values & Predicted Y values.
Square the differences
Differences are called “errors” or “residuals”

![Untitled](6%2013%20Linear%20Modeling%20a610cf705bff420c8061be737f4644c9/Untitled%204.png)

### Least Squares Graphically represented:

![Untitled](6%2013%20Linear%20Modeling%20a610cf705bff420c8061be737f4644c9/Untitled%205.png)

![Untitled](6%2013%20Linear%20Modeling%20a610cf705bff420c8061be737f4644c9/Untitled%206.png)

### prediction equation

![Untitled](6%2013%20Linear%20Modeling%20a610cf705bff420c8061be737f4644c9/Untitled%207.png)

### Sample Slope

![Untitled](6%2013%20Linear%20Modeling%20a610cf705bff420c8061be737f4644c9/Untitled%208.png)

### Sample Y - intercept

![Untitled](6%2013%20Linear%20Modeling%20a610cf705bff420c8061be737f4644c9/Untitled%209.png)

## When can we use LM?

One dependent variable
Dependent variable is continuous

## Linear Regression in R

```r
> lm(data=iris, Sepal.Width~Sepal.Length)

Call:
lm(formula = Sepal.Width ~ Sepal.Length, data = iris)

Coefficients:
 (Intercept)  Sepal.Length  
     3.41895      -0.06188

# so this is the best fit line:
> ggplot(data=iris) + geom_point(mapping = aes(x=Sepal.Length, y=Sepal.Width)) + geom_abline(slope = -0.06188, intercept = 3.41895)
```

![Untitled](6%2013%20Linear%20Modeling%20a610cf705bff420c8061be737f4644c9/Untitled%2010.png)

### Classwork 2 (unfinished)

[Classwork 2](6%2013%20Linear%20Modeling%20a610cf705bff420c8061be737f4644c9/Classwork%202%2072b051b533114465822474c3425e521d.md)

## When should we use LM?

- Is the “best” fit model a good model?!
- Evaluating the model
- Two conflicting objectives
    - Goodness-of-Fit
        - We want model to match the data
    - Complexity
        - We want model to be “simple”
- “Principle of parsimony”
    - Find a model that is as simple as possible without sacrificing too much goodness-of-fit

### classwork 3

[classwork 3](6%2013%20Linear%20Modeling%20a610cf705bff420c8061be737f4644c9/classwork%203%201d4462a9aa654cf29012589603aac0b9.md)

## Coefficient of Determination

- The proportion of total variation (SST) that is explained by the regression (SSR)  is the Coefficient of Determination (𝑅^2)
- 𝑅^2 ranges between 0 and 1
    - higher its value, the more accurate is the regression model
- 𝑅^2=𝑆𝑆𝑅/𝑆𝑆𝑇=1−𝑆𝑆𝐸/𝑆𝑆𝑇
    - 
    
    ![Untitled](6%2013%20Linear%20Modeling%20a610cf705bff420c8061be737f4644c9/Untitled%2011.png)
    

## Sum of Squares of Error (SSE)

- A least squares regression selects the line with the lowest total sum of squared prediction errors.
- This value is called the Sum of Squares of Error (SSE)
- This is the “unexplained” variation

![Untitled](6%2013%20Linear%20Modeling%20a610cf705bff420c8061be737f4644c9/Untitled%2012.png)

## Sum of Squares Regression (SSR)

- The Sum of Squares Regression (SSR) is the sum of the squared differences between the
- prediction for each observation and the population mean.
- This is the “explained” variation

![Untitled](6%2013%20Linear%20Modeling%20a610cf705bff420c8061be737f4644c9/Untitled%2013.png)

![Untitled](6%2013%20Linear%20Modeling%20a610cf705bff420c8061be737f4644c9/Untitled%2014.png)

Pr(>|t|) - This is the probability that you would get this model from random chance. The lower, the less likely it’s random 

### Good linear model:

![Untitled](6%2013%20Linear%20Modeling%20a610cf705bff420c8061be737f4644c9/Untitled%2015.png)

### Bad linear model:

## Regression Coefficient Significance Tests

Linear regression coefficients, when estimated using least-squares, follow a t-distribution
lm() includes the standardized t value and a p-value for each coefficient
The smaller the p-value, the stronger the evidence against the null hypothesis: the coefficient is 0
i.e., there is strong evidence for the claim that the predictor has an effect

## Regression Diagnostics

The three conditions required for the validity of the regression analysis are:
the error variable is normally distributed
the error variance is independent of x
The errors are independent of each other
How can we diagnose violations of these conditions?

## Residuals

![Untitled](6%2013%20Linear%20Modeling%20a610cf705bff420c8061be737f4644c9/Untitled%2016.png)

```r
# to add residuals to a model
> library(modelr)
Warning message:
package ‘modelr’ was built under R version 4.1.3 
> m <- iris %>% add_residuals(m) %>% view()
```

![Untitled](6%2013%20Linear%20Modeling%20a610cf705bff420c8061be737f4644c9/Untitled%2017.png)

```r
ggplot(data=m) + geom_histogram(mapping = aes(x=resid))
```

![Untitled](6%2013%20Linear%20Modeling%20a610cf705bff420c8061be737f4644c9/Untitled%2018.png)

## Residual Analysis

Plot a scatterplot
Residuals vs x
Points should appear to be randomly scattered around zero

```r
 library(modelr)
irisCopy <- iris %>% add_residuals(mod)
gplot(data=irisCopy) + geom_point(mapping = aes(x=Petal.Width, y=resid))
```

instructor example:

```r
> ggplot(data=m) + geom_point(mapping = aes(y=resid, x=Petal.Length))
```

![Untitled](6%2013%20Linear%20Modeling%20a610cf705bff420c8061be737f4644c9/Untitled%2019.png)

# missing slides here

## Outliers

- Outlier: an observation that is unusually small or large
- Several possibilities need to be investigated when an outlier is observed:
    - There was an error in recording the value.
    - The point does not belong in the sample.
    - The observation is valid.
- Suspect an observation is an outlier if its
    - **|standardized residual| > 2**
    

```r
# this gives you a list of the residiuals
rstandard(model)
```

```r
iris %>% mutate(rstd = rstandard(model)) %>% view()
```

![Untitled](6%2013%20Linear%20Modeling%20a610cf705bff420c8061be737f4644c9/Untitled%2020.png)

you’ll see the new column rtd on the right

### remember dependant ~ independant:

- dependent should always be on the y axis

### Finding outliers

- so you’re looking for rows that are greater than 2
- use filter()

```r
> m <- lm(data=iris, Petal.Width~Petal.Length)
> m
Call:
lm(formula = Petal.Width ~ Petal.Length, data = iris)

Coefficients:
 (Intercept)  Petal.Length  
     -0.3631        0.4158
> outliers <- iris %>% mutate(rstd = rstandard(m)) %>% filter(rstd > 2 | rstd < -2) %>% view()
```

![Untitled](6%2013%20Linear%20Modeling%20a610cf705bff420c8061be737f4644c9/Untitled%2021.png)

```r
> ggplot(data=iris) + geom_point(mapping = aes(x=Petal.Length, y=Petal.Width)) + geom_point(data=outliers, mapping=aes(x=Petal.Length, y=Petal.Width), color="red") 
```

![Untitled](6%2013%20Linear%20Modeling%20a610cf705bff420c8061be737f4644c9/Untitled%2022.png)

```r
> summary(m)

Call:
lm(formula = Petal.Width ~ Petal.Length, data = iris)

Residuals:
     Min       1Q   Median       3Q      Max 
-0.56515 -0.12358 -0.01898  0.13288  0.64272 

Coefficients:
              Estimate Std. Error t value Pr(>|t|)    
(Intercept)  -0.363076   0.039762  -9.131  4.7e-16 ***
Petal.Length  0.415755   0.009582  43.387  < 2e-16 ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 0.2065 on 148 degrees of freedom
Multiple R-squared:  0.9271,	Adjusted R-squared:  0.9266 
F-statistic:  1882 on 1 and 148 DF,  p-value: < 2.2e-16
```

Remember the R-Squared value is the most important value. 

<aside>
💡 you want the R-Squared value to be **AS CLOSE TO 1** as possible

</aside>

# Missing slides here

# Making predictions

- The fitted model can be used to make predictions for new x values
    - For accuracy, x should be within the range seen in the data used for modeling (interpolation)
- Data.frame used for prediction must have the same variable names as in the model

```r
m <- lm(data=iris, Petal.Width~Petal.Length)
> predx <-data.frame(Petal.Length=c(0.5, 2.5, 10.0))
> predict(m, predx)
         1          2          3 
-0.1551978  0.6763130  3.7944786

# Petal.Width = -0.3630755 + 0.4157554*Petal.Length
> -0.3630755 + 0.4157554*2.5
[1] 0.676313
```

## Standard Error

- Calculating Standard Error of the regression is used for calculating
    - prediction intervals
    - confidence intervals
- Standard Error = square root of the average prediction error.

## Prediction interval

- For a given value of x, the interval estimate of the dependent variable is called the prediction interval
- predict(mod, newdata=predx, interval="prediction", level=0.95)

![Untitled](6%2013%20Linear%20Modeling%20a610cf705bff420c8061be737f4644c9/Untitled%2023.png)

```r
> m <- lm(data=iris, Petal.Width~Petal.Length)
> predx <-data.frame(Petal.Length=c(0.5, 2.5, 10.0))
> predict(m, predx, interval="prediction", level=0.95)
         fit        lwr       upr
1 -0.1551978 -0.5692164 0.2588208
2  0.6763130  0.2662243 1.0864017
3  3.7944786  3.3683610 4.2205963

> predict(m, predx, interval="confidence")
         fit        lwr         upr
1 -0.1551978 -0.2253126 -0.08508304
2  0.6763130  0.6353565  0.71726953
3  3.7944786  3.6716741  3.91728318
```

You’ll see that the confidence prediction shows greater confidence because the bounds are narrow

In confidence, the second row is narrower than the third row

```r
> ggplot(data=iris) + geom_point(mapping = aes(x=Petal.Length, y=Petal.Width)) + geom_point(data=outliers, mapping=aes(x=Petal.Length, y=Petal.Width), color="red") + geom_smooth(mapping=aes(x=Petal.Length, y=Petal.Width), method="lm", color="red")
`geom_smooth()` using formula 'y ~ x'
```

![Untitled](6%2013%20Linear%20Modeling%20a610cf705bff420c8061be737f4644c9/Untitled%2024.png)

you can see here where the confidence gets narrower and thicker

even though the model is capable of making predictions, the predictions become less accurate as you leave the area that had no datapoints

# Why is LR important?

- Simple
- Efficient
- Assumptions are reasonable
- Model is surprisingly powerful
    - Multiple predictor variables
    - Can use transformed predictors

# REVIEW: Procedure for Regression Diagnostics

- Gather data for the variables in the model
- Draw a scatterplot to determine whether a linear model appears to be appropriate
- Determine the regression equation (lm)
- Check the required conditions for the errors (residual analysis)
- Check the existence of outliers
- Assess the model fit (R2)
- If the model fits the data, use the model to predict new values (predict)

## Review

### List the most important things today:

- Linear Regression
- Prediction
- Least Squares
- Confidence
- 

### What questions remain in your mind?

- How do I do some of these for sub-groups
    - ex: how would I use this to predict what species a data point is connected with
    

# Functions to create:

# BRAIN BREAK: Slow Breathing:

[https://www.youtube.com/watch?v=b2WaWw9VNww](https://www.youtube.com/watch?v=b2WaWw9VNww)
