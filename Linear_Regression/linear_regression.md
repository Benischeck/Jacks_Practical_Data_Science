<div align="center" id="user-content-toc">
  <ul align="center" style="list-style: none;">
    <summary>
      <h1>Linear Regression</h1>
    </summary>
  </ul>
</div>

<br>



# Overview

<br>

**Supervised or Unsupervised:** Supervised.

<br> 

**Purpose:** To describe/generalize the linear relationship between a dependent variable Y, and one or more independent variable(s) X<sub>i</sub> . 

<br>

# Assumptions:

- **Linearity:** The relationship between the dependent variable and the independent variable(s) is linear. That is, they do not exhibit exponential, logarithmic, or other non-linear relationships. 

- **Normal Distribution of the error terms (residuals):** The residuals should not show a relationship with the dependent variable Y. Can check this by plotting Y against the residuals.
    - Related to the linearity assumption – if the error terms aren’t normally distributed, then it means that, somewhere, the regression ‘line’ is deviating more than normal from the actual data. 
    - To test, plot the residuals by the predicted values. There should be no pattern to the data.
    - Can also test using a QQ plot (distribution of residuals vs. draws from the normal distribution). 

- **Independence of the Observations:** Predominantly an assumption regarding time-series analysis, in that sequential observations should not be correlated, else it can cause auto-correlation.

- **Equal Variances of Errors (residuals):** the variance of the residuals is the same for all values of X (showing homoskedasticity). In particular, we are concerned with the variability in the response not increasing as the predictor value(s) increase (a sign of heteroskedasticity).  
    - To test, plot the residuals by the predicted values.

**Additive:** The impact of one independent variable on the dependent variable is not affected by changes in other independent variables. 
 
<br>

<br> 

# How: 
By using the Least Squares method, we fit a line to the data that minimizes the squared errors (how far each observation is away from the estimated point on the regression line). We want to know if the slope of the line (specifically, the beta coefficient) is statistically different than 0 (implying no relationship). By calculating the Mean Square Error (SSE/[n-2]) and the variance of Xi, we can calculate the test statistic ‘t’ as the beta coefficient divided by (MSE/sqrt(sum of variance of Xi). This is then compared against the p-value. We can also confirm this by creating a confidence interval of the beta coefficient +/- t*s, where t is the value in the t distribution associated with n-2 degrees of freedom, and s is the square root of the sum of variance of Xi. If 0 is not in the confidence interval, we can reject.

<br>

<br>

# Interpretation: 
- By holding all else equal, a 1 unit increase in a particular independent variable leads to a 1*beta coefficient increase/decrease in the response variable. 
- As a best practice, interpretation should fall to only the range of observed values. New data beyond the sample set may not have the same relationship.
- Unless the regression line passes through the origin of the graph (x=0, y=0 on a bivariate graph) without having been coerced to do so, it is typically frowned upon to make interpretations of the dependent variable when all independent variables are equal to 0, unless there is some intuition to do so. (eg, it is probably ok in a simple linear regression if we are trying to predict the price of a car solely based on the number of years since it was manufactured, but it wouldn’t be ok if we were trying to predict something like the estimated cost of a hospital visit if our only predictor is the number of surgeries [In this case, while we might expect 0 surgeries to estimate a cost of $0, our model is unlikely to pass through the origin for a number of reasons.] This disconnect is why we would not interpret the y-intercept). 

<br>

<br>

# Evaluation: 
- Coefficient of Determination (R-squared). This is simply SSR/SST (recall SST = SSR + SSE, where SSE is the squared errors [how we derived our best fit line], SST is simply the sum of squared errors if we used the mean as our regression line [ie if every predicted value was the mean], and SSR is the difference between the two). 
- Adjusted Coefficient of Determination (Adjusted R-Squared). Because additional variables and data points always increase the value of R-squared, this adjusts by penalizing for additional variables and datapoints. 
- Residual vs. Fitted Plot 
    - Residuals plotted on y-axis, fitted values plotted on x-axis
    - There should be no pattern to the plot, which suggests the relationship is linear and reasonable.
    - The fitted line to this plot should roughly be horizontal and around 0, suggesting that the variances of the error terms are equal.
    - Residuals shouldn’t stand out. If they do, it would suggest outlier datapoints.

- Residuals vs. Leverage
    - Is used to determine if any of the datapoints have an outsized impact on the model, which would indicate them as outliers. These are significant points that, if removed, would considerably change the model.
    - Points of influence (those that have ‘leverage’) are found via Cook’s Distance. 

- Q-Q Plot (Quantile-Quantile Plot)
    - Plots your (sorted) dependent variable against (sorted) values drawn at that “quantile” from a distribution (typically the Normal, but it doesn’t have to be). We are generally looking for a straight line, which would suggest that our dependent variable came from our chosen distribution. There are a few interpretations when the graph is not a straight line. For example, extreme tails in the plot suggest that our data have more extreme values than would be expected if our dependent variable came from a normal distribution. 

- Correlation Coefficient matrix to check for presence of multicollinearity (rule of thumb abs(.7) or higher is an issue. If multicollinearity exists, one or all might not be significant from t-test. In extreme cases, their true coefficient signs might be flipped). 
- Mean Square Error (MSE)
    - Most common measure. It is the average between the predicted and actual value. 
    - It is a good indication when the MSE using the test set is lower than the MSE using the training set, which suggests the model built on training data has not been overfit.

- Mean Absolute Error (MAE)
    - Simply the average of the absolute value of the difference between the predicted and actual value.
    - Not great when there are outliers, as there is no penalty for them.
    - Similar on MSE on how to read it.

- Mean Absolute Percentage Error (MAPE)
    - Almost the same as MAE, but divides the difference by the actual value to turn the overall calculation into a percentage as a measure of accuracy.
    - Also does not work well with outliers.

- Mallow’s Cp
    - Formula to determine the usefulness of a full model vs. subsets of the full model. If the Cp value of a subset is close to the value of the full p, then the subset is the better choice.

<br>

<br>

# Pros: 
- Linear regression models are easy to explain. By reading the sign and coefficient associated with each variable in the model (assuming statistical significance), we can understand the importance and impact that each independent variable has on the dependent variable.
- Linear regression models have a closed-form solution and simple means of optimization (OLS).

<br>

<br>

# Cons:
- Interpretation can be tricky if the practitioner is not familiar with both the methods of evaluation, as well as limited scope of interpretation (eg, only interpreting new observations that fall within the line segment of data used to train the model). 


<br>

<br>

# Helpful Resources

https://data.library.virginia.edu/diagnostic-plots/

https://www.jmp.com/en_us/statistics-knowledge-portal/what-is-regression/simple-linear-regression-assumptions.html
