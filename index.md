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
| Physical_Activity_Hrs | 주간 운동 시간(시간) | 수치 | 0.0-13.4시간 |
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
ect.
# IV.Evaluation & Analysis
ect.
# V.Related Work 
ect.
# VI.Conclusion: Discussion
ect.
