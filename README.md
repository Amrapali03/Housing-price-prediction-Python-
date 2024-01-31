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


## Confounding variables 
With confounding variables, the problem is one of omission: an important variable is not included in the regression equation.
The original regression model does not contain a variable to represent location—a very important predictor of house price.
Hence, we consider zipcode.


## Interpretation
![image](https://github.com/Amrapali03/Housing-price-prediction/assets/114306627/85d4b43f-8780-4c1a-b12e-5c72ea621aa7)

Bedroom is negative. This implies that adding a bedroom to a house will reduce its value. How can this be? This is because the predictor variables are correlated: larger houses tend to have more bedrooms, and it is the size that drives house value, not the number of bedrooms. 
Consider two homes of the exact same size: it is reasonable to expect that a home with more but smaller bedrooms would be considered less desirable.

The vari‐ ables for bedrooms, house size, and number of bathrooms are all correlated.
Now the coefficient for bedrooms is positive.
![image](https://github.com/Amrapali03/Housing-price-prediction/assets/114306627/9c181bb8-ba5b-4df4-bb04-17ee83cbe866)


