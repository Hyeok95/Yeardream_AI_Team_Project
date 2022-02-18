## **1. 대회설명**
* 대회 기간: 2월 8일 13:00 AM ~ 2월15일 12:00 PM 
* 과제명: 흉부CT를 이용한 코로나 감염 여부 분류 과제 수행

## **2. 과제개요**
이미지 영역 | 개방형 문제 | Accuracy

* 문제정의<br>
흉부 CT 이미지를 이용해 코로나19 감염 여부를 이진 분류

* 추진배경
  * 코로나 펜데믹 도래와 장기화에 따른 코로나 확진자 분류 필요성 증대
  * 의료 이미지 AI 기술 적용 가능성 확대

## **3. 데이터설명**

* 문제설명<br>
흉부 CT 이미지를 이용해 코로나19 감염 여부를 이진 분류하는 과제입니다. train.csv에 학습 데이터의 각 타겟값('COVID' 컬럼) 정보가 들어있습니다.

* 제출 방법<br>
test.zip 내의 sample_submission.csv의 'COVID' 컬럼에 0(비감염) 또는 1(감염) 값을 채워 제출하세요.<br>
모든 test 이미지에 대해 값을 채워 제출해야 정상적으로 채점됩니다. <br>
public:private 데이터 비율은 약 3:7이며, 대회 중에는 public 스코어만 리더보드에서 확인되고, 대회 종료 후 private 스코어만 반영한 최종 순위가 공유됩니다.<br>
그렇기 때문에 public 리더보드의 점수와 CV 스코어 등을 고려하여 최종 파일 2개를 선택해주시기 바랍니다.<br>
('결과제출'에서 해당 파일의 '최종선택' 체크박스 선택) <br>
최종 파일 미선택 시, public 스코어가 가장 높은 2개의 제출 파일이 자동 선택됩니다.

## **4. 참여인원 및 역할**
    - 참여인원 : 4명
    - 역할 (팀원)
        1. 기본 Baseline 코드를 가지고 모델 별로 성능을 확인!
            - CNN, DCNN, AlexNet, VGG, ResNet, EfficientNet 사용함.
            - 이 중에서 VGG모델이 성능이 좋아서 VGG모델을 사용하였음.
        2. 좋은 성능을 가진 모델을 찾아서 baseline 코드를 수정하여 팀원들이 쓸 수 있도록 재구성함.
        3. 팀원이 진행한 Data Augumentation 코드를 받아서 적용 시킨 후 다시 데이터를 증식한 단계에서 모델 별로 성능을 확인.
        
## **5. 프로젝트 진행 순서**
    
    1. 기본 Baseline 코드를 가지고 모델별로 성능을 확인해본다
    
    - CNN, DCNN, AlexNet, VGG, ResNet, EfficientNet...
    
    2. 모델별로 돌려보고 Hyperparameter 튜닝 및 batch_size, image_size 등 조절
    
    3., 과적합 발생 시 과적합 방지를 위해 Dropout, BatchNorm, Early Stopping 등을 사용함
    
    4. Data Augumentation을 통해 데이터를 뻥튀기 시켜서 성능이 올라가는 지 확인
    
    5. k-fold 및 앙상블을 써서 성능을 향상 시키도록 함.
    
    - hard voting, soft voting...
    
    -> 1번과 3번 순서를 바꿔서도 진행해봄

## **6. 사용 스택 및 협업 도구**
**- 개발 환경**
        - JupyterLab(Ubuntu), Google Colab
**- 기술 및 라이브러리**
        - python, albumentations, numpy, pandas, cv2, sklearn, dataloader, torch, transforms
**- 협업 도구**
        - Notion, Zoom, Discord
    
## **7. 프로젝트 내용 요약**
    1. 주어진 데이터를 가져와 dataloader 설정 후 Train과 Valid를 9:1로 나눔.
    2. Seed값과 파라미터 값 설정
    3. Albumentation 모듈을 이용하여 Data Augumentation을 진행함.
        - Resize, RandomCrop, HorizontalFlip, Normalize, RandomBrightnessContrast, RandomRotate, VerticalFlip 이용
    4. 모델을 돌려가며 제일 좋은 성능을 가진 모델을 선정함.
        - Pytorch 공식 문서에 있는 모델들을 불러와 pretained=False를 써서 사용함.
            - ResNet, Efficient 모델 사용
        - Baseline에 쓰여진 CNN(Lenet)과  DCNN, AlexNet, VGG11, VGG13, VGG16모델을 사용
    5. 모델을 돌려보며 과적합 발생 시 과적합 방지를 위해 Dropout, BatchNorm을 사용하여 성능 향상 알아봄
    6. EarlyStopper을 사용하여 손실이 올라가게 되면 과대적합으로 적용시켜 학습을 종료시킴.
    7. 모델별로 나온 결과를 저장시킨 후 앙상블인 Soft Voting과 Hard Voting을 이용해 accuracy를 높힘.


### **주체**
중소벤처기업진흥공단

### **주관**
마인즈앤컴퍼니
