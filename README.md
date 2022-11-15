# Disease Prediction

The basis of this project is to use one or more machine learning models that can make accurate predictions of a disease by taking in arguments for symptoms (X) and predict the causative illness (y). This trained model will then be deployed to a webpage to accept user inputs and make real-time predictions. 

## Why Disease Prediction?
As a group, we wanted to work on something that we thought could have an impact on people. There are many people around the world suffering from various diseases. While this project will only function as a test, it is a good indication of what machine learning is capable of, and how it may be used in the future of healthcare.

[Link to Google Slides Presentation](https://docs.google.com/presentation/d/17sEjf6EPZSJ9EY5Vl9RA3tWl3OAGQc6XCYFe-FfR_w0/edit?usp=sharing)

## Dataset

The dataset contains four CSV files.

* [Disease Dataset](./Data/Cleaned/dataset_clean.csv) consists of 41 diseases and 131 possible symptoms. Each disease has 120 cases or incidences.

* [Disease Description](./Data/Cleaned/disease_description_clean.csv) is a list of the diseases with a brief description of each illness.

* [Symptom Severity](./Data/Cleaned/symptom_severity_clean.csv) is a list of all symptoms with a weight to indicate severity.

* [Disease Precaution](./Data/Cleaned/disease_precaution_clean.csv) is a list of precautions to take for each disease.

## Data Cleaning & Processing

Many replacements were made to the dataset for the sake of clarity and consistency. The main dataset of disease symptoms per case was then transformed to contain columns for every possible symptom, each containing boolean values.

<!-- Pictures of the DataFrame before and after boolean transformation -->

### Before
![data_df](./Images/data_df.png)

### After
![bool_df](./Images/bool_df.png)

This format is much easier for any machine learning model to interpret, as it is already encoded and scaled.

## Machine Learning Model

Decision Tree Classifier was used as a benchmark classification model. Support Vector Classifier was investigated for superior performance. Support vector machines (SVM) work well on small datasets with clear separation between boundaries and don't perform as well on datasets with much noise.

The dataset was filled with many duplicates; removing these duplicates would drop the sample size for each disease from 120 to 5-10. Retaining these duplicates proved to make the models more robust against overfitting. The small effective size of the unduplicated dataset was mitigated by using a SVM classifier and using a 50/50 split between training and test data. sklearn's train_test_split() was used to create the training and testing datasets.

Decision Tree Classifier was trained with a max depth of 10 to prevent overfitting. Similarly, many values for the SVM 'gamma' and 'C' parameters were tried, until a model with a reasonable accuracy score and confusion matrix were returned. An [online introduction](https://vitalflux.com/svm-rbf-kernel-parameters-code-sample/) to these parameters was used to guide the selection of their values. The RBF kernel was used for the SVM due to its suitability for nonlinear data that is not well-known or characterized.

The decision tree benchmark performed decently at nearly 95% accuracy, yet the confusion matrix reveals a practical issue with the model: heart attacks are often falsely predicted as many other illnesses that don't require prompt medical attention.

The support vector machine performs at a better 98% accuracy and has a less worrying confusion matrix. Variations of hepatitis are sometimes confused with each other or another liver illness, chronic cholestasis. Acne is sometimes misdiagnosed as a drug reaction, which should be straightforward for the end user to distinguish. This model appears to perform well in the context of accurately and reasonably diagnosing illness based on reported symptoms.

## Database

SQL will be used to create a relational database with multiple tables for Disease Description, Disease Precautions, and the main dataset.

* The first step in setting up the SQL database with our dataset is to create tables to import the data that we have. 
* The four tables initially created are:
  - "Disease_Cases" (to show the symptoms found in each case of the diseases in our dataset) 
  - "Disease_Descriptions" (to provide a brief description of the unique diseases in the dataset) 
  - "Disease_Precautions" (to provide possible precautions one can take if potentially facing one of the diseases)
  - "Symptom_Severity" (so that the symptoms of a disease can be weighed and more easily measured).
* With our data imported, we use the "Disease_Descriptions" and "Disease_Precautions" tables to create a new joined table called "Disease_Info" with all information on the diseases. 
* Now that we have some new tables, we can create new clean CSV files for them, and upload these to our repository Data section.

## Dashboard
The trained ML model can be deployed to a webpage. Using Flask/JavaScript, we can build a simple webpage that will allow the user to input symptoms they are experiencing and view the model's prediction of their illness. Recommendations for treatment/precautions can be displayed, based on [symptom_precaution.csv](./Data/symptom_precaution.csv) 

## Team Communication Protocol
The team meets twice per week via Zoom and uses Slack to communicate as needed. There is a Group Plan file to help document our upcoming goals and overall plan for the project.
