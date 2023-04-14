# Project 2 - Ames Housing Data and Kaggle Challenge

## Home Sale Price Estimator for Zillow
### Daniel Rossetti, Data Science Consultant Hired by Zillow


# 1. Problem Statement:
Zillow wishes to prototype a home sale price estimator that can be used by website users to estimate the value of their home or home they wish to buy.  Home sale data from Ames, Iowa have been provided as a starter set and include information on almost 80 different attributes of the home or the sale itself.  This data will be used to train a linear regression model which will use a subset of these attributes to predict a home sale price.  The model quality will be evaluated against the mean absolute error of the predictions on the training dataset selected.  The target error is to be within $30,000 of the actual home price on average.  If successful, the methods used to create this prototype model will be employed to predict home values in other areas of the country to understand it's general applicability with the ultimate goal of being rolled out onto the Zillow website for users.

# 2. Description of Data, Overview of Feature Analysis, and Modeling
## 2.1 Description of Data
Data were provided for home sales in the city of Ames, Iowa between 2006 and 2010.  The data can be found [here](https://www.kaggle.com/competitions/dsir-320-project-2-regression-challenge/data).

A total of 2051 individual home sales are included in this dataset which was split into training and test datasets with 1435 and 616 samples respectively (representing a 70/30 split).

Of the data provided, the following features were selected for use in the final model:
* Total basement square footage
* Garage square footage
* Overall home quality
* Year the home was remodeled or added to
* Total square feet, 
* Square footage of masonry
* Number of fireplaces
* Neighborhood

Additional features were created using the data above to improve model performance.  A full list of features can be found in the appendix of this executive summary.

## 2.2 - Feature Analysis
Features were selected for modeling which:
* Are a common characteristic that a home buyer or seller may be intersted in
* Showed a decent correlation to the sale price
* Were shown to improve model performance

## 2.3 - Modeling
A simple liear regression model was built, and features were added or removed iteratively to continually improve the performance of the model.  See Appendix B for more information on how this model works.

# 3 - Model Performance

The final model met the overall requirement that the average sale price error (in either direction) be within $30k. The mean absolute error values in the table below are far below that limit.  Overall, the vast majority of the home prices were predicted to be within \\$30k of the true sale price with 83.8% achieving this metric.

The R-Squared values below indicate two things:
* Almost 90% of the variabilty in sale price is accounted for by this model with the features selected
* Model has an excellent balance between bias and variance with the R-Squared values on both the training and testing data being nearly identical
    * This would suggest that this model would provide similar performnace on new data passed throgh it

| Performance Metric            | data_7_poly_nbr_log |
|-------------------------------|---------------------|
| R-Squared, Training Data                 | 0.8946              |
| R-Sqaured, Testing Data                  | 0.8921              |
| RMSE, Training Data                      | $25,789             |
| RMSE, Testing Data                       | $25,887             |
| Mean Absolute Error (MAE), Training Data | $17,692             |
| Mean Absolute Error (MAE), Testing Data  | $18,643             |
| Percentage Within $30k, Training Data    | 83.7631%            |

A total of seven other models were attemtped, however, none delivered performacne metrics as good as those of the final model above.  Ridge and Lasso regularization techniques were attempted with the final model as well, but as the model already had an excellent balance of bias and variance, regularization only decreased model performance.  A comparison of all models with their performance metrics can be found in Appendix C and the code notebook.





# 4 - Model Limitations and Additional Refinements
* Stated previously, these models are not geared towards inference and shound not be used to establish confident relationships between the selected features and the target variable
* With more time, more attention could be given to categorical variables which may help to better characterize the sale prices of higher value homes than the current model
* The model could stand to be de-featured to make room for other higher-correlation features.  While it has been stated that multicolinearity exists but is acceptable, some terms may be found to be redundant with more time

# 5 - Conclusions:
* A model can be created which will predict home prices in Ames Iowa within a Mean Absolute Error (MAE) \\$30,000
    * With the final model, 83.8% of sale prices were prediced to within $30,000 (on the training data)
* The model exibits a good balance of bias and variance as the R-sqaured terms of this model on both the training and test data are nearly identical
* The model can be further refined to incorporate more features, but as it stands, must collect the following information from users when estimating a home sale price:
    * Total basement square footage
    * Garage square footage
    * Overall quality of the home on a 1 - 10 scale with 1 being poor and 10 being excellent
    * Year the home was remodeled or added to, defaulting to the year it was built if not remodeled or added to
    * Total Square footage (not including the basement and garage) also known as the 'graded living area'
    * Square footage of masonry veneer
    * Number of fireplaces in the home
    * Neighborhood in which the home resides
    
# 6 - Next Steps:
* The characterisitcs of homes with absolute sale price errors exceeding \\$30,000 should be examined to determine if they exhibit and particular traits that could be better modeled in a future verson of this model
    * A framework for this analysis has been established in Appendix B, though the analysis was not able to be completed in time
* The model should first be optimized by removing features that appear to be redundant or colinear with other features that do not noticably increase the performance of the model when included
* Additional categorical variables can be encoded and evluated for correlation with the sales price to possibly be included in a future version of this model
* Test this model on housing data from other time periods and other areas of the country to determine national applicability
__________________________________________
# Appendix A - Data Dictionary for Final Model

| Feature                      | Data Type | Dataset                     | Description                                                                            |
|------------------------------|-----------|-----------------------------|----------------------------------------------------------------------------------------|
| Total Bsmt SF                | Float64   | Kaggle, Ames, Iowa          | TotalBsmtSF: Total square feet of basement area                                        |
| Garage Area                  | Float64   | Kaggle, Ames, Iowa          | GarageArea: Size of garage in square feet                                              |
| Overall Qual                 | Float64   | Kaggle, Ames, Iowa          | OverallQual: Overall material and finish quality                                       |
| Year Remod/Add               | Float64   | Kaggle, Ames, Iowa          | YearRemodAdd: Remodel date (same as construction date if no remodeling or   additions) |
| Gr Liv Area                  | Float64   | Kaggle, Ames, Iowa          | GrLivArea: Above grade (ground) living area square feet                                |
| Mas Vnr Area                 | Float64   | Kaggle, Ames, Iowa          | MasVnrArea: Masonry veneer area in square feet                                         |
| Fireplaces                   | Float64   | Kaggle, Ames, Iowa          | Fireplaces: Number of fireplaces                                                       |
| Total Bsmt SF^2              | Float64   | Derived                     | Second order interaction term                                                          |
| Total Bsmt SF Garage Area    | Float64   | Derived                     | First order interaction term                                                           |
| Total Bsmt SF Overall Qual   | Float64   | Derived                     | First order interaction term                                                           |
| Total Bsmt SF Year Remod/Add | Float64   | Derived                     | First order interaction term                                                           |
| Total Bsmt SF Gr Liv Area    | Float64   | Derived                     | First order interaction term                                                           |
| Total Bsmt SF Mas Vnr Area   | Float64   | Derived                     | First order interaction term                                                           |
| Total Bsmt SF Fireplaces     | Float64   | Derived                     | First order interaction term                                                           |
| Garage Area^2                | Float64   | Derived                     | Second order interaction term                                                          |
| Garage Area Overall Qual     | Float64   | Derived                     | First order interaction term                                                           |
| Garage Area Year Remod/Add   | Float64   | Derived                     | First order interaction term                                                           |
| Garage Area Gr Liv Area      | Float64   | Derived                     | First order interaction term                                                           |
| Garage Area Mas Vnr Area     | Float64   | Derived                     | First order interaction term                                                           |
| Garage Area Fireplaces       | Float64   | Derived                     | First order interaction term                                                           |
| Overall Qual^2               | Float64   | Derived                     | Second order interaction term                                                          |
| Overall Qual Year Remod/Add  | Float64   | Derived                     | First order interaction term                                                           |
| Overall Qual Gr Liv Area     | Float64   | Derived                     | First order interaction term                                                           |
| Overall Qual Mas Vnr Area    | Float64   | Derived                     | First order interaction term                                                           |
| Overall Qual Fireplaces      | Float64   | Derived                     | First order interaction term                                                           |
| Year Remod/Add^2             | Float64   | Derived                     | Second order interaction term                                                          |
| Year Remod/Add Gr Liv Area   | Float64   | Derived                     | First order interaction term                                                           |
| Year Remod/Add Mas Vnr Area  | Float64   | Derived                     | First order interaction term                                                           |
| Year Remod/Add Fireplaces    | Float64   | Derived                     | First order interaction term                                                           |
| Gr Liv Area^2                | Float64   | Derived                     | Second order interaction term                                                          |
| Gr Liv Area Mas Vnr Area     | Float64   | Derived                     | First order interaction term                                                           |
| Gr Liv Area Fireplaces       | Float64   | Derived                     | First order interaction term                                                           |
| Mas Vnr Area^2               | Float64   | Derived                     | Second order interaction term                                                          |
| Mas Vnr Area Fireplaces      | Float64   | Derived                     | First order interaction term                                                           |
| Fireplaces^2                 | Float64   | Derived                     | Second order interaction term                                                          |
| Neighborhood_Edwards         | uint8     | Kaggle, Ames, Iowa, Encoded | Neighborhood: Physical locations within Ames city limits                               |
| Neighborhood_IDOTRR          | uint8     | Kaggle, Ames, Iowa, Encoded | Neighborhood: Physical locations within Ames city limits                               |
| Neighborhood_NAmes           | uint8     | Kaggle, Ames, Iowa, Encoded | Neighborhood: Physical locations within Ames city limits                               |
| Neighborhood_NoRidge         | uint8     | Kaggle, Ames, Iowa, Encoded | Neighborhood: Physical locations within Ames city limits                               |
| Neighborhood_NridgHt         | uint8     | Kaggle, Ames, Iowa, Encoded | Neighborhood: Physical locations within Ames city limits                               |
| Neighborhood_OldTown         | uint8     | Kaggle, Ames, Iowa, Encoded | Neighborhood: Physical locations within Ames city limits                               |
| Neighborhood_Somerst         | uint8     | Kaggle, Ames, Iowa, Encoded | Neighborhood: Physical locations within Ames city limits                               |
| Neighborhood_StoneBr         | uint8     | Kaggle, Ames, Iowa, Encoded | Neighborhood: Physical locations within Ames city limits                               |
    
Codebook / Data Dictionary Entries for Original Features (not interaction terms) Taken Directly from the Kaggle Competition Site: [link](https://www.kaggle.com/competitions/dsir-320-project-2-regression-challenge/data)

# Appendix B - How this Model Works
This model takes in the numerical features listed above which were selected for their correlation to sale price or impact on model performance. These numerical features are then used to create interaction terms which are products of each of these features and themselves creating first and second order polynomial terms. Including these polynomial features was found to greatly enhance the model performance. Categorical columns which were one hot encoded are included for eight of the 28 total neighborhoods in Ames, Iowa which - when included in the model - enhanced its performance.  The model itself is a simple linear regression model performing ordinary least squares regression. The model is fitted against log-transformed sale price data as this was seen to improve performance. The predictions made by this model are themselves log data which are then exponentiated to return outputs in the original sale price units of dollars.

# Appendix C - Comparison of Models Attemtped
|                 | ILR     | data_1  | data_2  | data_3  | data_4  | data_5_poly | data_6_poly | data_7_poly_nbr (Final) | data_7_poly_nbr_log | data_7_poly_nbr_log_ridge | data_7_poly_nbr_log_lasso |
|-----------------|---------|---------|---------|---------|---------|-------------|-------------|-------------------------|---------------------|---------------------------|---------------------------|
| R2_train        | 0.8621  | 0.8269  | 0.8556  | 0.8743  | 0.8262  | 0.8735      | 0.8817      | 0.8902                  | 0.8946              | 0.8935                    | 0.8919                    |
| R2_test         | 0.7976  | 0.7389  | 0.7856  | 0.7769  | 0.7521  | 0.8697      | 0.8715      | 0.876                   | 0.8921              | 0.8888                    | 0.8876                    |
| RMSE_train      | 29492   | 33043   | 30177   | 28155   | 33114   | 28250       | 27314       | 26319                   | 25789               | 25921                     | 26111                     |
| RMSE_test       | 35452   | 40265   | 36486   | 37221   | 39233   | 28437       | 28241       | 27749                   | 25887               | 26279                     | 26417                     |
| mae_train       | 19786   | 22611   | 20319   | 18457   | 21256   | 19571       | 19080       | 18437                   | 17692               | 17745                     | 17879                     |
| mae_test        | 20797   | 23716   | 21498   | 20792   | 22618   | 20062       | 19799       | 19569                   | 18643               | 18671                     | 18779                     |
| Within $30k (%) | 80.8362 | 75.4007 | 79.6516 | 82.7178 | 78.9547 | 81.324      | 81.5331     | 82.2997                 | 83.7631             | 83.554                    | 83.2753                   |
| cv_train_mean   | 0.8232  | 0.7921  | 0.8214  | 0.8358  | 0.8188  | 0.8135      | 0.7955      | 0.8067                  | 0.8067              | NaN                       | NaN                       |
| cv_train_1      | 0.8366  | 0.8321  | 0.8385  | 0.8737  | 0.859   | 0.8575      | 0.8737      | 0.8732                  | 0.8732              | NaN                       | NaN                       |
| cv_train_2      | 0.8572  | 0.8141  | 0.8529  | 0.8802  | 0.8415  | 0.8554      | 0.8605      | 0.874                   | 0.874               | NaN                       | NaN                       |
| cv_train_3      | 0.7984  | 0.7651  | 0.8056  | 0.8111  | 0.8369  | 0.8646      | 0.8517      | 0.8614                  | 0.8614              | NaN                       | NaN                       |
| cv_train_4      | 0.854   | 0.8431  | 0.849   | 0.8609  | 0.8626  | 0.8638      | 0.8691      | 0.8772                  | 0.8772              | NaN                       | NaN                       |
| cv_train_5      | 0.7699  | 0.706   | 0.7608  | 0.7532  | 0.6939  | 0.6263      | 0.5223      | 0.5479                  | 0.5479              | NaN                       | NaN                       |
| R2_train_log    | NaN     | NaN     | NaN     | NaN     | NaN     | NaN         | NaN         | NaN                     | 0.8768              | 0.8729                    | 0.8735                    |
| R2_test_log     | NaN     | NaN     | NaN     | NaN     | NaN     | NaN         | NaN         | NaN                     | 0.8662              | 0.8676                    | 0.8664                    |