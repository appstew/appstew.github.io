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
|S3엔드포인트|http://be-108-appstew.s3-website.ap-northeast-2.amazonaws.com||
|RDS엔드포인트|jdbc:mysql://be-108-appstew.c0nwl8c1futc.ap-northeast-2.rds.amazonaws.com/test||
||||
||||

## 실습 EC2
- 나머지는 코드스테이츠의 컨텐츠를 따라하면 되는데, ec2 가 느리거나 자주 먹통이 되는 현상.
```bash
sudo systemctl status amamzon-ssm-agent
sudo dnf install -y https://s3.amazonaws.com/ec2-downloads-windows/SSMAgent/latest/linux_amd64/amazon-ssm-agent.rpm
sudo systemctl enable amazon-ssm-agent
sudo systemctl start amazon-ssm-agent
sudo systemctl status amamzon-ssm-agent
```
- 그리고 EC2 는 기본적으로 instance start > connet > session manager 순서대로 진행이 되어야 하고 세션 매니저(터미널) 이 멈추거나 해서 부득이 재시작해야할 때에는 instance stop > start > connect sesseion manager 순서대로 진행하여야 한다.
- 그리고 중요한 것은 이 사이사이에 최소 1~2분 이상 걸리니 새로고침을 하면서 느긋하게 진행해야 할 것 같다.

- ec2 세션매니저 에 익숙해졌을 것이다. 그렇다! 너무 많이 들어보고 흔히 생각하는 클라우드 컴퓨팅 하면 생각나는 그게 ec2 에 가장 가깝다! 원격 서버 컴퓨팅.

- 이제 그 다음 단계는 로컬에서 ./gradlew clean build 
bundle exec jekyll serve 

java -jar build/libs/DeployServer-0.0.1-SNAPSHOT.jar

등 로컬에서 빌드 후 localhost:8080 테스트 하던 것과 똑같이 할 수 있다!

다만 좀 느리거나 멈춰서 나는 local 에서 빌드 후 cloudSetting 리포에 올리고 ec2/~ 에 클론하여서 진행했다.

- ec2 에서 

java -jar build/libs/DeployServer-0.0.1-SNAPSHOT.jar

실행 후

http://ec2-54-180-128-249.ap-northeast-2.compute.amazonaws.com:8080/

접속. 잘 된다.

- 이제 vi restart.sh 로 생성 후 다음 복사

```vi
#!/bin/bash

ps -ef | grep "DeployServer-0.0.1-SNAPSHOT.jar" | grep -v grep | awk '{print $2}' | xargs kill -9 2> /dev/null

if [ $? -eq 0 ];then
    echo "my-application Stop Success"
else
    echo "my-application Not Running"
fi

echo "my-application Restart!"
echo $1
nohup java -jar build/libs/DeployServer-0.0.1-SNAPSHOT.jar --spring.profiles.active=dev > /dev/null 2>&1 &
```

