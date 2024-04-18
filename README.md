####### Introduction:
In this project, we want to use a variety of algorithms and classifiers to predict the type of tree cover in a sample area within Roosevelt National Forest of Northern Colorado given various other features about the area, including the soil type, the vertical and horizontal distance to hydrology, the elevation, etc. 
Using 13 temporal and geographic variables, the goal of this project is to classify the type of tree 
cover in the Roosevelt National Forest of northern Colorado, just outside of Fort Collins. The 
forest consists of 6 wilderness areas that have, according to the University of California, Irvine’s 
project repository, experienced minimal human disturbances, leaving the tree cover to be the 
result of natural processes.
The actual forest cover type for a given observation (30 x 30 m cell) was determined from US 
Forest Service (USFS) Region 2 Resource Information System (RIS) data. Independent variables 
were derived from data originally obtained from US Geological Survey (USGS) and USFS data. 
Data is in raw form (not scaled) and contains binary (0 or 1) columns of data for qualitative 
independent variables (wilderness areas and soil types). This study area includes four wilderness 
areas located in the Roosevelt National Forest of northern Colorado. These areas represent 
forests with minimal human-caused disturbances, so that existing forest cover types are more a 
result of ecological processes rather than forest management practices. 
Some background information for these four wilderness areas: Neota (area 2) probably has the 
highest mean elevational value of the 4 wilderness areas. Rawah (area 1) and Comanche Peak 
(area 3) would have a lower mean elevational value, while Cache la Poudre (area 4) would have 
the lowest mean elevational value. As for primary major tree species in these areas, Neota would 
have spruce/fir (type 1), while Rawah and Comanche Peak would probably have lodgepole pine 
(type 2) as their primary species, followed by spruce/fir and aspen (type 5). Cache la Poudre 
would tend to have Ponderosa pine (type 3), Douglas-fir (type 6), and cottonwood/willow (type 
4). The Rawah and Comanche Peak areas would tend to be more typical of the overall dataset 
than either the Neota or Cache la Poudre, due to their assortment of tree species and range of 
predictive variable values (elevation, etc.) Cache la Poudre would probably be more unique than 
the others, due to its relatively low elevation range and species composition.
In this project, we want to use a variety of algorithms and classifiers to predict the type of tree 
cover in a sample area within Roosevelt National Forest of Northern Colorado given various other 
features about the area, including the soil type, the vertical and horizontal distance to hydrology, 
the elevation, etc. We will use the following algorithms to make our predictions:
• K-Nearest Neighbor
• Decision Trees
• Naive Bayes
We will do some data exploration, preprocessing and other processes to ensure the algorithms 
we choose can make the best possible predictions. This dataset poses classification type of the 
problem.
**************************************************************************************************************************************
###### Dataset Description:
Link of the datset: https://archive.ics.uci.edu/dataset/31/covertype
Description of the features or parameters: Multivariate categorical and integer data
Number of Instances (Rows): 581012
Number of attributes (Columns): 52
Attribute Information:
• Cover_Type: One of seven types of tree cover found in the forest. In the data downloaded for 
the project, the observations are coded 1 through 7. We have renamed them for clarity. 
Observations are based on the primary cover type of 30m x 30m areas, as determined by the 
United States Forest Service. This is our response variable.
• Wilderness_Area: Of the six wilderness areas in the Roosevelt National Forest, four were used in 
this dataset. In the original dataset, these were one-hot encoded. 
• Soil_Type: 40 soil types were identified in the dataset and more detailed information regarding 
the types can be found at https://www.kaggle.com/uciml/forest-cover-type-dataset. 
• Elevation: The elevation of the observation in meters above sea level.
• Aspect: The aspect of the observation in degrees azimuth.
• Slope: The slope at which the observation is observed in degrees.
• Hillshade_9am: The amount of hillshade for the observation at 09:00 on the summer solstice. 
This is a value between 0 and 225.
• Hillshade_Noon: The amount of hillshade for the observation at 12:00 on the summer solstice. 
This is a value between 0 and 225.
• Hillshade_3pm: The amount of hillshade for the observation at 15:00 on the summer solstice. 
This is a value between 0 and 225.
• Vertical_Distance_To_Hydrology: Vertical distance to nearest water source in meters. Negative 
numbers indicate distance below a water source.
• Horizontal_Distance_To_Hydrology: Horizontal distance to nearest water source in meters.
• Horizontal_Distance_To_Roadways: Horizontal distance to nearest roadway in meters.
• Horizontal_Distance_To_Fire_Points: Horizontal distance to nearest wildfire ignition point in 
meters.
5
Code Designations:
Wilderness Areas: 1 -- Rawah Wilderness Area
2 -- Neota Wilderness Area
3 -- Comanche Peak Wilderness Area
4 -- Cache la Poudre Wilderness Area
Soil Types: 1 to 40 : based on the USFS Ecological
Landtype Units for this study area.
Forest Cover Types: 1 -- Spruce/Fir
2 -- Lodgepole Pine
3 -- Ponderosa Pine
4 -- Cottonwood/Willow
5 -- Aspen
6 -- Douglas-fir
7 -- Krummholz
Missing values: None
Class distribution:
 Number of records of Spruce-Fir: 211840 
