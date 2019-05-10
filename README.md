# Animal Shelter Outcome Classification
Classification Project - Predicting whether animals of Sonoma County Animal Shelter will be adopted, returned to their owner, transferred, or euthanized 

## Data
Data came from [County of Sonoma Department of Health Services](https://data.sonomacounty.ca.gov/Government/Animal-Shelter-Intake-and-Outcome/924a-vesw)

The Target classes and value count for each class were: 



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
