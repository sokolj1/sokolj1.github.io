---
header:
  image: /assets/predicting-heart-disease/heart_disease_screenshot_8_2_2018.png
  
tags: 
  - python
  - tableau
  - pca
  - logistic regression
  - healthcare
author_profile: false
toc: true 

excerpt: Machine learning application in the healthcare industry

---

This study serves as an viable example of data science, specifically machine learning, in the healthcare industry. Using United States heart disease data from the UCI machine learning repository, a Python logistic regression model of 14 features, 375 observations and 78% predictive accuracy, is trained and optimized to assist healthcare professionals predicting the likelihood of confirmed patient heart disease presence. Selection of the fourteen training features was based upon data cleanliness and clinical validity of the feature's contribution to presence of heart disease. 

Principle Component Analysis served as an exploratory data analysis technique. The dimensionality of the UCI machine learning repository heart disease dataset was reduced from the ten continuous features to two principle components for 2D visualization. The PCA dimensionality reduction retained only 39% of the dataset variance, suggesting the ten features contributed to heart disease prediction fairly equally. To choose the best machine learning technique to train the data, the innovative automated machine learning package Tree Based Optimization Tool (TPOT) determined logistic regression as the optimal technique/classifier with the most predictive power. A logistic regression model was fitted with 78% error out accuracy. 

The logistic regression model was instantiated in a Python function, then deployed to a Tableau Dashboard with Tableau extension TabPy to build a plausible graphical user interface; the healthcare professional can modify model parameters for each patient to obtain a risk assessment based on the aforementioned health metrics. This predictive analytics application serves as proof of viability for implementation in the healthcare industry. In regards to long term implications, this study enables healthcare professionals to consider putting into practice machine learning predictive analytics for future state patient risk assessment. 

## Introduction

Heart disease is described as any condition that detrimentally affects the heart. Heart disease is often used interchangeably with the term "cardiovascular disease." However, cardiovascular disease generally refers to conditions involving heart blockages such as atherosclerosis (narrowing or blocking of the arteries due to plaque buildup), whereas heart disease is an umbrella term that is inclusive of other heart conditions. Heart Disease can not only affect the arteries, but the heart muscle, valves, rhythm, or other important aspects of a well-functioning heart. 

