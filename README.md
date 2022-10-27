# Predictive Undewriting Decision Model

## Introduction

**Background & context**

   The conventional way of purchasing a life policy involves many steps starting from deciding on how much and what type of coverage is needed. The potential applicant will then select a suitable product for his needs. Next, the applicant would be required to fill out the application form as well as to schedule for a life insurance medical examination where necessary. Typically, the application form will consist of questions related to the applicants profile (Age, weight, height, occupation),current and past health conditions, family medical history and existing insurance cover. Upon receipt of the applicant's application, the application will be underwritten. During which the underwriter will consult an actuarial table. This resource enables the underwriter to see the mortality probability of the applicant. The higher that probability, the higher your premium will likely be. Following which, taking everything into consideration, the underwriter will issue the applicant an insurance classification rating such as a "Preferred, Standard Plus, Standard, Substandard". Generally, these classification exists for both smokers and nonsmokers having serperate rates.

   Increased data availability, and the improved efficacy of machine learning techniques in handling complex data and processing natural languages, mean we are on the horizon of being able to drastically simplify the underwriting journey, with limited or no impact on the risk profile. Combining a simple questionnaire with external data sources should enable insurers to accurately assess risk and make instant decisions in almost all applications.
    
**What is this project about?**

   The aim of the project is to provide a demonstration of how ML techniques can be used to predict underwriting decision for life insurance applicants, which could then in turn support underwriters in their decision-making process on how prospective new business should be valued. This model may then be implemented into the business process be it through providing an early glimpse of the likely underwriting result or implemented as part of the decision classifier model of a Straight Through Processing ("STP") chain.
    
   As a case study, we will use the dataset featured in the Prudential Life Insurance Assessment competition previously hosted on Kaggle, and showcase how ML classifiers can be used to quantitatively assess risk and ultimately provide us with an underwriting decision.
##Problem Statement

At present, Underwriters in the Life Insurance industry review all Policy applications manually. This results in inefficiencies, inaccuracies and overall longer turnaround times before Policies are issued but are a necessary exercise for direct life insurance underwriters. 

Through our machine learning model, we will develop a supervised machine learning model to predict the underwriting decision for new applicants based on the data completed in their application form. This will in-turn help alleviate some manpower off from the auto-accepted applications. Radically Improve Efficiency, Accuracy, and Speed of Life Insurance Underwriting with Machine Learning

## Datasets
Prudential Life Insurance Assessment competition previously hosted on Kaggle. You may find details of the competition and the dataset [here](https://www.kaggle.com/competitions/prudential-life-insurance-assessment).


##	Binary Classification
**For the purpose of this analysis**, we have turned the multiclass classification problem to binary classification problem. From the dataset, class 8 has the highest number of records which suggests that these are clean and accepted records (i.e. policy issued to these lives on standard or preferred terms) whilst the rest of the other classes can be considered as a declined application with no policy issuance.

## Model Evaluation/Metrics
|                                    |   Train score |   Test score |   Generalisation |   Accuracy |   Precision |   Recall |   Specificity |    F1 |   ROC AUC |
|:-----------------------------------|--------------:|-------------:|-----------------:|-----------:|------------:|---------:|--------------:|------:|----------:|
| Logistic Regression                |         0.813 |        0.812 |            0.123 |      0.812 |       0.724 |    0.689 |         0.871 | 0.706 |    0.8828 |
| k-Nearest Neighbour Classification |         0.783 |        0.752 |            3.959 |      0.752 |       0.619 |    0.636 |         0.809 | 0.627 |    0.8158 |
| Random Forest Classification       |         0.81  |        0.805 |            0.617 |      0.805 |       0.758 |    0.598 |         0.907 | 0.669 |    0.8867 |
| Decision Tree Classification       |         0.82  |        0.809 |            1.341 |      0.809 |       0.688 |    0.766 |         0.83  | 0.725 |    0.8791 |
| XGBoost Classification             |         0.827 |        0.824 |            0.363 |      0.824 |       0.718 |    0.762 |         0.854 | 0.739 |    0.8991 |
| AdaBoost Classification            |         0.828 |        0.824 |            0.483 |      0.824 |       0.717 |    0.769 |         0.852 | 0.742 |    0.9003 |
| Gradient Boosting Classification   |         0.844 |        0.83  |            1.659 |      0.83  |       0.735 |    0.753 |         0.867 | 0.744 |    0.9054 |


In order to solve our problem statement, we looked at the highest AUC-PR curve. This curve compares precision and recall scores at different thresholds. GB model has the highest AUCPR curve score and therefore is the best performing model. 

In addition, we looked at several criterias such as :

1. Accuracy 
2. Generalisation < 5% 
3. F1 Score

Based on the above criterias, we have selected the **Gradient Boosting Classifer**.

- **Generalisation Score** of 1.659% means that the model has the ability to properly adapt to new, previously unseen data, drawn from the same distribution as the one used to create the model.

- **Accuracy Score** of 0.83. The high Accuracy score means overall, our model classifies results correct 83% of the time. Accuracy = (TP+TN) / Total 

- **F1 Score** of 0.744. F1 Score is an average of Precision and Recall, it means that the F1 score gives equal weight to Precision and Recall. Of all the models, Gradient Boosting Classifier has the highest F1 score indicating a good balance of both Precision and Recall. 

## Conclusion 
* From our results, we have selected the Gradient Boosting Classifer model. The  model has the highest Accuracy & AUC PR curve score. Indicating the best performance amongst the other models for our specific problem statement.
 
 
* As the datasets feature names have been anonymised, it has not been possible to incorporate "business logic" but rather on a best effort basis. With the help of a "deanonymised" dataset as well as the input of subject matter expertise, it may be possible to create more predictive features and validate them for use in production. 


* Albeit limited EDA can be performed due to masked data, the top features are consistent with real world application such as applicant profile (BMI , AGE , Medical Hx).


* FP & FN cases are to be considered on a risk-to-reward basis. Different stakeholders to consider. (Cost savings vs lost business and potential losses). 



## Recommendations
* Consider using  Stacking techniques to compare the result gains by stacking the top 3 models.


* In order to mitigate the risk, may wish to consider limiting model predictions to certain products or by face value (base mortality, low sum assured cover).


* Fine tuning model for precision performance by increasing threshold such that this model may be implemented in the STP process. Cost savings would be quantified by STP cases not requiring review. Rejected applications will be reviewed by existing underwriters and thus no extra implications to resources.



