---
layout: single
title: ""
permalink: /
toc: true
toc_sticky: true
---

팀원들: 

 * 박문길 경영학과 jinyu@hanyang.ac.kr

 * 진이 무용학과 chenyi20020923@gmail.com
       
 * 장범 영어영문학과 zhangfan20000408@163.com
       
 * 증자서 인공지능학과 zzxzzx1818@163.com
       
# I.Proposal
etc.
## Motivation
ect.
## Our expectations
ect.
# II.Datasets

this is the link of the dataset used in our project:

[https://www.kaggle.com/datasets/ak0212/anxiety-and-depression-mental-health-factors](https://www.kaggle.com/datasets/ak0212/anxiety-and-depression-mental-health-factors)

first, let's read the csv file and check our dataset using pandas:

   ```python
   import pandas as pd
   df = pd.read_csv("anxiety_depression_data.csv")
   print(df.info())
   ```

we should get a terminal output like below:

   ```python
   <class 'pandas.core.frame.DataFrame'>
   RangeIndex: 1200 entries, 0 to 1199
   Data columns (total 21 columns):
    #   Column                         Non-Null Count  Dtype
   ---  ------                         --------------  -----
    0   Age                            1200 non-null   int64
    1   Gender                         1200 non-null   object
    2   Education_Level                1200 non-null   object
    3   Employment_Status              1200 non-null   object
    4   Sleep_Hours                    1200 non-null   float64
    5   Physical_Activity_Hrs          1200 non-null   float64
    6   Social_Support_Score           1200 non-null   int64
    7   Anxiety_Score                  1200 non-null   int64
    8   Depression_Score               1200 non-null   int64
    9   Stress_Level                   1200 non-null   int64
    10  Family_History_Mental_Illness  1200 non-null   int64
    11  Chronic_Illnesses              1200 non-null   int64
    12  Medication_Use                 453 non-null    object
    13  Therapy                        1200 non-null   int64
    14  Meditation                     1200 non-null   int64
    15  Substance_Use                  366 non-null    object
    16  Financial_Stress               1200 non-null   int64
    17  Work_Stress                    1200 non-null   int64
    18  Self_Esteem_Score              1200 non-null   int64
    19  Life_Satisfaction_Score        1200 non-null   int64
    20  Loneliness_Score               1200 non-null   int64
   dtypes: float64(2), int64(14), object(5)
   memory usage: 197.0+ KB
   ```

and here's the summarized information of every column: 

| 변수명 | 설명 | 유형 | 범위/예시 |
|--------|------|------|----------|
| Age | 응답자 연령 | 수치 | 18-74세 |
| Gender | 성별 | 범주 | 남성, 여성, 논바이너리, 기타 |
| Education_Level | 교육 수준 | 범주 | 고등학교, 학사, 석사, 박사, 기타 |
| Employment_Status | 고용 상태 | 범주 | 취업자, 실업자, 학생, 은퇴자 |
| Sleep_Hours | 일일 수면 시간(시간) | 수치 | 2.0-12.4시간 |
| Physical_Activity_Hrs | 주간 운동 시간(시간) | 수치 | 0.0-15.1시간 |
| Social_Support_Score | 사회적 지지 점수 | 수치 | 1-9(점수가 높을수록 지지가 강해진다) |
| Anxiety_Score | 불안 증상 점수 | 수치 | 1-20(점수가 높을수록 증상이 심해진다) |
| Depression_Score | 우울 증상 점수 | 수치 | 1-20(점수가 높을수록 증상이 심해진다) |
| Stress_Level | 스트레스 수준 | 수치 | 1-9(점수가 높을수록 스트레스가 커진다) |
| Family_History_Mental_Illness | 정신 질환 가족력 | 이분 | 0(없음), 1(있음) |
| Chronic_Illnesses | 만성 질환 | 이분 | 0(없음), 1(있음) |
| Medication_Use | 약물 사용 빈도 | 범주 | 없음, 가끔, 정기적 |
| Therapy | 심리 치료 여부 | 이분 | 0(아니오), 1(예) |
| Meditation | 명상 실천 여부 | 이분 | 0(아니오), 1(예) |
| Substance_Use | 물질 사용 빈도 | 범주 | 없음, 가끔, 빈번함 |
| Financial_Stress | 재정적 스트레스 | 수치 | 1-9(점수가 높을수록 스트레스가 커진다) |
| Work_Stress | 직장 스트레스 | 수치 | 1-9(점수가 높을수록 스트레스가 커진다) |
| Self_Esteem_Score | 자아 존중감 점수 | 수치 | 1-9(점수가 높을수록 자존감이 강해진다) |
| Life_Satisfaction_Score | 삶의 만족도 | 수치 | 1-9(점수가 높을수록 만족도이 높아진다) |
| Loneliness_Score | 외로움 점수 | 수치 | 1-9(점수가 높을수록 외로움이 심해진다) |

# III.Methodology

## Preprocessing & Feature Engineering

### Feature Encoding

we have a few columns that have non-numeric values 

so we use **One-Hot Encoding** and **Ordinal Encoding** to preprocess the columns below:

One-Hot Encoding (for categorical variables without an obvious order) :

| Gender | Employment_Status | Medication_Use | Substance_Use |
|---------|--------------------|-----------------|----------------|
| | | |

Ordinal Encoding (for categorical variables with an obvious order) ：

| Education_Level | Medication_Use | Substance_Use |
|------------------|-----------------|----------------|
| | | |

and here's the code of the encoding process:

   ```python
   df = pd.get_dummies(df,columns=[
    "Gender",
    "Employment_Status",
   ], drop_first=False,dtype=int)
   ```

   ```python
   education_map = {
    "Other": 0,
    "High School": 1,
    "Bachelor's": 2,
    "Master's": 3,
    "PhD": 4
   }
   df["Education_Level"] = df["Education_Level"].map(education_map)

   medication_map = {
    "None": 0,
    "Occasional": 1,
    "Regular": 2
   }
   df["Medication_Use"] = df["Medication_Use"].map(medication_map)
   
   substance_map = {
    "None": 0,
    "Occasional": 1,
    "Regular": 2
   }
   df["Substance_Use"] = df["Substance_Use"].map(substance_map)
   ```

### Feature Construction

to make the target values more easier to predict,

we'll create a new feature **Mental_Distress_Score**

which discribes the overall psychological distress level by combining 

**Anxiety_Score**,**Depression_Score** and **Stress_Level**

   ```python
   df['Mental_Distress_Score'] = df['Anxiety_Score'] + df['Depression_Score'] + df['Stress_Level']
   ```

### Feature Selection

to improve model performance and interpretability,

we use several models to evaluate feature importance

and only keep features that are significant to our prediction

p.s. in order to continue this step

a package other than sklearn is required, 

you can install it as follows:

   ```python
   pip install xgboost shap scikit-learn matplotlib
   ```

**First**：

use **XGBoost** to determine feature importance 

   ```python
   import numpy as np
   import xgboost as xgb
   import shap
   import matplotlib.pyplot as plt
   from sklearn.model_selection import train_test_split
   from sklearn.metrics import mean_squared_error, r2_score

   # select the target column and other training data separately
   X = df.drop(columns=['Mental_Distress_Score','Anxiety_Score','Depression_Score','Stress_Level'])
   y = df['Mental_Distress_Score']

   # spliting the data 
   X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

   # model training
   model = xgb.XGBRegressor(
    n_estimators=100,
    max_depth=4,
    learning_rate=0.1,
    subsample=0.8,
    random_state=42
   )
   model.fit(X_train, y_train)

   # model evaluation
   y_pred = model.predict(X_test)
   mse = mean_squared_error(y_test, y_pred)
   rmse = np.sqrt(mse)
   r2 = r2_score(y_test, y_pred)
   print(f"RMSE: {rmse:.2f}")
   print(f"R² Score: {r2:.3f}")

   # initializ explainer
   explainer = shap.Explainer(model, X_train)

   # getting the SHAP value
   shap_values = explainer(X_train)

   # displaying feature importance
   shap.plots.bar(shap_values, max_display=25)
   ```

![feature importance](img/1.png)

so we'll drop columns that scores under 0.1

   ```python

   ```

# IV.Evaluation & Analysis
ect.
# V.Related Work 
ect.
# VI.Conclusion: Discussion
ect.
