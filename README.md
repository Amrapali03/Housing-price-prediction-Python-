# Housing-price-prediction
Predicted King County housing sale prices using Python, utilizing exploratory and quantitative analysis of summary statistics, Root Mean Squared Error values, dummy and confounding variable representation, interaction effects, and a robust Multiple Linear Regression model for accurate property value estimates.

## Initial Regression
<img width="721" alt="image" src="https://github.com/Amrapali03/Housing-price-prediction/assets/114306627/69ec8d0b-a015-4210-8c35-d9db5f076207">

## Stepwise Selection
After selection of variables the regression results are better with a better R-square.
<img width="856" alt="image" src="https://github.com/Amrapali03/Housing-price-prediction/assets/114306627/b23eeda5-d7de-4b98-9d96-0b659a6dece0">


## Factor and Dummy variables

### Dummy variable
There are three possible values: Multiplex, Single Family, and Townhouse for the housing dataset variable 'property type'.
To use this factor variable, we need to convert it to a set of binary variables. 
The factor variable PropertyType, which has three distinct levels, is represented as a matrix with three columns. 
This is called one hot encoding.

![image](https://github.com/Amrapali03/Housing-price-prediction/assets/114306627/11de5aca-d22d-4072-b34f-e466a433ca4f)

![image](https://github.com/Amrapali03/Housing-price-prediction/assets/114306627/2232b009-53ac-40e8-ac4c-a8dc14f08671)

### Factor variables with many levels
ZipCode is an important variable, since it is a proxy for the effect of location on the value of a house. Including all levels requires 79 coefficients corresponding to 79 degrees of freedom.
The median residual is computed for each zip, and the ntile function is used to split the zip codes, sorted by the median, into five groups. 
![image](https://github.com/Amrapali03/Housing-price-prediction/assets/114306627/e7513d3d-2cba-493e-8a6b-a5f7fa26060f)


## Interpretation of old regression model
![image](https://github.com/Amrapali03/Housing-price-prediction/assets/114306627/85d4b43f-8780-4c1a-b12e-5c72ea621aa7)

Bedroom is negative. This implies that adding a bedroom to a house will reduce its value. How can this be? This is because the predictor variables are correlated: larger houses tend to have more bedrooms, and it is the size that drives house value, not the number of bedrooms. 
Consider two homes of the exact same size: it is reasonable to expect that a home with more but smaller bedrooms would be considered less desirable.

The variables for bedrooms, house size, and number of bathrooms are all correlated. 
Hence we keep only Bedrooms.
Now the coefficient for bedrooms is positive.
![image](https://github.com/Amrapali03/Housing-price-prediction/assets/114306627/9c181bb8-ba5b-4df4-bb04-17ee83cbe866)

## Confounding variables 
With confounding variables, the problem is one of omission: an important variable is not included in the regression equation.
The original regression model does not contain a variable to represent location—a very important predictor of house price.
Hence, we consider zipcode in new regression model.
![image](https://github.com/Amrapali03/Housing-price-prediction/assets/114306627/ba136763-41f8-4c4a-a523-5626b7b51464)


## Interactions and Main Effects
 An interaction term between two variables is needed if the relationship between the variables and the response is interdependent.
 A big house built in a low-rent district is not going to retain the same value as a big house built in an expensive area. 
 We introduce SqFtTotLiving*ZipGroup into the model.
 ![image](https://github.com/Amrapali03/Housing-price-prediction/assets/114306627/75e813a0-e8c6-422f-a57e-c544d93729d7)


## Regression diagnostics
Things to consider as below:
**Standardized residuals**: Residuals divided by the standard error of the residuals.
**Outliers**: Records (or outcome values) that are distant from the rest of the data (or the predicted outcome).
![image](https://github.com/Amrapali03/Housing-price-prediction/assets/114306627/40edeb2d-ecb9-46a6-9f16-5c7a88b6e3ec)

**Influential value**: A value whose absence would significantly change the regression equation is termed an influential observation. 
**Heteroskedasticity** is the lack of constant residual variance across the range of the predicted values. 
In other words, errors are greater for some portions of the range than for others.

![image](https://github.com/Amrapali03/Housing-price-prediction/assets/114306627/e8cf2909-5b6e-4cf0-8b9c-68980991251a)

Evidently, the variance of the residuals tends to increase for higher-valued homes but is also large for lower-valued homes. 
This plot indicates that lm_98105 has heteroskedastic errors.
For example, the heteroskedasticity in lm_98105 may indicate that the regression has left something unaccounted for in high- and low-range homes.


## Non-linear
### Partial residual plot
Partial residual plots are a way to visualize how well the estimated fit explains the relationship between a predictor and the outcome. 
The basic idea of a partial residual plot is to isolate the relationship between a predictor variable and the response, taking into account all of the other predictor variables.
The relationship between the response and a predictor variable isn’t necessarily linear.
The partial residual is an estimate of the contribution that SqFtTotLiving adds to the sales price. The relationship between SqFtTotLiving and the sales price is evidently nonlinear (dashed line). The regres‐ sion line (solid line) underestimates the sales price for homes less than 1,000 square feet and overestimates the price for homes between 2,000 and 3,000 square feet. There are too few data points above 4,000 square feet to draw conclusions for those homes.

### Polynomial
Nonlinear regression means we are referring to models that can’t be fit using least squares. 
Essentially all models where the response cannot be expressed as a linear combination of the predictors or some transform of the predictors.
Polynomial regression involves including polynomial terms in a regression equation.
There are now two coefficients associated with SqFtTotLiving: one for the linear term and one for the quadratic term.
![image](https://github.com/Amrapali03/Housing-price-prediction/assets/114306627/aca8c4f8-7450-40f1-9e35-d876633bf889)

### Spline
Polynomial regression captures only a certain amount of curvature in a nonlinear relationship. Adding in higher-order terms, such as a cubic quartic polynomial, often
leads to undesirable “wiggliness” in the regression equation. An alternative, and often superior, approach to modeling nonlinear relationships is to use splines. Splines pro‐ vide a way to smoothly interpolate between fixed points. Splines were originally used by draftsmen to draw a smooth curve, particularly in ship and aircraft building.
![image](https://github.com/Amrapali03/Housing-price-prediction/assets/114306627/047e8893-c99f-42a0-ac89-defa4f899141)