- chmod 755 restart.sh
- ./restart/sh
- 마찬가지로 [테스트](http://ec2-54-180-128-249.ap-northeast-2.compute.amazonaws.com:8080/) 잘 되는 것을 알 수 있다.
- 그리고 lsof -i:8080 후 kill 로 끼고 테스트 하면 확실히 안되는 것을 알 수 있고 재실행 후에는 약 10초 후 화면이 뜨는 것을 확인할 수 있다.



## 실습 S3 -클라이언트 배포

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

## 실습 RDS - 데이터베이스 연결



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
```
spring.jpa.database=mysql
spring.jpa.database-platform=org.hibernate.dialect.MySQL5InnoDBDialect
spring.datasource.url=jdbc:mysql://be-108-appstew.c0nwl8c1futc.ap-northeast-2.rds.amazonaws.com:13306/test
spring.datasource.username=admin
spring.datasource.password=lT0NBS4NsQ
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
config.domain=http://be-108-appstew.s3-website.ap-northeast-2.amazonaws.com
```

4. ./gradlew clean 
5. ./gradlew build

## ./gradlew clean build failed 문제 section4/be-sprint-deployment/DeployServer
- 에러 전문
```bash
FAILURE: Build failed with an exception.

* Where:
Settings file '/javatest/hrd/intelliJ_projects/section4/cloudSetting/be-sprint-deployment/DeployServer/settings.gradle'

* What went wrong:
Could not compile settings file '/javatest/hrd/intelliJ_projects/section4/cloudSetting/be-sprint-deployment/DeployServer/settings.gradle'.
> startup failed:
  General error during conversion: Unsupported class file major version 61
  
  java.lang.IllegalArgumentException: Unsupported class file major version 61
        at groovyjarjarasm.asm.ClassReader.<init>(ClassReader.java:189)
        at groovyjarjarasm.asm.ClassReader.<init>(ClassReader.java:170)
        at groovyjarjarasm.asm.ClassReader.<init>(ClassReader.java:156)
        at groovyjarjarasm.asm.ClassReader.<init>(ClassReader.java:277)
        at org.codehaus.groovy.ast.decompiled.AsmDecompiler.parseClass(AsmDecompiler.java:81)
        at org.codehaus.groovy.control.ClassNodeResolver.findDecompiled(ClassNodeResolver.java:251)
        at org.codehaus.groovy.control.ClassNodeResolver.tryAsLoaderClassOrScript(ClassNodeResolver.java:189)
        at org.codehaus.groovy.control.ClassNodeResolver.findClassNode(ClassNodeResolver.java:169)
        at org.codehaus.groovy.control.ClassNodeResolver.resolveName(ClassNodeResolver.java:125)
        at org.codehaus.groovy.ast.decompiled.AsmReferenceResolver.resolveClassNullable(AsmReferenceResolver.java:57)
        at org.codehaus.groovy.ast.decompiled.AsmReferenceResolver.resolveClass(AsmReferenceResolver.java:44)
        at org.codehaus.groovy.ast.decompiled.AsmReferenceResolver.resolveNonArrayType(AsmReferenceResolver.java:79)
        at org.codehaus.groovy.ast.decompiled.AsmReferenceResolver.resolveType(AsmReferenceResolver.java:70)
        at org.codehaus.groovy.ast.decompiled.MemberSignatureParser.createMethodNode(MemberSignatureParser.java:57)
        at org.codehaus.groovy.ast.decompiled.DecompiledClassNode.lambda$createMethodNode$1(DecompiledClassNode.java:230)
        at org.codehaus.groovy.ast.decompiled.DecompiledClassNode.createMethodNode(DecompiledClassNode.java:236)
        at org.codehaus.groovy.ast.decompiled.DecompiledClassNode.lazyInitMembers(DecompiledClassNode.java:203)
        at org.codehaus.groovy.ast.decompiled.DecompiledClassNode.getDeclaredMethods(DecompiledClassNode.java:122)
        at org.codehaus.groovy.ast.ClassNode.tryFindPossibleMethod(ClassNode.java:1283)
        at org.codehaus.groovy.control.StaticImportVisitor.transformMethodCallExpression(StaticImportVisitor.java:251)
        at org.codehaus.groovy.control.StaticImportVisitor.transform(StaticImportVisitor.java:133)
        at org.codehaus.groovy.ast.ClassCodeExpressionTransformer.visitExpressionStatement(ClassCodeExpressionTransformer.java:108)
        at org.codehaus.groovy.ast.stmt.ExpressionStatement.visit(ExpressionStatement.java:40)
        at org.codehaus.groovy.ast.ClassCodeVisitorSupport.visitClassCodeContainer(ClassCodeVisitorSupport.java:138)
        at org.codehaus.groovy.ast.ClassCodeVisitorSupport.visitConstructorOrMethod(ClassCodeVisitorSupport.java:111)
        at org.codehaus.groovy.ast.ClassCodeExpressionTransformer.visitConstructorOrMethod(ClassCodeExpressionTransformer.java:66)
        at org.codehaus.groovy.control.StaticImportVisitor.visitConstructorOrMethod(StaticImportVisitor.java:108)
        at org.codehaus.groovy.ast.ClassCodeVisitorSupport.visitConstructor(ClassCodeVisitorSupport.java:101)
        at org.codehaus.groovy.ast.ClassNode.visitContents(ClassNode.java:1089)
        at org.codehaus.groovy.ast.ClassCodeVisitorSupport.visitClass(ClassCodeVisitorSupport.java:52)
        at org.codehaus.groovy.control.CompilationUnit.lambda$addPhaseOperations$3(CompilationUnit.java:209)
        at org.codehaus.groovy.control.CompilationUnit$IPrimaryClassNodeOperation.doPhaseOperation(CompilationUnit.java:942)
        at org.codehaus.groovy.control.CompilationUnit.processPhaseOperations(CompilationUnit.java:671)
        at org.codehaus.groovy.control.CompilationUnit.compile(CompilationUnit.java:635)
        at groovy.lang.GroovyClassLoader.doParseClass(GroovyClassLoader.java:389)
        at groovy.lang.GroovyClassLoader.lambda$parseClass$3(GroovyClassLoader.java:332)
        at org.codehaus.groovy.runtime.memoize.StampedCommonCache.compute(StampedCommonCache.java:163)
        at org.codehaus.groovy.runtime.memoize.StampedCommonCache.getAndPut(StampedCommonCache.java:154)
        at groovy.lang.GroovyClassLoader.parseClass(GroovyClassLoader.java:330)
        at org.gradle.groovy.scripts.internal.DefaultScriptCompilationHandler.compileScript(DefaultScriptCompilationHandler.java:139)
        at org.gradle.groovy.scripts.internal.DefaultScriptCompilationHandler.compileToDir(DefaultScriptCompilationHandler.java:95)
        at org.gradle.groovy.scripts.internal.BuildOperationBackedScriptCompilationHandler$2.run(BuildOperationBackedScriptCompilationHandler.java:54)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$1.execute(DefaultBuildOperationRunner.java:29)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$1.execute(DefaultBuildOperationRunner.java:26)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$3.execute(DefaultBuildOperationRunner.java:75)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$3.execute(DefaultBuildOperationRunner.java:68)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.execute(DefaultBuildOperationRunner.java:153)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.execute(DefaultBuildOperationRunner.java:68)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.run(DefaultBuildOperationRunner.java:56)
        at org.gradle.internal.operations.DefaultBuildOperationExecutor.lambda$run$1(DefaultBuildOperationExecutor.java:74)
        at org.gradle.internal.operations.UnmanagedBuildOperationWrapper.runWithUnmanagedSupport(UnmanagedBuildOperationWrapper.java:45)
  ...
  1 error


* Try:
Run with --stacktrace option to get the stack trace. Run with --info or --debug option to get more log output. Run with --scan to get full insights.

* Get more help at https://help.gradle.org

BUILD FAILED in 498ms
```
- 터미널 명령도 실패하고, intelliJ 에서도 gradle 프로젝트로 인식조차 안되었다. 혹시 몰라 jbr17.0.3 을 다른 걸로 바꿔보고 인텔리제이 제안에서 하라는대로 openJDK 로 프로젝트 java 변경 후 새로고침하니 gradle로 인식하면서 
```
Shared indexes for maven library "org.springframework.boot:spring-boot:2.5.4" are downloaded (71.25 MB in 6 sec, 563 ms)
```
메시지와 함께 gradle 라이브러리를 다운받는 것이 목격되었다. 이후 다른 java 로 변경해도 gradlew build 가 정상적으로 되는 것 확인.


||||||
|---|---|---|---|---|
||On-ste|Iaas|Paas|SaaS|
||onPremise|infrastructure as a Service|Platform as a Service|software as a Service|
|ex||AWS EC2 </br>GCE </br>Azure WMS|vercel|Ndrive oneDrive, mail...|
||||||
||||||
||||||

오늘 세가지 실습은 개인이 구성하면 얼마정도 해요?

||||
|---|---|---|
||클라우드|온프레미스|
|비용|유지비용(사용한만큼)|초기비용+유지비용|
|확장성|유리|불리|
|구축에 걸리는 시간|몇초 몇분~|좀 걸림|
||||
||||

안녕하세요~

[황정식님 깃헙](https://github.com/ITVillage-Kevin/rxjava )

||||
|---|---|---|
||||
||||
||||
||||
||||
||||

## 221004 17:00 선배적 참견시점
``````````````````````````````````````````````````                      ``````````````````````````````````````````````````
- Shawn Han 선배님. 

 