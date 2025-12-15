# Chapter 1. Declarative Resource Management

openshift 리소스를 배포하고 업데이트 할 때는, 
1)미리 리소스를 선언하는 declarative 방식이나 2)명령어를 사용하는 imperative 방법이 있다.

명령어를 사용해서 리소스를 다루는 경우에는 조작이 빠르지만 장애가 났을 때 추적하기가 어렵다.
그래서 테스트 하거나 간단한 작업을 하는 경우에만 사용하는 것이 좋다.

보통은 YAML 이나 JSON형식으로 리소스의 최종 목표 상태를 정의하고 관리한다.

## 계정관리

계정은 일반 계정과 관리자 계정이 있다. 두 계정은 관리 가능한 범위가 다른데, 계정이 관리하는 범위도 2가지가 있다.
cluster scope 와 namespace scope가 있는데, cluster scope는 전역변수에 해당하고 namespace는 지역변수에 해당한다.

관리자 계정은 cluster scope 까지 관리가 가능하고, 일반 계정은 본인이 만든 앱에 한정된 namespace내에서 관리가 가능하다.

### 시험에 나오는 문제
db pod 가 죽었을 때, 살려보시오

1)살리기
kubectl set env deployment/db-pod \
  MYSQL_USER='user1' \
  MYSQL_PASSWORD='*******' \
  MYSQL_DATABASE='items'

2) 확인(STATUS = RUNNING 여부)
oc get po


