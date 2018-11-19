# Amazon SageMaker와 Athena를 활용한 대용량 자연어처리 및 머신러닝 기법

## 아마존 고객 리뷰 데이터 셋
아마존은 1995년부터 프로덕트 리뷰를 도입하였다. 직접 사용한 경험들을 나누고 있다.
> 전세계 아마존 자연어처리 연구자들에게 도움이 된다.
> 아마존 고객리뷰데이터는 아마존의 중요한 자산입니다. 현재 1억 3천만개 이상의 고객 리뷰 자료가 연구 목적의 경우 자유로이 사용할 수 있게 공개되어 있습니다.

## 순서
* Athena : S3의 저장된데이터에 대해 SQL질의를 수행할 수 있게 합니다. 
* SageMaker : 비지도 방식의 데이터 분류와 지도 학습 방식의 고객 평가 점 예측을 실습
    1. NTM과 K-Means알고리즘을 활용하여 고객평가문을 자동으로 그룹별로 분류해봅니다.
    2. 주어진 고객평가문장으로 Comprehend서비스 처럼 리뷰점수를 예측하는 ML서비스를 개발해봅시다.

    > Amazon Reviews Dataset -> Amazon Athena -> Query Request -> SageMaker 

## Amazon Athena가 필요한 경우
* Amazon S3에 저장된 데이터를 직접 분석하고 싶은 경우
    * ETL(extrackt-Transform-Loading) 작업을 데이터 웨어하우스에서 하기 위해서 방대한 양의 작업이 필요하기 때문입니다.

* AWS US East (N.Virginia) Region의 `amazon-reviews-pds` S3 버킷에 저장되어 있습니다.
* TSV, Paraquet 데이터 포맷으로 저장되어 있습니다.
* Athena 의 질의 결과는 S3 에 저장할 수 있습니다.
* presto기반으로 Athena 가 구축되었다.

## Deep Learning /w SageMaker
* Data의 중요성 : 알고리즘 선정보다 학습 데이터의 양이 더 중요.
* SageMaker
    > Build, Train and deploy machine learning models at scale
    * End-to-End Machine Learning Platform
    * Zero Setup
    * Flexible Model Training
    * `PAY BY THE SECOND`
    * 개발에 필요한 서버, 학습에 필요한 서버, 배포에 필요한 서버를 다 구축해야한다.
    * 어떠한 규모의 워크로드도 지원가능한 실전형 머신러닝
        * 데이터 : 페타바이트 대용량 데이터, 스트리밍 데이터, 다양한 마이그레이션 도구
        * 학습 : 대규모 GPU서버, 병렬 트레이닝, 고성능 알고리즘 제공
        * 예측 : 대규모 GPU/CPU서버, 자동확장 서버 구축, 서버리스, 엣지 IoT
    * 노트북에서 Python SDK로 Athena 테이블 생성
  
* PANDAS 를 활용한 데이터 분석
  
* Demo ; https://github.com/pilhokim/amazon-sagemaker-workshop
* Stemming and Lemmaization
    * 형태소 분석을 통한 어간 추출(Steeming)과 표제어 추출(Lemmaization)은 실제 사용될 단어의 갯수를 효과적으로 줄여서 훈련과 추론 계산 시간을 향상시키게 합니다.
    * 이 작업은 학습된 토픽 단어들의 확률 예측 치 및 추론된 토픽 값들의 조합 결과들을 향상시키는 데에 큰 도움이 됩니다.
* NTM을 활용한 토픽 모델 구성법
    * `Neural Topic Model` 은 비지도 학습 알고리즘으로 발견된 데이터 셋을 별개의 카테고리의 조합으로 표현합니다.
    * NTM은 말뭉치 안의 문서들 간에 공유되어 있는 사용자 지정 갯수만큼의 퇵들을 발견하는데 주로 사용됩니다.
    * 각 관차로딘 내용들은 문서가 되고 특징들은 각 단어들의 존재를 의미하고 카테고리들은 토픽들이 됩니다.
    * 토픽들은 각 문서에 존재하는 단어들간의 분산된 확률을 학습해서 발견하게 됩니다. 각 문서들은 따라서 토픽드르이 조합으로 표현됩니다.
* K-means를 활용한 토픽모델링
    * K-Means 는 **비지도 학습 알고리즘**으로 데이터를 지정한 유사도를 기준으로 각각의 그룹으로 분류합니다.
    * SageMaker의 K-Means는 Web-scale k-means Clustering 알고리즘을 수정하여 정확도를 향상시킨 버전입니다.
    * `extra_center_factor`를 설정하면 num_cluster * extra_center_factor 갯수만큼 cneter가 초기에 생성이 되고 트레이닝이진행되면서 num_clusters 개수만큼 줄어들게 됩니다.
* Term Frequency-Inverse Document Frequency,
    * 문서들을 TFIDF 유사성에 따라 N개의 클러스터로 구분하는 기법입니다.
    * TFIDF 또는 tf-idf 는 수치통계기법으로 어떤 단어가 문서집합내에서 얼마나 중요한지를 반영하는 방식입니다.
    * TFIDF는 정보 추출, 텍스트 마이닝, 그리고 사용자 모델링 기법의 검색 과정에서 가중치로 종종 사용됩니다.c 