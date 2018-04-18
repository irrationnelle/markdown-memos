# github 과 lambda 로 서버리스 환경 구성해서 테스트, 빌드, 배포까지

## **AWS CodeStart**

### 아키텍쳐

* github 에서 변경이 있거나, aws 의 람다에서 변경이 있으면 CodeStart 에서 notice

### 사용방법

* 먼저 IAM 에서 새로운 유저를 추가해야함
* AWS Management Console Access 를 접근할 수 있게 체크해야함
* User must create a new password at next login 는 체크 표시를 해제
* AWSLambdaFullAccess, S3FullAccess, CodeStartFullAccess 에 대한 Role 을 추가해야함
