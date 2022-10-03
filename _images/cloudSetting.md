---
---

![](../img/cloudSetting.excalidraw.svg)

220930 금요일 클라우드챕터 aws 세팅q

코테에서 수강생마다 학습용 aws 계정를 만들어준다. 5일가량만 유효.
동의서 작성. 후 메일로.
그리고 이 계정은 앞에 section4 중 [cloud]가 앞에 있는, 4가지 챕터후에 만료된다.
계정명은 각자의 db 인덱스명+~~+깃헙ID 식으로 생성될 것이다. 
대략 be-0-SEYUN 이런 식 

[](https://mail.google.com/mail/u/0/#inbox/FMfcgzGqQmQvdfNzzmzMzXzLdvBDjlrW)

||||
|---|---|---|
|메일 링크|https://mail.google.com/mail/u/0/#inbox/FMfcgzGqQmQvdfNzzmzMzXzLdvBDjlrW||
|aws로그인 링크|https://event.stibee.com/v2/click/MTk3NTEwLzEyMDY4MjQvMzkzLw/aHR0cHM6Ly8xNDYxNDE4Nzc1MjYuc2lnbmluLmF3cy5hbWF6b24uY29tL2NvbnNvbGU||
|aws 사용자 이름|be-student-108-appstew||
|리소스 이름|be-108-appstew||
|AWS password|메일 내||
|DB password|메일 내||
||||
||||
||||
||||

## 실습 -클라이언트 배포

- 현재 section4/be-sprint-deployment/client 는 JS, React 로 구성되었다.
- 정적 웹사이트 호스팅
    - 단계 : 빌드>버킷생성 및 웹사이트 호스팅 용으로 구성>빌드된 페이지 업로드>퍼플릭액세스 차단 해제 및 정책 생성
1. nvm --version
2. node -v
3. be-sprint-deployment/client/ 안에서 npm install
4. .env // REACT_APP_API_URL=http://ec2-13-209-47-34.ap-northeast-2.compute.amazonaws.com:8080/ 로 수정
5. npm run build // compiled successfully.
6. aws/S3/be-108-appstew/ enable static website hosting // index.html 등 설정 후
7. bucket website endpoint(http://be-108-appstew.s3-website.ap-northeast-2.amazonaws.com/) 클릭
8. upload built files
9. bucket policy generator // S3 bucket Policy //  actions:getObject // ARN arn:aws:s3:::be-108-appstew/*
//     *

	Allow	

    s3:GetObject

	arn:aws:s3:::be-108-appstew/*	None
// generatate policy>json 데이터를 복사 후 json 으로 정책 생성

10. http://be-108-appstew.s3-website.ap-northeast-2.amazonaws.com/login 확인 




=====

## 실습 - 데이터베이스 연결

1. RDS 접속
```sh
mysql -u admin --host be-108-appstew.c0nwl8c1futc.ap-northeast-2.rds.amazonaws.com -P 13306 -p
// --host 이후는 RDS 의 endpoint 이다.
```
2. show databases;

3. be-sprint-deployment/DeployServer/src/amin/resources/apllication.properties 수정
```
spring.jpa.database=mysql
spring.jpa.database-platform=org.hibernate.dialect.MySQL5InnoDBDialect
spring.datasource.url=jdbc:mysql://{AWS RDS Endpoint}/test?useSSL=false&characterEncoding=UTF-8&serverTimezone=UTC
spring.datasource.username={RDS Mysql Admin id}
spring.datasource.password={RDS Mysql Admin password}
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
config.domain={AWS S3 Endpoint}
```

4. ./gradlew clean 
5. ./gradlew build

||||
|---|---|---|
||||
||||

[황정식님 깃헙](https://github.com/ITVillage-Kevin/rxjava )