The pervasiveness of heart disease in the United States has merited the ailment as the leading cause of death in the United States.
Here are a few statistics that emphasize how problematic heart disease has become in our society [[1](https://www.cdc.gov/heartdisease/facts.htm)]: 
- About 610,000 people die of heart disease in the United States every year. That is 1 in every 4 deaths.
- Heart disease is the leading cause of death for both men and women. More than half of the deaths due to heart disease in 2009 were in men.
- Coronary heart disease (CHD) is the most common type of heart disease, killing over 370,000 people annually.
- Every year about 735,000 Americans have a heart attack. Of these, 525,000 are a first heart attack and 210,000 happen in people who have already had a heart attack.

To illustrate the prevalence of heart disease, choropleth mapping shows comparative heart disease trends categorized by state, heart disease stratification, and gender using [Tableau Public](https://public.tableau.com/en-us/s/). The CDC's Division of Population Health provides yearly statistics of over 124 chronic health disease indicators that are reported on a city and state level, available to download [here](https://chronicdata.cdc.gov/Chronic-Disease-Indicators/U-S-Chronic-Disease-Indicators-CDI-/g4ie-h725). This dataset was cleaned and filtered using Pandas, then imported into Tableau Public. I provide the [iPython Notebook](https://github.com/sokolj1/Predicting-Heart-Disease/blob/master/Heart_Disease_Data_Cleaning_and_Tableau_Viz.ipynb) for those who want to know the intricacies of the data preparation process. The other iPython notebooks and cleaned datasets can also be found in that Github repository. The Tableau workbook can be downloaded by clicking on the bottom right download icon of the frame.

<iframe src = "https://public.tableau.com/views/PrevalenceofHeartDiseaseintheUnitedStates20145_0/Dashboard1?:showVizHome=no&:embed=true" width="95%" height="600"></iframe>


## Predictive Analytics Case Study: Heart Disease

Heart disease is a major issue across every state and gender in the United States. Treatment for heart disease cost the healthcare industry over 444 _billion_ dollars in 2010 [[2](https://www.webmd.com/healthy-aging/features/heart-disease-medical-costs#1)]. An assumption can be made that present day cost is substantially higher than the 2010 dollar amount. Although it is imperative that the healthcare industry provides high quality treatment for patients diagnosed with health disease, this industry must ameliorate the issue by reducing the number of future patients diagnosed with heart disease via *preventative care*.

Traditional preventative care uses propylatic measures to prevent people from developing various diseases. The key advantage from a healthcare perspective is lower cost to employ preventative care compared to disease treatments. This is especially applicable to heart disease. Heart disease preventative care begins with determining the likelihood of developing heart disease based upon a variety of patient attributes. The different attributes are assigned weights; the greater the weight, the more impactful the attribute is on disease prediction. The healthcare professional draws from years of formal education and medical training to interpret these attributes to holistically determine the best course of action for the patient: 

 - Small likelihood of heart disease presence: No prophylaxis measures necessary 
 - Plausible likelihood of heart disease presence: Prophylaxis recommended 
 - Very likely heart disease is present: Run additional tests to confirm severity of heart disease
 
Although healthcare professionals invoke incredible decision making abilities upon rendering a diagnosis, data science can help healthcare professionals with patient diagnosis for heart disease. The healthcare industry collects a substantial amount of data for each patient with appointments, office/lab tests, and medical history. With mainstream adoption of artificial intelligence and machine learning, the same attributes that healthcare professionals use to diagnose a patient with likelihood of heart disease can be leveraged to create machine learning models that help nurses, physician assistants, and medical doctors better understand their patient's health to make better decisions. By implementing a heart disease prediction system with machine learning, this system will "learn" from labeled data to probabilistically predict the likelihood of a patient having heart disease. 

Once the machine learning model is fitted, it can be deployed to Tableau using TabPy. This API encapsulates the model in a graphical user interface. The end user can modify patient data in Tableau parameter fields. The parameters serve as arguments for the backend machine learning Python functions. After user input, the model returns a binary prediction (no presence or presence of heart disease) in addition to the probability of the latter being true. 

## Data Source: University of California Irvine (UCI) Machine Learning Repository

The data was obtained from the UCI Machine Learning Repository. Considering the focus on heart disease in the United States, only the Cleveland and Long Beach files were used. After rigorous data cleaning, both files were imported into a Pandas DataFrame: 

<img src="/assets/predicting-heart-disease/master_df.png" >

The master DataFrame has 375 observations and 63 features.

In order to complete PCA and fit machine learning models, it is important to store our target labels in a separate DataFrame. The target labels are the diagnosis of heart disease. The doctors who collected the data determined the presence of heart disease in each patient on an integer value classification scale from 0 to 4: 0 indicates no presence of heart disease, and 4 indicates significant, concerning presence. For this study, we only care about binary classification of heart disease: 0 for no presence, and 1 for presence. 

## Selecting the Features for Analysis

Feature selection is one of the most important aspects of machine learning. These features will serve as the foundation of the model; the chosen features should be backed by considerable research. For our example, the data scientist should consult healthcare professionals such as cardiologists and ECG/EKG technicians to determine the features that reliably diagnosis heart disease. 

Although in this case, by using an aggregated dataset from a repository, only the data present is useable. The main factors that influenced my decision for selection of each feature was the following: 
- Presence of clean data, as the dataset is extremely dirty. For instance, a few features that were viable in the Cleveland dataset had missing/invalid values in the Long Beach dataset. 
- Using heart disease risk factor knowledge derived from my undergraduate studies and working as a Pharmacy Technician. I know classic indicators such as blood pressure, cholesterol, and family history are important features to include for the model from listening to pharmacist consultations. Lifestyle choices also have a major influence on heart health, so I choose several exercise and smoking metrics to include in the study. 
- Features should have no presence or minimal degree of multicollinearity. Considering logistic regression is a generalized linear model (GLM), multicollinearity may result in inconsistent parameter estimates. Fitting the training data can yield vastly different optimized parameters (weights) each time the model is fitted. This can lead to huge variations in the out of sample error, making the model's predictive power too inconsistent for viability. 
- Features should not be redundant. The dataset has many instances of continuous and discrete measures for features that are the same i.e cigarettes per day (0 - 100 cigarettes) and smoker? (1 or 0), resting blood pressure (90 to 200 mm Hg) and hypertension (1 or 0). For these examples, I kept the continous features and left out the redundant binary features. 
Ultimately, I narrowed down the selection to 14 features: 10 continuous and 4 binary. 

|   |Feature                          | Type              |     
|---|                       ---       |     ---           |
| 1 | Age                             | continuous        |
| 2 | Resting blood pressure          | continuous        |
| 3 | Cholesterol                     | continuous        |
| 4 | Cigarettes per day              | continuous        |
| 5 | Years as smoker                 | continuous        |
| 6 | Resting heart rate              | continuous        |
| 7 | Maximum heart rate achieved     | continuous        |
| 8 | Metabolic Equivalent of Task (METs)  | continuous   |
| 9 | Peak Exercise blood pressure (tpeakbps)| continuous |
| 10| Exercise Stress Test (rldv5e)     | continuous   |
| 11| Fasting blood sugar               | binary       |
| 12| History of heart disease          | binary       |
| 13| Exercise Induced Angina           | binary       |
| 14| Sex                               | binary       |

Now we're ready to dive into principle component analysis to become more familiar with our data.

## Principle Component Analysis (PCA)

Principle component analysis, or colloquially known as dimensionality reduction, is a statistical procedure that uses eigenvalue decomposition to generalize the most important features in a dataset. PCA simplifies the complexity of high dimensional (many features) data while retaining trends and patterns. For example, the popular beginner machine learning [MNIST Database](http://yann.lecun.com/exdb/mnist/) of handwritten digits has 60,000 observations (rows) and 785 features (columns). [A Kaggler](https://www.kaggle.com/ddmngml/pca-and-svm-on-mnist-dataset) completed PCA on this dataset. He effectively reduced the MNIST dimensions from 785 to 16, and retained 59% of the variance, or information that the original dataset conveyed. In a separate trial, he also reduced the dataset from 785 to 49, and retained 82% of the variance. By simplifying the dataset into principle components, we can observe features that contribute more information to the dataset than others, speed up process time if the dimensionality reduced is significant, and visualize trends and patterns of datasets that have many features. 

PCA is not ideal for non-continuous, discrete dataset attributes. The 10 continuous values out of the total 14 are the only attributes that can be used for PCA analysis. In order to obtain the most accurate PCA analysis results, the data needs to be scaled. If scaling is overlooked, then features that have higher quantitative values will influence the results far more than the other features. There are several ways to scale data, but the most common is to subtract each observation by the overall feature mean, then divide the difference by the feature standard deviation. 

<img src="/assets/predicting-heart-disease/heart_dis_pca_results.png" >

<img src="/assets/predicting-heart-disease/explained_var.png" >

<img src="/assets/predicting-heart-disease/explained_var_sum.png" >

The continous attributes are also visualized using a Pearson correlation matrix. The correlation values range from -1 to 1, with -1 indicating a negative correlation, 0 indicating no correlation, and 1 indicating a positive correlation. 

<img src="/assets/predicting-heart-disease/hd_pearson_correlation.png" >

Notable positive correlations amongst the data are cigarettes per day as years as a smoker increases, and an increase in METs as maximum heart rate achieved increases. 

Since all our data is standardized, we can divide our data into a 'train' dataset and a 'test' dataset. To evaluate the efficacy of the fitted, or trained model, we must use data that did NOT train the logistic regression model. The unfitted data is called 'unseen.' The rule of thumb is to divide the master DataFrame into separate 70-75% train and 20-25% test DataFrames. There are manual ways to Pythonically complete this task, but using the popular machine learning library sci-kit learn, the function train_test_split completes the heavy lifting.

We also need to reshape the diagnosis (label) dataset. The _to_categorical_ function converts a class vector to a binary class matrix. For example, instead of the y_train and y_test datasets consisting of n rows and 1 column of 1's and 0's depending on the diagnosis, _to_categorical_ reshapes these DataFrames to n rows and 2 columns, one for each class: 

## Logistic Regression

Logistic regression is a method for estimating categorical relationships amongst input variables based upon a trained probabilistic model. For this study, binomial logistic regression is employed to return the probability, or likelihood of heart disease classification. 

K-folds cross validation increases model error out accuracy. The model uses _all_ observations for model training. The observations are randomly divided into train and test datasets, the model is fitted, then the model is randomly divided again, fitted, and so on, K times with resampling. So all observations are used as training data to fit the model. To determine final accuracy output, all of the model accuracies are averaged for a cumulative accuracy score. This model uses 10 fold cross validation. For the sake of brevity, please reference the logistic regression model fitting code in the Jupyter Notebook. 

<img src="/assets/predicting-heart-disease/logistic_reg_fitting.png" >

It turns out that using logistic regression results in an error out of 78%. This will be our deployable TabPy function. 
Model accuracy above 70% accuracy is considered to be a decent classifier. For this particular study where the model is trained with a limited amount of observations, there is a case that 78% accuracy is excellent. I recently coded logistic regression from stratch in R. Knowing logistic regression is a binary classifier and considering the purpose of this post is an introduction to machine learning, I built a logistic regression model with the same features from the heart disease dataset.

```python
# logistic regression cross validation: probability, 0 - 100%
def suggest_diag_prob(age, sex, resting_blood_pressure, cholesterol, cigarettes_per_day, 
years_as_smoker, fasting_blood_sugar, hist_heart_dis, resting_hr, max_hr_ach, mets, tpeakbps, exer_ind_angina, rldv5e):
    
    features = np.column_stack([age, sex, resting_blood_pressure, cholesterol, cigarettes_per_day, 
    years_as_smoker, fasting_blood_sugar, hist_heart_dis, resting_hr, max_hr_ach, mets, tpeakbps, exer_ind_angina, rldv5e])
    
    features_scaled = scaler.transform(features)
    predict_proba = lgclf.predict_proba(features_scaled)[0,1].tolist()
    
    return(predict_proba)
suggest_diag_prob(18, 0, 120, 150, 0, 0, 0,0, 65, 200, 15, 140, 0, 93)
```

## Connect to TabPy

Tableau is a business intelligence company that produces powerful software for interactive data visualizations. TabPy is a Tableau extension that can import python code into Tableau dashboards, bridging the gap between business intelligence and data science. This extension will be used to deploy the fitted logistic regression function into the Tableau dashboard so the end user can modify the patient health parameters, so a likelihood metric can be returned.

Connecting Tableau to TabPy is relatively pain free after [installation](https://github.com/tableau/TabPy). Afterwards, run startup.sh (located in the TabPy-server folder) in the terminal to initiate the TabPy instance listening on localhost port 9004. Also ensure TabPy is [properly configured](https://www.tableau.com/about/blog/2016/11/leverage-power-python-tableau-tabpy-62077) in Tableau Desktop under Help > Settings and Performance > Manage External Connection.

Once both tasks are complete, deploy the logistic regression function to Tableau.

```python
# Connect to TabPy server using the client library
connection = tabpy_client.Client('http://localhost:9004')

# Publish the suggest_diag_prob function to TabPy server so it can be used from Tableau
connection.deploy('heart_disease_logregcv_prob',
                  suggest_diag_prob, override = True)
```

TabPy should now be communicating with the Python script. Unfortunately, Tableau dashbords connected to exernal services such as TabPy can _not_ be posted to Tableau Public. Nonetheless, I have a 30 second on-screen video to showcase the dashboard: 

<iframe id="ytplayer" type="text/html" width="640" height="360"
  src="https://www.youtube.com/embed/yW1hmb3GL30"
  frameborder="0" allowfullscreen></iframe>
  
 
The following is an assessment of Tableau Dashboards with respect to predictive analytics in the healthcare industry.

### Negatives 
TabPy is painfully slow with transmitting the updated parameters across the local server to call the logistic regression python function, and then returning the probability of the patient being at risk. In the fast paced healthcare setting, healthcare professionals demand an unimpeded workflow to prioritize patient care. Inputting all fourteen patient health attributes into the dashboard takes approximately one minute. This metric should be closer to 20 - 30 seconds at most. TabPy is still being in beta, so performance concerns may be assuaged in future iterations. Furthermore, the Tableau software is expensive. With commercial licenses upwards of $1,999 per li- cense, small healthcare organizations such as doctors offices may not have the financial means to prioritize Tableau in their budget.

### Positives 
The positive aspects of the dashboard are groundbreaking from a predictive analytics perspective. Performance issues aside, this application has the potential to become a huge contribution to healthcare professional’s decision regarding patient health. Machine learning is a powerful data science technology that can be utilized in the healthcare industry, but there must be a graphical user interface for the end user to interact and manipulate the function inputs, which would be the patient data.

## Future Work
Although this case study has shed light on how machine learning can greatly benefit the healthcare industry, there is room for study improvement. More data/patient observations should be obtained to fit a possibly more generalized and accurate model. Although this post focuses on employing logistic regression, there are other models that may yield even better results. 

### Choosing the right machine learning algorithm

When deciding which machine learning algorithm to use, there is a wide variety to choose from, but a "magic bullet" doesn't exist. There is no one machine learning algorithm best for all problems, but familiarity and understanding the pros and cons of each algorithm can guide the data scientist to the best decision for the problem at hand. 

1. **Understand the problem**
It is important to know what type of problem we are dealing with and what kind of algorithm works best for each type of problem. Once the problem and end goal is identified, the data scientist can break down algorithm selection by three categories: 
* Supervised learning
* Unsupervised learning
* Reinforcement learning

2. **Size of dataset (training and test)**
Some machine learning algorithms work optimally with small or large datasets. For example, 
Small datasets demand algorithms that have high bias to avoid overfitting.

3. **Exploratory data analysis**
* Compute summary statistics and visualizations (boxplots, density plots, etc) of your dataset. 
* Percentiles help identify the range for most or all of the data.
* Measure correlation and central tendency of the data.

4. **Required accuracy: bias-variance tradeoff**
* Bias: error from assumptions in the learning algorithm. Models with low bias are usually more complex with more accurate fitting to the train dataset, but inadvertently creates large amounts of noise, making predictions less accurate. Models with high bias tend to be simple, but may not generalize well to unseen data. 
* Variance: error from sensitivity to small fluctuations in the training dataset. High variance models represent the training dataset well, however, they may not generalize well to unseen data due to overfitting. Low variance produces simpler models that are not prone to overfitting but may fail to capture important irregularities present in the training dataset. 

5. **Timeframe**
Machine learning models can take hours or even more than a day to train, depending on the size, target accuracy, and algorithm of choice.

6. **Linear assumptions**
Common machine learning models such as linear regression , logistic regression and support vector machines are linear models, as linear models are algorithmically simple, fast to train, and relatively easy to interpret. But beware of data that does not conform to linear assumptions, as this can decrease model accuracy.

7. **Features**
A large number of features can provide accurate model predictions in conjunction with a large number of observations. But too many features may result in unfeasibly long training times for some algorithms.

Despite knowing this all of this information, even the most experienced data scientists can't tell which algorithm will perform best without trying them. Devoting time to go through the workflow above with each viable machine learning algorithm would greatly improve the credibility of the study.

Here is a model selection reference provided by the sci-kit learn library:

<img src="/assets/predicting-heart-disease/sci_kit_learn_cheat_sheet.png" >

## Changing the Healthcare Landscape
In summary, machine learning has proven to be a viable data science assistant for healthcare professionals. The logistic regression model was instantiated in a Python function, then deployed to a Tableau Dashboard with Tableau extension TabPy to build a plausible graphical user interface; the healthcare professional can modify model parameters for each patient to obtain a risk assessment based on the aforementioned measured health metrics. This predictive analytics application serves as proof of viability for implementation in the healthcare industry. As far as long term implications, this study enables healthcare professionals to consider putting into practice machine learning predictive analytics for future state aid in risk assessment.


