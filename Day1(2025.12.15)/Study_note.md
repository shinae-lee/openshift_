# Chapter 1. Declarative Resource Management

openshift 리소스를 배포하고 업데이트 할 때는, 
1) 미리 리소스를 선언하는 declarative 방식과 
2) 명령어를 사용하는 imperative 방법이 있다.

명령어를 사용해서 리소스를 다루는 경우에는 조작이 빠르지만 장애가 났을 때 추적하기가 어렵다.
그래서 테스트 하거나 간단한 작업을 하는 경우에만 사용하는 것이 좋다.

보통은 YAML 이나 JSON형식으로 리소스의 최종 목표 상태를 정의하고 관리한다.

## 리소스 생성과 관리

openshift에서 사용하는 계정은 일반 계정과 관리자 계정이 있다. 
두 계정은 관리 가능한 범위가 다른데, 계정이 관리하는 범위도 2가지가 있다.
cluster scope 와 namespace scope가 있는데, cluster scope는 전역변수에 해당하고 namespace는 지역변수에 해당한다.

관리자 계정은 cluster scope 까지 관리가 가능하고, 일반 계정은 본인이 만든 앱에 한정된 namespace내에서 관리가 가능하다.

### 시험에 나오는 문제
db pod 가 죽었을 때, 살려보시오

1) 살리기
kubectl set env deployment/db-pod \
  MYSQL_USER='user1' \
  MYSQL_PASSWORD='*******' \
  MYSQL_DATABASE='items'

여기서 set env 는 환경설정하는 명령어이다.

2) 확인(STATUS = RUNNING 여부)
oc get po


#### 프로젝트 생성 후, 클러스터 외부에서 접속하고 싶을 때

같은 cluster 내부에서는 curl 명령어로 pod에 접속이됨.
외부에서 접속하려면, apache_service.yaml을 따로 만들어야함.

1) vim apache_service.yaml

[apache_service.yaml 내용]

apiVersion: v1
kind: Service
metadata:
  name: apache-service
spec:
  ports:
    - port: 8080


2) oc create -f apache-service.yaml


#### oc apply와 oc create의 차이점

oc create 명령어를 쓰면, 전부 다 변경하므로 일부를 변경하고 싶으면
oc apply -f apache-service.yaml 을 사용해야한다. 


#### yaml 파일 작성시 문법이 헷갈리면 아래 명령어 사용하면 됨.

oc explain svc 
oc explain service.spec


live resource 는 edit 으로 본다

