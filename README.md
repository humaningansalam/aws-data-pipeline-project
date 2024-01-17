참여자 : 금도영 신민종 윤상훈 이정복

프로젝트 기간 : 2023.11.08 ~ 2023.12.15

## **프로젝트 개요**

- aws 기능을 활용한 데이터파이파인 구축
- spark와 emr을 사용해 데이터 ETL


## **프로젝트 기술 스택**

![스크린샷 2024-01-15 185223](https://github.com/humaningansalam/aws-data-pipeline-project/assets/89466243/cf2e8a56-e7fa-491a-9ece-4b8aeee8c327)

## **팀원 소개**

- 금도영
    - 팀장
    - 데이터 전처리
    - airflow EMR 자동화
    - superset 설치 및 시각화
- 신민종
    - 데이터 적재
    - 데이터 분석 및 쿼리 작성
    - airflow EMR, 적합성 자동화
- 윤상훈
    - 데이터적재
    - EMR환경 구축
    - mlflow
    - 모니터링 환경 구축
- 이정복
    - 데이터 전처리
    - 시각화 quick sight ,super set
    - airflow 설치



## **프로젝트 과정 소개**

![01](https://github.com/humaningansalam/aws-data-pipeline-project/assets/89466243/844c3cab-0aa1-42c4-b2fa-1b5be5e1df2d)

- kaggle 데이터를 spark를 사용하여 s3에 업로드
- 적제된 데이터를 aws emr을 통해 파티셔닝 버켓팅 진행
- s3에 적제된 transformed data를 aws athena 쿼리 조회
- aws quicksight를사용하여 적제된 데이터 대시보드로 확인
- 위의 과정들을 airflow로 자동화



## **프로젝트 세부 과정**

pyspark를 통해  s3에 파티셔닝 버켓팅을 통한 데이터적재

- 각 kaggle 데이터  articles, customers, transactions 파티셔닝 버켓팅을 소개
- 압축해서 적재 (parquet)

- 고민하여 추가해볼것들
    - 파티셔닝은 어떻게 진행했는지
    - 압축 방법은 또 머가있을까
  
  
[변환된 데이터 표시]

CNN으로 이미지 분류 학습을 시켜 카테고리별  파티셔닝 진행

- 95퍼정도의 정확도를 얻을수 있었지만 애시당초 데이터가 불균형한 문제가 있어서 신뢰 하기는 힘듬
- 이미지 분류를 했을때 사용한 모델을 서빙하는 과정도 포함해야할듯
    - 단순히 모델을 api서버에 띄어 결과값을 받아오는 과정을 시작으로 →
    - api 서버 도커 이미지화 →
    - 모델 관리의 필요성을 느껴 mlflow →
    - mlflow를 사용해 모델 서빙 →
    - mlflow의 모델서빙의 불편함을 느껴 서빙은 api로 대채
      
- 고민하여 추가해볼것들
    - 서빙의 강점이 있는 bentoml을 썻더라면??
    - CNN을 선정한 이유
    - 데이터 불균형이 있다면 어떻게 해결해야될까
    - mlflow를 왜썼는지? 모델 관리를 어떤식으로 해주는지
    - 모델서빙에 api 말고 다른 방식들은??


aws emr를 사용해 파티셔닝 버켓팅

- emr 성능 선택 방법
- 한정적인 권한을 얻을 수밖에 없었을때 생겼던 aws 권한 문제들

- 고민하여 추가해볼것들
     - aws emr serverless를 썻더라면(지금 상황은 serverless가 더 어울리는듯)

[emr 표시]

aws athena

- 아테나 쿼리에 대한 설명
- 파티셔닝을 해 리소스관점에서 이득을 봄
- parquet 형식으로 변환했을때 데이터 타입 변화의 문제

- 고민하여 추가해볼것들
    - athena대채제들??
  
aws quicksight

- athena에서 데이터 쿼리를 날려 대시보드작성
- 한정적 자원문제로 무료인 superset으로 변환

[quicksight 대시보드 표시]

airflow 

- ETL 작업의 자동화를 airflow로 구현
- 각 작업들이 완료될때마다 slack으로 메세지를 받을수있게함
- 데이터 적합성 로직 추가
- airflow 무거운웠던 문제

- 고민하여 추가해볼것들
    - airflow 대채 argo wrokflow 

[작동상태의 airflow 표시]

ci/cd

- mlflow와 ml api server를 도커 이미지화 시켜 이걸 ci/cd한거 설명
- ml api server build test할때  healthcheck 기능을 사용해 빌드가 잘되었는지 확인했음
- slack으로 진행상황을 메세지로 받아볼수있게 구현
- ml api server 로직은  더 복작하다함  기존 배포되어있는 모델의 성능을 비교해서 더 좋으면 배포 이런식으로

mlflow

- 모델 로깅
- 모델 서빙

[모델 로깅된 mlflow ui 표시]


모니터링

- aws → nodexporter
- airflow → statsd
- 프로메테우스 그라파나 모니터링
- alert를 통한 slack 메세지

[모니터링 대시보드 표시 및  slack 메세지 캡쳐]

## **프로젝트 결과**

[aws emr 비용]

## **프로젝트 회고**


[노션정리 팀프로젝트]
