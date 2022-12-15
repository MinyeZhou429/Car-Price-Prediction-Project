# BST260 Final Project: Car Price Prediction Models

## Introduction
### Data Source

*Automobile Data Set* from UCI Machine Learning Repository (DIM: 26 x 205)

### Outcome and Variable used in analyses

The dependent variable is car price, the car price distribution is as followed:

| Mean | 25 percentile | Median | 75 percentile | Maximum |
| ------ | ----------- | ----------- | ----------- | ----------- |
| $5118 | $7788 | $10295 | $16503 | $45400 |

The covariates used in the study are:

| Variable name | Description |
| ----------- | ----------- |
| symbolling | Its assigned insurance risk rating, A value of +3 indicates that the auto is risky, -3 that it is probably pretty safe.(Categorical)  |
| wheelbase | Weelbase of car (Numeric) |
| carlength |  Length of car (Numeric) |
| carwidth | Width of car (Numeric) |
| carheight | height of car (Numeric) |
| curbweight | The weight of a car without occupants or baggage. (Numeric) |
| enginesize | Size of car (Numeric) |
| boreratio | Boreratio of car (Numeric) |
| stroke | Stroke or volume inside the engine (Numeric) |
| compressionratio | compression ratio of car (Numeric) |
| horsepower | Horsepower (Numeric) |
| peakrpm | car peak rpm (Numeric) |
| citympg | Mileage in city (Numeric) |
| highwaympg | Mileage on highway (Numeric) |

### Missing Value

There is no missing value in the dataset

### Correlation Analysis

![Heat map for correlation](https://github.com/MinyeZhou429/MinyeZhou429.github.io/blob/main/截屏2022-12-14%20下午2.28.37.png)

It is noticed that among numeric variables:
- wheelbase has positive correlation with price of 58%.
- car length and car width have positive correlation with price of 68% and 76%.
- curbweight has positive correlation with price of 84%.
- enginesize has positive correlation with price of 87%.
- boreratio has positive correlation with price of 55%.
- horsepower has positive correlation with price of 81%.
- citympg and highwaympg have negative correlation with price of 69% and 70%.

### Goal

- Find powerful predictors of car price
- Construct accurate prediction models for car price
- Compare model performance

## Method

### Cross Validation

- K-fold Validation
- Data Splitting

### Modeling

*Parametric*
- Linear Regression
- LASSO Regression

*Non-Parametric*
- Random Forest
- Regression Tree

## Result

### Linear Regresson

Based on model summary and variable importance:

- Six covariates are statistically significant at 0.05 significance level
- Three variables have negative impact on the car price
- Twelve variables have positive impact on the car price
- Enginesize is the leading predictor for car price

![LM_importance](https://github.com/MinyeZhou429/MinyeZhou429.github.io/blob/main/截屏2022-12-14%20下午2.48.56.png)

Multicollinearity was checked by performing Variance Inflation Factor (VIF). Among fourteen VIF values, eight values are larger than 5, which means that eight variable exhibits correlation with other variables in the dataset.

![VIF](https://github.com/MinyeZhou429/MinyeZhou429.github.io/blob/main/截屏2022-12-14%20下午3.13.40.png)

The calculated R-square are:

|  | R-square |
| ------ | ------- |
| Training set | 0.8462 |
| Testing set | 0.8143 |

### LASSO Regression

*10-fold Cross Validation model* shows minimum lambda is 31.73.
![VIF](https://github.com/MinyeZhou429/MinyeZhou429.github.io/blob/main/截屏2022-12-14%20下午3.15.36.png)

Using the most optimal lambda as the parameter for LASSO regression, a model was fitted. The calculated R-square are:

|  | R-square |
| ------ | ------- |
| Training set | 0.8577 |
| Testing set | 0.8065 |

It is noticed that the difference between R-square on testing set and training set is larger than that of linear regression. This indicates that LASSO regression model may lack generalizability and exhibits more overfitting issue compared to the linear regression model.

### Random Forest

A Random Forest model was fitted on the dataset. Based on the plot below, as the number of trees increases to 100, the error decreases and tends to be stable. 

![RF](https://github.com/MinyeZhou429/MinyeZhou429.github.io/blob/main/截屏2022-12-14%20下午3.22.36.png)

The calculated R-square are:

|  | R-square |
| ------ | ------- |
| Training set | 0.9226 |
| Testing set | 0.9333 |

There is no big difference between the R-square on training set and R-square on testing set. The small difference indicates there is no over-fitting issue on random forest model.

Based on the IncNodePurity values, enginesize, curbweight, and horsepower are the most significant variables for the Random Forest model.
![RF_importance](https://github.com/MinyeZhou429/MinyeZhou429.github.io/blob/main/截屏2022-12-14%20下午3.24.20.png)

### Regression Tree

A regression tree was fitted to see whether better performance could be obtained. Here is the visualization of Regression tree:
![tree](https://github.com/MinyeZhou429/MinyeZhou429.github.io/blob/main/截屏2022-12-14%20下午3.26.44.png)

Based on the plot, first split occurred based on enginesize. The second split occurred based on curbweight. And the third split occurred based on curbweight and carwidth. The splits indicate that the most significant predictors in regression trees are enginesize, curbweight, and carwidth. 

The calculated R-square are:

|  | R-square |
| ------ | ------- |
| Training set | 0.90 |
| Testing set | 0.84 |

The difference is not very large, which indicated there is no dramatic overfitting issues.

### Model Comparison

- Random Forest model has the largest R-square, which indicates that Random Forest model has the best performance among all models. 
- Random Forest model has the smallest difference in R-square between training set and testing set. The small R-square difference shows that Random Forest model has the best generalizability. 
- Parametric methods have lower R-square than non-parametric methods.

![tree](https://github.com/MinyeZhou429/MinyeZhou429.github.io/blob/main/截屏2022-12-14%20下午8.20.34.png)


## Discussion

### Main Finding

- enginesize is the most powerful predictor for car price
- Random Forest model has the best performance based on the R-square
- parametric models are preferred for this dataset

### Limitation

- Excluding categorical data may decrease the model performance since they could provide some important information like car body, drive wheel, and engine type
- Small testing set siz may potentially cause the large difference of R-square between testing set and training set

### Future Direction

- car price could be transformed into categorical variable so that classification algorithms could be applied
- Perform feature engineering
- The model could be tested on larger dataset to increase its generalizability

## Reference
 
[1]Llp, F. &. L. (2022, July 27). Litigation and Governmental Regulation in Response to Record Vehicle Prices in the Wake of COVID-19. Blogs | Dashboard Insights | Foley & Lardner LLP. https://www.foley.com/en/insights/publications/2022/07/litigation-govt-regulation-record-vehicle-prices

[2] Jeffrey C. Schlimmer (1985). UCI Machine Learning Repository [https://archive.ics.uci.edu/ml/datasets/Automobile]. Irvine, CA: University of California, School of Information and Computer Science.

[3] Regression Trees. (2015, December 30). Solver. https://www.solver.com/regression-trees
