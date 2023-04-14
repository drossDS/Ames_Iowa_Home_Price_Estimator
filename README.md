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

The model met the overall requirement that the average sale price error (in either direction) be within $30k. The mean absolute error values in the table below are far below that limit.  Overall, the vast majority of the home prices were predicted to be within \\$30k of the true sale price with 83.8% achieving this metric.

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
