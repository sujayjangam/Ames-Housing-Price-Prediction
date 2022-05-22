# Ames Housing Data and Kaggle Challenge

## Overview

From some outside research, we come to know that the author of the data set, "Dean De Cock", obtained the dataset directly from the City Assessor's Office in Iowa. 

He removed any variables that required special knowledge or previous calculations for use in the project scenario. Of the 80 variables that remained, they were all directly related to property sales in one way or another. 

He highlights a variables that might be of special interest to us, `PID`. 
`PID` is the Parcel Identification Number assigned to each property within the Ames Assessor’s system. This number can be used in conjunction with [the Assessor’s Office](http://www.cityofames.org/assessor/) website to directly view the records of a particular observation. The typical record will indicate the values for characteristics commonly quoted on most home flyers and will include a picture of the property.

This may be useful as we proceed with the preliminary data cleaning on this data set.
Additionally the [Data Dictionary](http://jse.amstat.org/v19n3/decock/DataDocumentation.txt) for this dataset will surely be useful when cleaning the data.

---

## Problem Statement

A team of data scientists, which I am a part of, have been hired by an interior design and renovation firm. They are based in Ames, Iowa, and they have a dataset pertaining to properties there. 

They have a few home owners who have come to them, seeking their help in renovating their home and reselling it at a profit. The firm's aim is to featch the most attractive price possible for their potential clients, and present a plan to them on how they would go about it. However they are unsure what are some of the steps they could take to achieve this.

We hope to provide recommendations on how this firm can go about this, at the end of the analysis and modeling process.

---

### Datasets

#### Provided Data used

There were two datasets provided, a train dataset, and a test dataset.
The remaining datasets were created as a byproduct of cleaning as well as Kaggle Submission.

* [`train.csv`](datasets/train.csv): Provided train dataset
* [`train_cleaned.csv`](datasets/train_cleaned.csv): Cleaned train dataset 
* [`train_modeling.csv`](datasets/train_modeling.csv): Test dataset ready to be used for modeling  
* [`test.csv`](datasets/test.csv): Provided test dataset 
* [`test_cleaned.csv`](datasets/test_cleaned.csv): Cleaned test dataset
* [`test_modeling.csv`](datasets/test_modeling.csv): Test dataset ready to be used for modeling 
* [`kaggle_submission_sujayjangam.csv`](datasets/kaggle_submission_sujayjangam.csv): Kaggle Submission with predicted values of `SalePrice` for the test dataset.

---

### Data Dictionary

A detailed data Dictionary can be found [here.](http://jse.amstat.org/v19n3/decock/DataDocumentation.txt)

### Brief Summary of Analysis

#### Cleaning:
1. First of all, I explored the data files provided. It was clear that there were many missing data, 9,822 to be exact. In a file with 2051 rows, this was an alarming number of missing data.
2. Most of the missing data was interpreted from the Data Dictionary, and could be interpreted to 'None' values. However for `Lot Frontage` we had to impute the values using the mean Square Footage in each neighborhood.


#### Encoding, EDA and Feature Selection:
1. Once the files were all clean, we set about carrying out manual encoding or one-hot encoding. This needs to be done so that we may feed features from our data set into our model.
2. Along the way, we dropped columns where we saw little to no variance. Columns where there was indication of multicollinearity were also dropped, keeping one of them.
3. Upon investigation of trends in the data, we saw that there were strong indicators of correlation in 4 main groups with our target, `SalePrice`.
    - Square Footage
    - Quality of the Property
    - Location
    - Others, e.g. Age of property
4. We isolated features that fell into these groups, and eventually begain the modeling process.

#### Modeling:
1. We began with Linear Regression models, where we iterated through starting with a small number of features, and eventually including all the features that were in our 4 groups above.
2. We move to using Regularisation and found that the Lasso model had the best Root Mean Squared Error of 27,904.
3. After creating our final model, we fed all our remaining data into our final model and generate the predictions for Kaggle.
4. Afterwhich, we dove back into our final model to gain insights towards our problem statement.

---

### Conclusions and Recommendations:

#### Recommendations:
1. Try to increase the overall and exterior quality of their home through renovation.
2. Ensure Heating Quality is excellent, and consider changing Heating type to Wall Furnace, if you have any other style.
3. Switch to a cement, brick or vinyl siding, wood shingles exterior. Avoid hardboard, wood siding, or plywood. A change is especially needed if you have one of these three.
4. Improve garage size.
5. The house style that created a maximum improvement in `SalePrice` was the 1 storey type, followed by Split Foyer and Split Level.
6. Increase Basement Square Footage if possible.
7. If there are no Bathrooms in the basement, add a full Bath, or a half Bath if full is not possible
8. If you already have a half bath, consider upgrading to full bath.

With these suggestions, clients will surely see an increase in the value of the `SalePrice` of their property.

    
#### Model Shortcomings: 
1. While this model generalizes well to the city of Ames, it's probably not generalizable to other cities, given that each city tends to differ greatly in terms of external factors.

2. Another point to keep in mind that this model doesn't take into account the inflation of housing prices. Since the end of the financial crisis in 2008, housing prices throughout the US have been increasing steadily year over year. The model will need to take this factor into account and would need retraining with new data, and most likely it would affect the feature selection as well.

**Improvements**:
- One improvement to make is to insist that all data is filled in before presented to us
- Another improvement is to select features algorithmically instead of common sense so as to ensure no important features are missed out.
- Account for interactivity between factors, e.g. A house that is 1 Storey AND has a Basement vs one that is only 1 Storey with no Basement.
