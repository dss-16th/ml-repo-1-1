<img width="739" alt="스크린샷 2021-05-12 오후 5 03 25" src="https://user-images.githubusercontent.com/75604413/117940416-02bcae80-b344-11eb-986c-9b3943580b69.png">




***
# 1. 개요
### 1-1 프로젝트 목적
- 본 프로젝트는 실제 SOCAR 사고차량 데이터를 기반으로 보험 사기 차량을 분류하는 머신러닝 프로젝트 입니다.
- 해당 프로젝트에서는 재작년에 비해 2배 이상 성장한 공유차량 업계에서 급증한 보험사기 사례의 심각성을 인지하고 사기 차량을 구분하는 것을 목표로 합니다.
- 해당 프로젝트에서는 실제 데이터를 통해 머신러닝 과정을 이해하고 모델 성능을 높이기 위해 사용한 머신러닝 모델 알고리즘과 샘플링 기법을 학습합니다.





### 1-2 데이터 소개
- 해당 데이터는 SOCAR에서 제공받은 실제 데이터로 총 16000개 row, column은 총 25개로 구성 (컬럼 비공개)
- Null 값은 없었으나 알수없음 및 확인불가 값을 결측치로 판단


<img width="310" alt="스크린샷 2021-04-27 오후 6 31 40" src="https://user-images.githubusercontent.com/78460413/116219671-cfe0bb00-a786-11eb-811c-a0cf02bf2f3b.png">

16000개 차량 데이터 중 사기 데이터는 41개 불균형 데이터**


### 1-3 프로젝트 진행 프로세스
<img width="605" alt="스크린샷 2021-05-13 오전 11 25 28" src="https://user-images.githubusercontent.com/78460413/118069058-6dbac380-b3de-11eb-9911-8095430ca85c.png">


* 범주형 데이터 결측치 최빈값 대체 및 연속형 데이터 결측치 중앙값 대체

<img width="465" alt="스크린샷 2021-05-13 오전 10 12 51" src="https://user-images.githubusercontent.com/75604413/118063299-c8025700-b3d3-11eb-9f45-e69e3878661b.png">

  - 결측치 최빈값 및 중앙값 대체 후 샘플러 적용
  - adasyn 샘플링 한 Logistic Regression에서 높은 성능 


### 4-3 하이퍼 파라미터 튜닝 

<img width="521" alt="스크린샷 2021-05-13 오전 10 15 06" src="https://user-images.githubusercontent.com/75604413/118063460-1879b480-b3d4-11eb-9290-13febc96d27b.png">

<img width="438" alt="스크린샷 2021-05-13 오전 10 16 31" src="https://user-images.githubusercontent.com/75604413/118063550-4bbc4380-b3d4-11eb-91c0-afe581da6d27.png">

# 5. 결과 및 회고

### 5-1. 최종 모델
 4가지로 모델 성능을 평가 한 결과, Logistic regression 모델로, accuracy 77% recall 85% 성능을 보임
<img width="386" alt="스크린샷 2021-04-27 오후 7 05 48" src="https://user-images.githubusercontent.com/78460413/116224412-9494bb00-a78b-11eb-8f35-3f771a0ef116.png">

    
# 2. EDA


### 2-1. Insight




# 3. 데이터 전처리
  - [x] 결측치 및 이상치 
    > 범주형 데이터 결측치 : '알 수 없음' 및 '확인 불가' 값을 결측치로 판단. 이를 최빈값으로 대체
    
    > 연속형 데이터 결측치 : 0값을 평균값과 중앙값으로 대체
  - [x] 범주화
    > 인코딩 : 범주형 데이터들을 원핫 인코딩을 사용해 변경
  - [x] 스케일링
    > MinMax scaling, Standard Scaling, Robust Scaling, Log Scaling
  - [x] 샘플링
    > RandomOverSampling, ADASYN, SMOTE-ENN 


# 4. 모델링 

  ### 머신러닝 모델
  
  
<img width="467" alt="스크린샷 2021-04-27 오후 7 01 13" src="https://user-images.githubusercontent.com/78460413/116223867-f0ab0f80-a78a-11eb-94e0-90905ce013bc.png">


  ### 4-1. 평가 지표 및 기준
  <img width="454" alt="스크린샷 2021-05-13 오전 9 46 01" src="https://user-images.githubusercontent.com/75604413/118061782-976cee00-b3d0-11eb-9051-e9598edec649.png">
  
  * 실제 사기 데이터 중 모델이 사기라 예측한 recall(재현율)을 주요 지표로 분석
  * Baseline : 범주화와 스케일링만을 적용한 모델을 선정. accuracy 41% 와 recall 14%
  * Baseline 수치보다 성능을 높이는 것을 목표로 하고, 정확도를 높이기 위하여 recall 수치를 높이는 것으로 평가기준 설정
  
  
  ### 4-2. 모델링
  
  * 범주화 및 스케일링
 <img width="478" alt="스크린샷 2021-05-13 오전 9 55 51" src="https://user-images.githubusercontent.com/75604413/118062197-6b9e3800-b3d1-11eb-8dc7-0da2c3fe6f21.png">
 
 - 범주화 및 스케일링만 진행한 데이터는 모든 모델에서 낮은 성능 나타남. 비교적 Logistic Regression에서 높은 recall을 보였지만 accuracy가 낮았음

  * cost 컬럼 로그 스케일링 및 샘플링

<img width="394" alt="스크린샷 2021-05-13 오전 10 03 25" src="https://user-images.githubusercontent.com/75604413/118062688-773e2e80-b3d2-11eb-8596-a63ff90a84a6.png">

<img width="343" alt="스크린샷 2021-05-13 오전 10 09 36" src="https://user-images.githubusercontent.com/75604413/118063082-54604a00-b3d3-11eb-98e9-7d8eb00417a6.png">

  - 연속형 값 가진 두 컬럼에 로그 스케일링 적용함 
 

<img width="361" alt="스크린샷 2021-05-13 오전 10 10 16" src="https://user-images.githubusercontent.com/75604413/118063134-6b9f3780-b3d3-11eb-8130-b2c12be7afd0.png">

  - 오버 샘플러인 randomover 및 adasyn 적용, 복함 샘플러인 SMOTE-ENN 적용
  - RandomOver 샘플러를 적용한 Decision tree 모델에서 비교적 recall 수치 높았지만 높은 성능은 아님



### 5-2. 회고
  - 다양한 전처리 부재
  - 하이퍼 파라미터 튜닝 시 다양한 파라미터 적용 부재

# 6. Contributor
- [정다은] (https://github.com/**** )
  - 데이터 탐색(EDA), 스케일링을 통한 데이터 전처리, 샘플링을 이용한 모델링, PPT 및 리드미 자료 작성
- [이지홍] (https://github.com/jihong7107)
  - 데이터 탐색(EDA), 결측치 처리를 통한 데이터 전처리, 샘플링을 이용한 모델링, PPT  리드미 자료 작성
  

