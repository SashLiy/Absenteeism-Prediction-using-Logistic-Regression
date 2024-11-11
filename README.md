# Absenteeism-Prediction-using-Logistic-Regression
Python+SQL+Tableau

The Absenteeism Prediction project focuses on predicting absenteeism in the workplace using an employee dataset. The goal is to preprocess and analyze the absenteeism data to gain insights and create a model for predicting future absenteeism based on various employee features.

1. Data collection
Dataset: Absenteesim_new_data.csv

2. Data preprocessing
The original Absenteeism dataset includes the following columns:
ID
Reason for Absence
Date
Transportation Expense
Distance to Work
Age
Daily Work Load Average
Body Mass Index (BMI)
Education
Children
Pets
Absenteeism Time in Hours

The dataset undergoes several preprocessing steps:

ID Column Removal: The ID column is removed as it is not essential for analysis.

Reason for Absence Grouping: The reasons for absenteeism, initially provided as 28 unique categories, are grouped into four categories based on logical classifications:

Group 1: Reasons 1 to 14
Group 2: Reasons 15 to 17
Group 3: Reasons 18 to 21
Group 4: Reasons 22 and 28
Adding Group Columns: These reason groups are then added as new columns to the dataset and reordered to appear as the first four columns.

Checkpoint: A temporary save of the work is created to ensure that the current progress is preserved, reducing the risk of data loss.

Date Formatting: The Date column, initially stored as a string, is converted into a more usable format (Year, Month, Day). The month value is extracted for further analysis.

Education Column Encoding: The Education column is transformed into binary values to indicate whether an employee has higher education (graduate, postgraduate, or doctorate). The encoding is as follows:

1 (High School) → 0
2 (Graduate) → 1
3 (Postgraduate) → 1
4 (Master/Doctorate) → 1




3. Modeling:
After preprocessing, the dataset is ready for modeling. A Logistic Regression model is applied to predict absenteeism based on the processed features. Logistic regression is chosen as it is ideal for binary classification problems, and the data includes both categorical and continuous features.

4. Data Storage and Serialization:
The preprocessed dataset is stored in a new file, Absenteeism_preprocessed.csv. Additionally, to preserve the trained model and preprocessing parameters, the scaler (used for feature scaling) and the trained model are saved using Pickle:

import pickle
with open('scaler', 'wb') as file:
    pickle.dump(absenteeism_scaler, file)



5. Model Integration and Prediction:
To use the model for predictions, the absenteeism_module.py is imported, which contains the necessary functions for loading and cleaning the data, and applying the model. The following steps are performed:

Data Loading and Cleaning: The model loads and preprocesses the new dataset.
Prediction: The trained model is used to make predictions on absenteeism based on the new data.

from absenteeism_module import *
model = absenteeism_model('model', 'scaler')
model.load_and_clean_data('Absenteeism_new_data.csv')
model.predicted_outputs()


6. Database Integration:
To store the predicted results, a connection is established to a MySQL database. The predictions are inserted into the predicted_outputs table. The insertion query is generated dynamically to handle each prediction:
import pymysql
conn = pymysql.connect(database='predicted_outputs', user='nativeuser', password='365Pass')
insert_query = 'INSERT INTO predicted_outputs VALUES '
for i in range(df_new_obs.shape[0]):
    insert_query += '(' 
    for j in range(df_new_obs.shape[1]):
        insert_query += str(df_new_obs[df_new_obs.columns.values[j]][i]) + ', '
    insert_query = insert_query[:-2] + '), '


7. Tableau Integration for Visualization:
After predictions are made and stored in the database, Tableau creates interactive and insightful visualizations. By connecting Tableau to the MySQL database where the predicted outputs are stored, users can:

Visualize trends in absenteeism over time.
Analyze absenteeism by department, age, or education level.
Compare absenteeism reasons across different groups.
Examine the predicted absenteeism values to identify potential absenteeism patterns.
Tableau provides an intuitive and powerful platform for creating interactive dashboards. This allows stakeholders to gain deeper insights from the data and make informed decisions.

Coefficient and Odds Ratio Interpretation: A feature's coefficient close to 0 or an odds ratio close to 1 suggests that the feature has little influence on the prediction.
Reason_0: This represents a situation where no specific reason for absence is provided.
The project leverages Logistic Regression for classification, preprocessing techniques for cleaning and transforming data, and Pickle for saving the model and scaler, ensuring that predictions are accurate and data storage is efficient. By integrating Tableau, the project provides a user-friendly visualization layer, allowing businesses to analyze and predict absenteeism in the workplace effectively.