Number of records of Lodgepole Pine: 283301 
Number of records of Ponderosa Pine: 35754 
Number of records of Cottonwood/Willow: 2747 
Number of records of Aspen: 9493 
Number of records of Douglas-fir: 17367 
Number of records of Krummholz: 20510

*************************************************************************************************************************************
####### Conclusions from EDA:
1. From the heat map, we can see the following positive and negative relationships:
Positive correlation pairs:
• Hillshade_9am and Aspect
• Hillshade_3pm and Aspect
• Horizontal_Distance_To_Hydrology and Vertical_Distance_To_Hydrology
• Horizontal_Distance_To_Roadways and Horizontal_Distance_To_Fire_Points
• Hillshade_3pm and Hillshade_Noon
Negative correlation pairs:
• Elevation and Horizontal_Distance_To_Hydrology
• Elevation and Horizontal_Distance_To_Roadways
• Aspect and Hillshade_9am
• Slope and Hillshade_Noon
• Hillshade_9am and Hillshade_3pm
• Wilderness_Area3 and Wilderness_Area1
2. Krummholz cover is found at very high elevations where other covers are rare. Not only do 
Krummholz and Cottonwood/Willow covers not share many of the same soil types, they 
aren’t found within nearly 500 meters of elevation to each other.
3. Cottonwood/Willow trees are only found in the Cache la Poudre area and Krummholz trees 
are only found in the upper elevations of the other three areas.
4. Krummholz and Lodgepole Pines can tolerate being further from hydrology.
5. For forest cover type 4, we notice it only has wilderness area 4. Forest cover 3 and 6 have a 
mix of Wideness are 3 and 4 Forest cover 5 has a mix of wilderness area 1 and 3 Forest cover 
types 1,2 and 7 have more than 2 wideness types. Infact forest cover type 2 has presennce of 
all 4 types of wilderness .
6. Fur (Forest cover type 1) and Pine (Forest cover type 2) are the most occurring forest cover 
type and found mostly in Wilderness area 1 and 2.
***********************************************************************************************************************************
##### Conclusions:
• Number of trees by Cover Type are as follows:
Lodgepole Pine: 283301
Spruce/Fir: 211840
Ponderosa Pine: 35754
Krummholz: 20510
Douglas Fir: 17367
Aspen: 9493
Cottonwood/Willow: 2747

• Elevation is the most important variable for all of the types of tree according to feature 
importance of Decision Tree classifier.
• Cottonwood/Willow trees are only found in the Cache la Poudre area and Krummholz trees 
are only found in the upper elevations of the other three areas.
• Krummholz cover is found at very high elevations where other covers are rare.
• Out of all 4 ML models KNN classifier is performing very well with an accuracy of 0.97.
• Naïve Bayes is not performing well with an accuracy of 0.46 because of class imbalance 
problem in our dataset.
