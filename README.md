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

The aim is to adopt a parsimonious model that accurately predicts future data, hence the selection of models like LASSO, Ridge, and Elastic Net. These models mitigate multicollinearity issues and enhance interpretability, consequently improving the robustness of the analysis.

## Model Building

### Multiple Linear Regression Model
Multiple Linear Regression allows the utilization of multiple independent features and assumes a linear relationship between them. The model was trained using the "lm" method in R, with 344 samples and 14 predictors. Cross-validation was performed using 10-fold resampling repeated 5 times. The evaluation highlighted the significance of the "Disciplinary Failure" feature.

![image](https://github.com/Mattdozie/Predicting-Employee-Absenteeism-using-Linear-Regression-Models-in-R-/assets/100968289/3a5e3767-9f11-4a25-add5-acd52f52ed81)

### Ridge Regression Model
Ridge regression, employing L2 regularization, shrinks variable coefficients to prevent overfitting. The "glmnet" package in R was utilized for model development, with alpha set to zero and lambda chosen via cross-validation. The model selection was based on Root Mean Square Error (RMSE).

![image](https://github.com/Mattdozie/Predicting-Employee-Absenteeism-using-Linear-Regression-Models-in-R-/assets/100968289/971e1059-34e9-433c-8c3a-3f5029070b17)

### Lasso Regression Model
Lasso regression, employing L1 regularization, reduces coefficients and eliminates variables with zero coefficients. The "glmnet" package was employed in R, with alpha set to 1 and lambda selected via cross-validation. RMSE guided model selection.

![image](https://github.com/Mattdozie/Predicting-Employee-Absenteeism-using-Linear-Regression-Models-in-R-/assets/100968289/c001ac2b-fb4a-4fc3-8ebd-bd5e7e5b0047)

### Elastic Net Regression Model
Elastic Net regression combines L1 and L2 penalties, offering a balanced approach. The model, trained using the "glmnet" package in R, underwent cross-validation to select optimal alpha and lambda values. RMSE guided the final model selection.

These regression models were developed after comprehensive data preprocessing, ensuring robustness and accuracy in subsequent analyses.

## Model Evaluation and Project Assessment

### Model Selection
Model evaluation metrics, including Mean Absolute Error (MAE), Root Mean Square Error (RMSE), and R-Squared, were utilized for model comparison. The Elastic Net model exhibited superior performance in terms of MAE and RMSE on the training dataset, despite a lower R-Squared value compared to other models. Visual representation via boxplots corroborated this finding, showcasing the Elastic Net model's overall effectiveness.

![image](https://github.com/Mattdozie/Predicting-Employee-Absenteeism-using-Linear-Regression-Models-in-R-/assets/100968289/61c84eb1-bfcf-4f3c-a2c0-054b26e35b62)

### Box & Whisker Plot of R-Squared, MAE, and RMSE
The best tuning parameters for the Elastic Net model indicated its similarity to a Ridge model. Variable importance analysis highlighted the significance of "Disciplinary Failure" and "Transportation Expense" in predicting the target variable.

![image](https://github.com/Mattdozie/Predicting-Employee-Absenteeism-using-Linear-Regression-Models-in-R-/assets/100968289/96712ef2-38aa-4a8e-bcd5-be7ec4052ed6)

### Model Prediction and Accuracy Estimation
The final selected model was subjected to both in-sample (training data) and out-of-sample (test data) predictions. The Root Mean Square Error (RMSE) served as the primary metric for assessing model accuracy. Lower RMSE values for both predictions indicated satisfactory performance, with the model demonstrating improved accuracy on the test data.

### Project Evaluation
The success of the project was evaluated against predefined goals, Key Performance Indicators (KPIs), and the ability to deliver actionable insights. The project encompassed comprehensive phases including data collection, processing, analysis, model evaluation, and reporting, all meeting the set objectives. Exploratory data analysis uncovered valuable insights, such as non-linear relationships between variables and the presence of outliers. Multivariate analysis revealed multicollinearity issues, addressed through feature selection techniques. The final model selection, based on rigorous evaluation, recommended actionable strategies for reducing absenteeism, emphasizing the importance of disciplinary measures and transportation incentives.

Find the full Report [HERE](https://github.com/Mattdozie/Predicting-Employee-Absenteeism-using-Linear-Regression-Models-in-R-/blob/main/Absenteeism%20Report.pdf)
