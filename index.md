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
etc.제안
## Motivation
ect.동기
## Our expectations
ect.우리의 기대
# II.Datasets
데이터셋
this is the link of the dataset used in our project:
이것은 우리 프로젝트에서 사용한 데이터셋 링크입니다:
[https://www.kaggle.com/datasets/ak0212/anxiety-and-depression-mental-health-factors](https://www.kaggle.com/datasets/ak0212/anxiety-and-depression-mental-health-factors)

first, let's read the csv file and check our dataset using pandas:
먼저, CSV 파일을 읽고 pandas를 사용하여 데이터셋을 확인해 봅시다:
```python
   import pandas as pd
   df = pd.read_csv("anxiety_depression_data.csv")
   print(df.info())
   ```

we should get a terminal output like below:
터미널에서 아래와 같은 출력 결과를 얻을 수 있습니다:
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
각 열의 요약된 정보는 다음과 같습니다:
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
방법론
## Preprocessing & Feature Engineering
전처리 및 특징 엔지니어링

### NaN 값 처리

Medication_Use와 Substance_Use 열에 많은 NaN 값이 있는 것을 알 수 있으므로 이를 처리해야 합니다.

   ```python
   df['Medication_Use'] = df['Medication_Use'].fillna('None')
   df['Substance_Use'] = df['Substance_Use'].fillna('None')
   ```

### Feature Encoding
특징 인코딩
we have a few columns that have non-numeric values 
비수치형 값을 가진 몇몇 열이 있습니다
so we use **One-Hot Encoding** and **Ordinal Encoding** to preprocess the columns below:
그래서 아래 열들을 전처리하기 위해 원-핫 인코딩(One-Hot Encoding) 과 순서 인코딩(Ordinal Encoding) 을 사용합니다:
One-Hot Encoding (for categorical variables without an obvious order) :
원-핫 인코딩（One-hot encoding) (명확한 순서가 없는 범주형 변수의 경우):
| Gender | Employment_Status | Medication_Use | Substance_Use |
| 성별    | 고용 상태            | 약물 사용 여부    | 약물 사용 여부    |
| | | |

Ordinal Encoding (for categorical variables with an obvious order) ：
순서 인코딩 (명확한 순서가 있는 범주형 변수의 경우):
| Education_Level | Medication_Use | Substance_Use |
| 학력 수준          |약물 사용 여부     | 약물 사용 여부    |
| | | |

and here's the code of the encoding process:
다음은 인코딩 과정을 위한 코드입니다:
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
    "Frequent": 2
   }
   df["Substance_Use"] = df["Substance_Use"].map(substance_map)
   ```

### Feature Construction
특징 생성
to make the target values more easier to predict,
예측 대상 값을 더 쉽게 만들기 위해,
we'll create a new feature **Mental_Distress_Score**
우리는 Mental_Distress_Score 라는 새로운 특징을 생성할 것입니다.
which discribes the overall psychological distress level by combining 
이를 통해 전반적인 심리적 고통 수준을 설명합니다.
**Anxiety_Score**,**Depression_Score** and **Stress_Level**
불안 점수、우울 점수、스트레스 수준
```python
   df['Mental_Distress_Score'] = df['Anxiety_Score'] + df['Depression_Score'] + df['Stress_Level']
   ```

### Feature Selection
특징 선택
to improve model performance and interpretability,
모델 성능과 해석 가능성을 향상시키기 위해
we use several models to evaluate feature importance
여러 모델을 사용하여 특징 중요도를 평가하고
and only aim to keep features that are significant to our prediction
예측에 중요한 특징만을 선별하여 유지합니다
、p.s. in order to continue this step
추신: 이 단계를 계속 진행하기 위해서
a package other than sklearn is required, 
학습 이외의 패키지가 필요합니다,
you can install it as follows:
다음과 같이 설치할 수 있습니다:
```python
   pip install xgboost shap scikit-learn matplotlib
   ```

**First**：
먼저
use **XGBoost** to determine feature importance 
특징 중요도를 결정하기 위해 XGBoost를 사용합니다
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

Although **Gender_Male**, **Gender_Other**, and **Gender_Non-Binary** 
비록 성별_남성, 성별_기타,성별_기타,그리고 성별_논바이너리
received relatively low SHAP values, we chose not to remove them
비교적 낮은 SHAP 값을 받았지만, 우리는 이를 제거하지 않기로 결정했습니다
because they originate from the same categorical feature
왜냐하면 이들은 동일한 범주형 특징에서 비롯되었기 때문입니다
but some categories within this feature showed relatively high importance
하지만 이 특징 내 일부 범주는 비교적 높은 중요도를 보였습니다
### Standardization
표준화
we're using the SVR model form sklearn
우리는 학습의 SVR 모델을 사용하고 있습니다
because SVM is very sensitive to different feature scales
SVM은 서로 다른 특징 스케일에 매우 민감하기 때문입니다
so the standardization of our data is necessary
따라서 데이터의 표준화가 필요합니다
   ```python
   from sklearn.preprocessing import StandardScaler

   # 대상 열과 정렬된 코드화된 열을 명확하게 정의합니다(표준화 없이)
   target_cols = ['Mental_Distress_Score', 'Anxiety_Score', 'Depression_Score', 'Stress_Level']
   encoded_ordered_cols = ['Education_Level', 'Medication_Use', 'Substance_Use']

   # 모든 숫자 열
   numeric_cols = df.select_dtypes(include='number').columns.tolist()

   # One-Hot 인코딩된 열 식별: 값은 0 또는 1이고 열 이름은 get_dummies에서 가져옵니다.
   possible_one_hot_cols = [col for col in numeric_cols if df[col].nunique() <= 2 and set(df[col].unique()) <= {0, 1}]

   # 표준화할 열 = 대상 제거, 정렬된 인코딩, 원핫 인코딩 열
   standardize_cols = [
       col for col in numeric_cols
       if col not in target_cols + encoded_ordered_cols + possible_one_hot_cols
   ]

   # 표준화 수행
   scaler = StandardScaler()
   df_scaled = df.copy()
   df_scaled[standardize_cols] = scaler.fit_transform(df[standardize_cols])
   ```

# IV.Evaluation & Analysis
ect.평가 및 분석
# V.Related Work 
ect.관련 연구
# VI.Conclusion: Discussion
ect.결론: 토론
