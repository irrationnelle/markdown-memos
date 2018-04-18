## 자동화

* 자동화 작업을 위하여 도커를 사용

## 빌드 자동화

* 빌드 서버: 빌드 서버는 개인 컴퓨터여도 되고 별도의 서버여도 상관없음
* 젠킨스 사용

## VPC

* 디폴트 VPC 보다 완전히 프라이빗한 환경을 위해 새로운 VPC 생성
* subnet 은 인터넷 게이트가 연결되지 않아서 완전히 프라이빗
* 인터넷 게이트웨이를 만들고 서브넷은 퍼블릿 서브넷과 프라이빗 서브넷으로 구성

## Elastic Beanstalk

### 의문: 사내환경과 동일하게 aws 에서도 Docker 로 구성이 가능한가?

* ECS: 가장 먼저 검토한 것. ECR 로 관리. 인스턴스의 오토 스케일링과 클러스터 처리를 해줌. 하지만 검토 당시 서울 리전이 없었음.
* Elasitc Beanstalk: 다양한 플랫폼 지원. 톰캣도 지원.
* 사진의 초록색 네모가 environment
* 같은 설정의 다른 환경을 만든다면 설정 파일을 가져와서 다른 환경을 만들 수 있음.
* war 같은 경우 버전 관리도 알아서 해줌.

### Elastic Beanstalk 주의해야 하는 점

* 오토스케일리의 시작 구성
* vpc 설정
* 인스턴스 type 변경
* ami 변경
* ssh key-pair 변경

## 부하테스트

* 사용자 테스트 시점에 50 만이 넘었음.
* 제이미터 사용
* spot instance 로 비용 절감.
* ssm 을 사용해서 run command 로 spot instance 에 명령어를 내림
  * 모든 팀원들이 사용하기에는 불편함이 있었다.
  * 따라서 별도로 제작한 loadtest server 사이트에서 대시보드로 관리
* **cloud watch** 의 로그 기능으로 제어
* **네이버의 오픈소스인 pinpoint** 를 사용 -> **aws 의 x-ray** 사용

## 게임 데이터 활용

* 데이터 계층 구조
  * 스테이지 클리어: id 1000
    * 재화 획득: id 10001, parent id:1000
* 이런 식으로 행위에 대해 id 를 부여

## 데이터 시각화

* **elatic stack** 사용( elastic search 등 )
* **파이프라인: webserver 의 filebeat - logstash - elasticsearch**
* 엘라스틱 노드를 추가하는 상황
  * 한 대의 머신(ec2 나 ecs 를 이야기하는 듯)에서 한계치 측정하는 것으로 테스트
  * 한계치 측정으로 클러스터 추가 상황을 알게 되면 그 때 추가
* 클러스터 장애에 대해서 AWS 로 **elastic search service** 로 처리
* **변경된 파이프라인: amazon kinesis enabled app - kinesis streams - lambda function - elasticsearch**

## 데이터 이중화

* Amazon Kinesis-enabled app -> S3 <- **aws athena** 로 점검
* 로그를 위한 s3 버킷 구조 (사진 참조)
* aws athena 를 통해 cs 처리가 용이해졌음

## 데이터 시각화

* **kibana** 사용
* 과하다 싶을 정도로 로그를 남겼음

## 발표자 스타트업 상황

* 서버 개발자가 3 명이어서 aws 의 도움으로 해결한 문제가 많았다
