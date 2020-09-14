# Determine the Cause of A Collision

## Introduction
A traffic accident may be caused by objective factors, such as weather, address type, condition of the road, light conditions, or due to human factors, such as inattention, speeding, drinking.If it is an objective reason, we need to improve the traffic conditions in the streets where collisions often occur.If it is a subjective reason, the corresponding evidence needs to be collected.When a traffic accident occurs, initial forecasts of the cause will facilitate the traffic police to investigate the accident. So the traffic office may be interested in this study.
In this study, I will build a model to predict whether a collision is caused by human factors or not.

## Data
### Data understanding
I will use the example data of traffic accidents in Seattle City. The data set recorded the weather, the condition of the road, the light conditions, when a collision happened，and the behavior of the driver. If a driver was inattention, speeding or under the influence of alcohol,  the accident was due to human factors.
### Feature selection
I selected several relevant attributes from the dataset：
+ "SEVERITYCODE":A code that corresponds to the severity of the collision:
    * 3—fatality;
    * 2b—serious injury;
    * 2—injury;
    * 1—prop damage;
    * 0—unknown.
+ "PERSONCOUNT": The total number of people involved in the collision.
+ "VEHCOUNT": The number of vehicles involved in the collision.
+ "ADDRTYPE":Collision address type
+ "WEATHER":A description of the weather conditions during the time of the collision.
+ "ROADCOND": The condition of the road during the collision.
+ "LIGHTCOND":The light conditions during the collision.
+ "INATTENTIONIND":Whether or not collision was due to inattention. (Y/N)
+ "UNDERINFL": Whether or not a driver involved was under the influence of drugs or alcohol.
+ "SPEEDING": Whether or not speeding was a factor in the collision. (Y/N)

### Data Preparation
There are several problems with the datasets.
First, a labeled attribute needs to be created which represents the accident caused by human factors. If there is any inattention, speeding, drunk driving, etc., the labeled attribute will be marked as "1 ", otherwise marked as "0".
Second, there are some missing data in the datasets, such as "Unknown" in the 'ADDRTYPE','WEATHER','ROADCOND' and 'LIGHTCOND'. I dropped the whole row which had missing data in it.
 
Third, in the column of 'LIGHTCOND', there are several types of "dark", including "Dark - Street Lights On","Dark - No Street Lights","Dark - Street Lights Off" and "Dark - Unknown Lighting". I merged them into the same type as "Dark".
 
Finally, I converted the columns of'ADDRTYPE','WEATHER','ROADCOND' and'LIGHTCOND' to one-hot codes.


## Modeling
### Data Visualization
After data preparation,the distribution of data is as follows.
![alt "ADDRTYPE"](https://github.com/timeng27/Coursera_Capstone/blob/master/ADDRTYPE.png?raw=true)
![alt "WEATHER"](https://github.com/timeng27/Coursera_Capstone/blob/master/WEATHER.png?raw=true)
![alt "ROADCOND"](https://github.com/timeng27/Coursera_Capstone/blob/master/ROADCOND.png?raw=true)
![alt "LIGHTCOND"](https://github.com/timeng27/Coursera_Capstone/blob/master/LIGHTCOND.png?raw=true)

### Split Data
Split the datasets into train data and test data.

### Classing
Use the training set to build several classing model,including "K Nearest Neighbor", "Decision Tree", "Support Vector Machine" and "Logistic Regression". Then use the test set to report the accuracy of the model.

## Results 
The following shows the accuracy of the built models using different evaluation metrics, including Jaccard, F1-score and confusion matrix. 
The accuracy of models is near 75%. However, accidents due to objective reasons also reach 74.22%. That means the results are not better than guessing.

|Algorithm|Jaccard |F1-score|
|  :----:  | :----:  | :----:  |
| KNN    | 0.725  | 0.208  |
| SVM    | 0.746  | 0.106  |
| Decision Tree |  0.748 | 0.182  |
| LogisticRegression   | 0.745  | 0.016  |

![alt "KNN"](https://github.com/timeng27/Coursera_Capstone/blob/master/KNN.png?raw=true)
![alt "sVM"](https://github.com/timeng27/Coursera_Capstone/blob/master/SVM.png?raw=true)
![alt "DT"](https://github.com/timeng27/Coursera_Capstone/blob/master/DTree.png?raw=true)
![alt "LR"](https://github.com/timeng27/Coursera_Capstone/blob/master/LR.png?raw=true)


## Evaluation
In this study, I try to predict whether a collision is caused by human factors. But honestly, all of the results from the built models are not better than guessing directly. It may be due to the following reasons.
1. The features selected are not correct.
2. The shared data has unbalanced labels. I didn't balance the data well, and created biased ML models.
3. The ML models are under-fitting.


