# Loan-Data-Analysis-Numpy-Pandas-Seaborn-Matplotlib

## Python Libraries Used 

1.Numpy

2.Pandas

3.Seaborn

4.Matplotlib

## Variables in the Dataset

LOAN_NUMBER                       int64

SAMPLE_DATE                      object

FILE_REQ_DATE                    object

SECOND_REQUEST_DATE              object

SENT_TO_IMAGING_DATE             object

LENDER_RESPONSE_DUE_DATE         object

DATE_LOAN_FINALIZED              object

LENDER_ID                        object

LENDER_NAME                      object

LENDER_LOAN_ID                   object

PROP_STATE                       object

NEW_CONSTRUCTION_INDICATOR       object

CONDOMINIUM_INDICATOR            object

LOAN_ORIG_DATE                   object

 CURRENT_BALANCE                 object
 
FICO_SCORE                        int64

LTV                             float64

 ORIG_VALUE                      object
 
 AVM_VALUE                       object
 
FIELD_REVIEW_VALUE_SUPPORTED     object

FIELD_REVIEW_VALUE              float64

PURPOSE_CODE                     object

OCCUPANCY_CODE                   object

LENDER_INST_TYPE_DESCRIPTION     object

UNDERWRITER_NAME                 object

REVIEW_DATE                      object

REVIEW_STATUS                   float64

DEAL_NAME                        object

START_DATE                       object

## Importing Pandas and Numpy libraries
import pandas as pd

import numpy as np

df=pd.read_csv("LoanDataN.csv")

df.dtypes

df.columns = df.columns.str.replace(' ','')

## Descriptive Statistics

![image](https://user-images.githubusercontent.com/100436462/221300960-02dce4a9-1cce-492c-bc7a-a36f6076acaf.png)

## Converting column Current Balance from object to float

![image](https://user-images.githubusercontent.com/100436462/221301132-a9457ff1-15a5-4b9f-b3a5-5dbc70a9253c.png)

## REPORT 1: Data by Lender Institution Type

![image](https://user-images.githubusercontent.com/100436462/221303280-0392d82f-488c-473b-97a1-944b9df35c49.png)

## REPORT 2: Data by LTV (Loan to Value) Cohorts

## Create a list of our conditions
conditions = [
    (df['LTV'] <= 85),
    (df['LTV'] > 85) & (df['LTV'] <= 90),
    (df['LTV'] > 90) & (df['LTV'] <= 95),
    (df['LTV'] > 95)
    ]

## Create a list of the values we want to assign for each condition
values = ['<= 85%', '>85% and <= 90%', '>90% and <= 95%', '> 95%']

## Create a new column and use np.select to assign values to it using our lists as arguments
df['LTV_Cohort'] = np.select(conditions, values)

### Display updated DataFrame
df.head()

![image](https://user-images.githubusercontent.com/100436462/221303749-e0b19ffb-5cad-4c0a-a4bc-0cc1cf74cfec.png)

## REPORT 3: Data by Loan Age Cohort (Loan Age = 6/1/2013 minus LOAN_ORIG_DATE in months)

### Create a list of our conditions
conditions = [
    (df['Loan_Age'] >= 0) & (df['Loan_Age'] <= 9),
    (df['Loan_Age'] >=10) & (df['Loan_Age'] <= 19),
    (df['Loan_Age'] >=20) & (df['Loan_Age'] <= 29),
    (df['Loan_Age'] > 30) & (df['Loan_Age'] <= 39),
    (df['Loan_Age'] >= 40)
    ]

### Create a list of the values we want to assign for each condition
values = ['0 - 9 Months', '10 - 19 Months', '20 - 29 Months', '30 - 39 Months','>= 40 Months']

### Create a new column and use np.select to assign values to it using our lists as arguments
df['Loan_Age_Cohort'] = np.select(conditions, values)

![image](https://user-images.githubusercontent.com/100436462/221304273-c0764891-85a5-427b-9b11-cd5d4da1bf85.png)

## REPORT 4: Crosstab Report- SUM of CURRENT_UPB by LTV Cohorts and FICO Cohorts


![image](https://user-images.githubusercontent.com/100436462/221304535-7527e9ca-c910-4a8e-9a09-b4842882af93.png)

## Bar graph of  Report 4: SUM of CURRENT_UPB by LTV Cohorts and FICO Cohorts

import seaborn as sns

chart = sns.catplot(data=df, x="LTV_Cohort", y="Sum_Current_Balance", hue="FICO_Cohort", kind="bar")

chart.set_xticklabels(rotation=45)

plt.subplots_adjust(top=0.9)

plt.suptitle('SUM of CURRENT_UPB by LTV Cohorts and FICO Cohorts ', fontsize = 12)

![image](https://user-images.githubusercontent.com/100436462/221304741-685f0005-e895-4b1d-b374-cc2322d094ab.png)






