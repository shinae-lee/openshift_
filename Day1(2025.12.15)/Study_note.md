# Chapter 1. Declarative Resource Management

openshift 리소스를 배포하고 업데이트 할 때는, 
1)미리 리소스를 선언하는 declarative 방식이나 2)명령어를 사용하는 imperative 방법이 있다.

명령어를 사용해서 리소스를 다루는 경우에는 조작이 빠르지만 장애가 났을 때 추적하기가 어렵다.
그래서 테스트 하거나 간단한 작업을 하는 경우에만 사용하는 것이 좋다.

보통은 YAML 이나 JSON형식으로 리소스의 최종 목표 상태를 정의하고 관리한다.

