# Animal Shelter Outcome Classification
Classification Project - Predicting whether animals of Sonoma County Animal Shelter will be adopted, returned to their owner, transferred, or euthanized 

- [Data](#data)
- [EDA](#eda)
  - [Taking a look at Outcome based on different variables:](#taking-a-look-at-outcome-based-on-different-variables)
- [Modeling](#modeling)
- [Next Steps](#next-steps)

## Data
Data came from [County of Sonoma Department of Health Services](https://data.sonomacounty.ca.gov/Government/Animal-Shelter-Intake-and-Outcome/924a-vesw). Animal intake dates ranged from 8/16/2013 to 5/4/2019.  My final (cleaned) dataset had 16,457 data points. 

The Target classes and value count for each class were: 

![targets](https://github.com/MsJacksonIYN/PetAdoptionClassification/blob/master/viz/targets.png)


The features I used were:
- **Type**: Animal Type (Cat, Dog, Other)
- **Sex**: Male, Female, Neutered, Spayed, Unkown
- **Size**: Toy, Small, Medium, Large, X-Large
- **Intake Type**: Reason for intake (i.e. Stray, Owner Surrender, Confiscation, etc.)
- **Intake Subtype**: Sub-reason for intake (i.e. Field, Over the Counter)
- **Intake Condition**: Health & rehabilitation status upon intake
- **Intake Jurisdiction**
- **PredomBreed**: Breed.  Where animal was mixed breed, first breed listed
- **PredomColor**: Color of animal.  Where animal was multi-colored, first color listed
- **Days in Shelter**: # of Days animal spent in shelter
- **IntakeAgeYrs**: Intake Date - Birth Date (in years)
Plus Interaction terms for these features.

## EDA
My biggest issue with this dataset was that all features were categorical.  This meant that if I were to One Hot Encode all of my features, the dimensions of my dataset would be huge.  So I spent a good amount of time cleaning up categories such as "Breed" and "Color" into "PredomBreed" (Predominant Breed) and "PredomColor" (Predominant Color).  Below are the final Breeds included in modeling:

**Cat Breeds:**

![cats](https://github.com/MsJacksonIYN/PetAdoptionClassification/blob/master/viz/cat_breeds.png)

**Dog Breeds:**

![dogs](https://github.com/MsJacksonIYN/PetAdoptionClassification/blob/master/viz/dog_breeds.png)

**Other Breeds:**

![other](https://github.com/MsJacksonIYN/PetAdoptionClassification/blob/master/viz/other_breeds.png)

### Taking a look at Outcome based on different variables: 

**Intake Condition:** <br>
It's easy to see that healthy anmials usually are adopted or returned to their original owner.  Only animals labeled "Untreatable" have a high concentration of Euthanization.


![intake condition](https://github.com/MsJacksonIYN/PetAdoptionClassification/blob/master/viz/outcome_by_intakecond.png)

**Days In Shelter:** <br>
Animals that they are trying to find new homes for (adoption) tend to stay in the shelter the longest.

![days in shelter](https://github.com/MsJacksonIYN/PetAdoptionClassification/blob/master/viz/days_in_shelter.png)


## Modeling
For modeling, I created LabelEncoded my categorical variables for the sake of time and keeping dimensionality low.  I then created interaction terms for all of my variables.  When all was said and done I had 66 features that were loaded into each model. 

**Models Attempted**
 - Logistic Regression
    - Accuracy: .7193
 - Logistic Regression with SMOTE upsampling
    - Accuracy: .6938
- Decision Tree
    - Accuracy: .8275
 - Decision Tree with SMOTE upsampling
    - Accuracy: .8281
- KNN
    - Accuracy: .7913
 - KNN with SMOTE upsampling
    - Accuracy: .7795
- Random Forrest
    - Accuracy: .8615
 - Random Forrest with SMOTE upsampling
    - Accuracy: .8600
 - XGBoost
    - Accuracy: .8639

**My objective** was to reduce the amount of False Positives for Euthanization (# of times animals were incorrectly predicted to be Euthanized), so I selected the model that minimized this number: XGBoost.

For Reference: 
- 0 = Adoption
- 1 = Euthanize
- 2 = Return to Owner
- 3 = Transfer

![conf matrix](https://github.com/MsJacksonIYN/PetAdoptionClassification/blob/master/viz/conf_matrix_xgb.png)

Taking a look at feature importance shows that important features include Intake Condition, Days in Shelter, Sex, and Type

![feat importance](https://github.com/MsJacksonIYN/PetAdoptionClassification/blob/master/viz/feature_importance.png)

## Next Steps
With more time, I would like to One Hot encode the variables that aren't ordinal, and spend more time looking at feature importance to tune and reduce complexity of my models.
