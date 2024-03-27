# Table of Content

1. [Overview](#overview)
2. [Motivation](#motivation)
3. [Exploratory Data Analysis](#exploratory-data-analysis)
4. [Data Preprocessing](#data-preprocessing)
5. [Model Justification](#model-justification)
6. [Model Building](#model-building)
7. [Model Evaluation and Project Assessment](#model-evaluation-and-project-assessment)
8. [Model Prediction and Accuracy Estimation](#model-prediction-and-accuracy-estimation)


## Overview
Workplace absenteeism, the habit or deliberate choice of not attending work, significantly affects organizational strategies by lowering productivity and increasing costs, including salaries and overtime payments. As highlighted by Cucchiella et al. (2014) and the U.S. Bureau of Labor Statistics (2022), which notes a 3.2% daily workforce absence rate, identifying and understanding its causes is crucial. Factors like workplace bullying, poor morale, inadequate rewards, mental health issues, and substance use contribute to absenteeism. This project aims to identify and analyze such factors using a 3-month data set and linear regression models, ultimately helping businesses minimize associated losses and improve their bottom line.

## Motivation
Drawing from my journey as a team leader across diverse departments, I've seen firsthand how absenteeism can throw a wrench into the gears of productivity. Fueled by this insight, I decided to wield the power of machine learning to dive deep into the root causes of absenteeism, predict its patterns, and forge strategies to preempt its occurrence. This project is a testament to how blending personal experience with cutting-edge technology can spark innovative solutions to age-old challenges.

## Exploratory Data Analysis 
Exploratory Data Analysis (EDA) serves as a crucial preliminary step in understanding the structure of a dataset. It offers insights into variable distributions, and relationships between variables, and aids in identifying anomalies such as outliers that may impact model accuracy.

Find the Dataset [HERE](https://github.com/Mattdozie/Predicting-Employee-Absenteeism-using-Linear-Regression-Models-in-R-/blob/main/absenteeism.csv)

### Missing Value Analysis
The dataset was meticulously examined for missing values, defined as essential but unavailable data points for analysis. The absence of missing values is crucial as they can distort analytical outcomes. Fortunately, the absenteeism dataset exhibits no missing values, as depicted below.

![image](https://github.com/Mattdozie/Predicting-Employee-Absenteeism-using-Linear-Regression-Models-in-R-/assets/100968289/9733d296-ab99-4ed0-b427-31c4c756eeb2)


                                                    Missing value analysis plot

### Univariate Graphical Exploratory Data Analysis
Univariate graphical EDA was conducted to unveil the underlying characteristics and distributions of dataset features. Histograms were employed to illustrate frequency distributions of numerical features, revealing their inherent characteristics.
![image](https://github.com/Mattdozie/Predicting-Employee-Absenteeism-using-Linear-Regression-Models-in-R-/assets/100968289/68ff290c-b73d-4948-a37a-ba8f2daf6e6f)

![image](https://github.com/Mattdozie/Predicting-Employee-Absenteeism-using-Linear-Regression-Models-in-R-/assets/100968289/0e3be1ea-ac3b-4527-9647-80d2ceb95367)
                                                  
                                                  Histogram Plots: Distribution of Numerical Features

The histograms indicated predominantly non-symmetric distributions, with features exhibiting left or right skewness, bimodality, or multimodality.

##### i. Transportation Expense
Transportation expense demonstrates a multimodal distribution, with approximately 45% of participants spending between £100-200 on transportation during the investigation period.

##### ii. Distance to Work
Like transportation expense, distance to work exhibits a multimodal distribution. Contrary to expectations, the scatterplot between transportation expense and distance to work doesn't demonstrate a linear correlation, suggesting variations in transportation expenses due to different modes of transportation.

![image](https://github.com/Mattdozie/Predicting-Employee-Absenteeism-using-Linear-Regression-Models-in-R-/assets/100968289/38dce5c5-a34d-452d-8526-91172a0b083a)

                                            Relationship between Transportation Expense and Distance to Work

##### iii. Age
The age distribution is right-skewed, with a notable concentration of employees below 45 years. Outliers in the age feature were identified and subsequently removed during data preprocessing.

##### iv. Other Numerical Features
The remaining numerical features demonstrate either right or left skewness, warranting further investigation for extreme values during preprocessing.

Categorical features were analyzed using bar plots to discern relationships with the target variable.

### Multivariate Graphical Exploratory Data Analysis
To assess correlations between independent and dependent features, as well as covariance among independent features, a correlation matrix was employed.

![image](https://github.com/Mattdozie/Predicting-Employee-Absenteeism-using-Linear-Regression-Models-in-R-/assets/100968289/743c7bea-4882-4b3f-8739-1bcb55d47249)


#### Correlation Chart: Relationships and Coefficient of Variables
The correlation chart revealed a high correlation (0.90) between weight and body mass index (BMI), indicating multicollinearity. Multicollinearity, is detrimental to model accuracy and reliability, necessitating remediation. Consequently, the variable weight, exhibiting high correlation, was eliminated from the dataset. Other variables did not display strong positive or negative correlations.

Multicollinearity, defined as the presence of highly correlated independent variables, it poses challenges to machine learning models' accuracy and reliability. To address this issue, variables with high correlation coefficients were removed from the dataset. 

## Data Pre-processing
After examining the distribution of variables in the dataset, it was evident that most variables were not normally distributed, displaying either left or right skewness and, in some cases, multi-modal distributions. Skewness is often attributed to the presence of outliers, which are observations with unusually high or low values.

### Outlier Analysis
Boxplots were utilized to confirm the presence of outliers in various variables. Outliers, being abnormal values, can significantly impact regression models. Before deciding on their treatment, it was imperative to ascertain whether outliers provided meaningful insights into the data.

![image](https://github.com/Mattdozie/Predicting-Employee-Absenteeism-using-Linear-Regression-Models-in-R-/assets/100968289/49123424-55d5-4601-bd31-69c8c45e19ed)
![image](https://github.com/Mattdozie/Predicting-Employee-Absenteeism-using-Linear-Regression-Models-in-R-/assets/100968289/f64a0b7d-211d-4e2b-bc41-6392a78c843b)
![image](https://github.com/Mattdozie/Predicting-Employee-Absenteeism-using-Linear-Regression-Models-in-R-/assets/100968289/d94b763d-41f0-47d8-b4a8-098522ebb25e)
![image](https://github.com/Mattdozie/Predicting-Employee-Absenteeism-using-Linear-Regression-Models-in-R-/assets/100968289/48ef977d-6b10-43c3-b35f-ab234af413dd)
![image](https://github.com/Mattdozie/Predicting-Employee-Absenteeism-using-Linear-Regression-Models-in-R-/assets/100968289/93b1cbdb-139b-4f8a-9949-cadc2dd7d5ad)


<div style="display:flex;">
    <img src="https://github.com/Mattdozie/Predicting-Employee-Absenteeism-using-Linear-Regression-Models-in-R-/assets/100968289/49123424-55d5-4601-bd31-69c8c45e19ed" alt="Image 1" width="200" height="150" style="margin-right: 10px;"/>
    <img src="https://github.com/Mattdozie/Predicting-Employee-Absenteeism-using-Linear-Regression-Models-in-R-/assets/100968289/f64a0b7d-211d-4e2b-bc41-6392a78c843b" alt="Image 2" width="200" height="150" style="margin-right: 10px;"/>
    <img src="https://github.com/Mattdozie/Predicting-Employee-Absenteeism-using-Linear-Regression-Models-in-R-/assets/100968289/d94b763d-41f0-47d8-b4a8-098522ebb25e" alt="Image 3" width="200" height="150" style="margin-right: 10px;"/>
    <img src="https://github.com/Mattdozie/Predicting-Employee-Absenteeism-using-Linear-Regression-Models-in-R-/assets/100968289/48ef977d-6b10-43c3-b35f-ab234af413dd" alt="Image 4" width="200" height="150" style="margin-right: 10px;"/>
    <img src="https://github.com/Mattdozie/Predicting-Employee-Absenteeism-using-Linear-Regression-Models-in-R-/assets/100968289/93b1cbdb-139b-4f8a-9949-cadc2dd7d5ad" alt="Image 5" width="200" height="150" style="margin-right: 10px;"/>
</div>



Outliers were identified in the following features:

- Transportation expense
- Service time
- Age
- Workload
- HIT
- Height

### Feature Scaling
Given the disparate measurement units and magnitudes of features, scaling them down to a fixed range becomes crucial. This normalization facilitates the proper functioning of machine learning algorithms, particularly in optimization tasks like gradient descent convergence.

### Feature Selection
Machine learning models often grapple with a multitude of input features, posing challenges for accurate predictions. Feature selection methods help identify relevant attributes while eliminating redundant or highly correlated data, thereby enhancing model interpretability, reducing computational requirements, and improving generalization.

Least Absolute Shrinkage and Selection Operator (LASSO), Ridge, and Elastic Net regressions, known for their inherent feature selection capabilities, were chosen for this project.

## Model Justification
The aim is to adopt a parsimonious model that accurately predicts future data, hence the selection of
