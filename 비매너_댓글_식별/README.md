## **1. 대회설명**
* 대회 기간: 2월 23일 13:00 AM ~ 3월 4일 12:00 PM 
* 과제명: 비매너 댓글 식별

## **2. 과제개요**
* 멀티 라벨 자연어 분류 (Multi-label Text Classification) <br>
자연어 영역 | 개방형 문제 | Macro F1-Score
* 문제정의 <br>
뉴스 기사의 댓글 (comment) 중 편견, 혐오 표현 (bias, hate)이 포함된 댓글을 식별하는 과제
* 추진배경 <br>
온라인 게임 속 비매너 채팅 빈도 증가 추세<br>
건전한 온라인 댓글, 채팅 문화 정착을 위한 혐오, 편견적 언어 필터링의 필요성 증대

## **3. 데이터설명**
* 데이터 구조
- train.csv : 8367개의 뉴스 기사 제목 및 해당 기사 댓글 하나, 댓글이 가진 혐오 표현 종류를 분류한 라벨 두가지 (bias, hate)
(필요에 따라 train 데이터를 train / validation 으로 나누기 가능) 
-test.csv : 511개의 뉴스 기사 제목 및 해당 기사 댓글 하나

## **4. 참여인원 및 역할**
- 참여인원 : 4명
- 역할 (팀원)
    1. **문장 길이, 토큰 수 분포** 및 **1글자, 2글자, 3글자 단어 분포**를 다양한 시각화로 나타내어 데이터 전처리를 하고 인사이트를 도출함.
    2. **TF/IDF Vectorizer**를 이용해 단어의 빈도 수를 가지고 가중치를 주었음.
    3. 우선 뉴스 기사 데이터가 잘 분류 되었는지 확인하기 위해 다양한 머신러닝 모델들을 사용하여 **Stacking 앙상블**을 이용해 성능 개선이 있는지 확인해봄.
        - **SVM,SGD,Logistic,Pac,LightGBM,XGboost 사용**
        - [TF/IDF Vectorizer를 이용하여 머신러닝 모델 적용 (notion.so)](https://www.notion.so/TF-IDF-Vectorizer-845b2b1da55d49c3aefabe26ebf9d352)
    4. **Text Augmentation**을 하기 위해 **ktextaug** 라이브러리를 이용하여 noise text로 만들기 위해 분포가 적은 bias 데이터들만 2배로 늘려주고 기존 데이터와 결합시켜 새로운 train 데이터를 생성함
    5. **Kcelectra**모델을 이용해 새로 만든 데이터를 학습시켜 성능개선 시킴.
        
## **5. 프로젝트 진행 순서**
1. **HuggingFace**에서 **Pretained된 모델**을 불러와 좋은 성능을 가진 모델을 확인.
2. 좋은 모델을 찾고, Text데이터를 **전처리**하여 성능 변화 확인
3. Text Data Augmentation을 이용하여 데이터를 늘릴 때마다 성능 변화 확인.
4. title과 comment, bias와 , hate를 각각 따로할 때와 같이 포함할 때를 비교하여 성능 확인
5. WanDb에 연결하여 Loss값 확인 및 최적의 F1-score 찾기
6. 앙상블을 이용하여 성능 개선

## **6. 사용 스택 및 협업 도구**
### **- 개발 환경**
* JupyterLab(Ubuntu), Google Colab
### **- 기술 및 라이브러리**
* python, numpy, pandas, sklearn, pytorch, Konlpy, ktextaug, transformer, Matplotlib, Seaborn, Wandb
### **- 협업 도구**
* Notion, Zoom, Discord
    
## **7. 프로젝트 내용 요약**
1. 데이터 이상치 및 결측치 확인
2. EDA를 통해 인사이트 도출하기
  * 단어의 길이를 조사하여 bias, hate 분포 확인하기
  * 토큰 수로 쪼개서 bias, hate 분포 확인하기
  * 1글자, 2글자, 3글자인 단어들을 조사하여 빈도 수 확인하기
  * 결론 <br>
  → bias에서 others와 gender 분포가 적어 학습의 불리하다고 판단(Data Augumentation을 통해 데이터를 늘려야겠다고 판단) <br>
  → 글자별로 단어를 나타낼 때 각 단어가 hate, bias에 잘 분류 되어있는것을 확인함. 
3. 모델 적용하기
    * TF/IDF를 이용한 머신러닝 모델 적용
    * Kcelectra, KcBert, Koelectra, KoRoberta 적용


### **주체**
중소벤처기업진흥공단

### **주관**
마인즈앤컴퍼니
