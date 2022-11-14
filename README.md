# King County Housing Price Analysis
***
### Overview
Using the housing data from the King County dataset, this project aims to analyze the features of a house that impacts sale price the most. I will be exploring this dataset and performing multiple linear regression analysis.

### Business Problem
The stackholder of this projet is a real estate agency in King County. My multiple linear regression analysis will provide them with pricing information for their clients buying and selling homes.

### Data Understanding
This dataset contains housing sale data from King County, Washington. 
- id - Unique identifier for a house
- date - Date house was sold
- price - Sale price (prediction target)
- bedrooms - Number of bedrooms
- bathrooms - Number of bathrooms
- sqft_living - Square footage of living space in the home
- sqft_lot - Square footage of the lot
- floors - Number of floors (levels) in house
- waterfront - Whether the house is on a waterfront
- view - Quality of view from house
- grade - Overall grade of the house. Related to the construction and design of the house.
- sqft_above - Square footage of house apart from basement
- sqft_basement - Square footage of the basement
- yr_built - Year when house was built
- yr_renovated - Year when house was renovated
- zipcode - ZIP Code used by the United States Postal Service
- lat - Latitude coordinate
- long - Longitude coordinate
- sqft_living15 - The square footage of interior housing living space for the nearest 15 neighbors
- sqft_lot15 - The square footage of the land lots of the nearest 15 neighbors

### Modeling
After cleaning the data and transforming ordinal variables, like 'view', 'grade', 'condition', into numerical values, I examined the features correlations with 'price' and with one another. 

I noticed a few key features with strong correlation:
- 'sqft_living', 'bathrooms', 'sqft_above', 'sqft_living15'
- 'grade'
I found 'sqft_living' to be strongly correlated with other features that correlated with 'price'. Because of this, I only used 'sqft_living' in my modeling because it has the strongest correlation with 'price' out of tthese correlated variables.

Before creating my model, I normalized 'price' and 'sqft_living' with log transformation. Then, I used those as my baseline model with 'sqft_living' as my predictor.

I then improved my modeling by adding another feature, 'grade', that strongly correlated with 'price'. I normalized that as well and tested the model.

Finally, I took 'zipcode'. This feature was a numerical value however it doesn't properly represent the feature. Zip codes are numbers but they represent a location and should be treated as a categorical variable, so I used One Hot Encoding on the feature before adding it to my model.

### Findings
Below is the R-squared results of my models
- Baseline model (only 'sqft_living'): 0.455
- Second model ('sqft_living' and 'grade'): 0.537
- Final model (adding encoded 'zipcode' data): 0.839

Model Coefficients:
- 'sqft_living': 0.559 which suggests that for every % increase in 'sqft_living', price will increase by 0.559%.
- 'grade': 0.867 which suggests that for every % increase in 'grade', price will increase by 0.867%
- 'zipcode': 98112, 98004, 98039 are the 3 zip codes with sale prices that are on average over 100% higher than the other zip codes in  King County.

Through 5-fold cross validation and a train test split, the Mean Squared Errors were all similar and around 0.045 throughout.

### Concluding Thoughts
My analysis suggests that 'sqft_living', 'grade', and 'zipcode' are the features that most influence higher sale prices.

Because of that, I would recommend the real estate agency focus on the following with regards to their pricing:
- Square Footage of the House
- Construction and Design Quality of the House
- Location of the House

## Repository Structure
├── README.md                                        <- The top-level README for reviewers of this project
├── king-county-housing-analysis.ipynb               <- Narrative documentation of analysis in Jupyter notebook
├── King_County_Housing_Presentation.pdf             <- PDF version of project presentation

└── data                                             <- King County Housing Dataset