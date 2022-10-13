---
---

- 챕터 시작 전, 내 노트북 네트워크 안에서 localhost:8080 localhost:8082 두 포트에서 자꾸 김코딩 로그인 창이 뜨는 것을 확인하였는데
aws S3 의 index.html 과 같았으나 이것인지는 확실하지 않고, docker desktop 내의 컨테이너는 모두 삭제한 상태였다. 나중에 다시 확인 및 해결..
s3 버킷 삭제에도 여전. var/www/ 아님 

## 실습 시작 후
-ssm-user@ip-172-31-10-86:/var/snap/amazon-ssm-agent/5656$ sudo ./aws/install
You can now run: /usr/local/bin/aws --version

## 실습 - AWS Pipeline 을 통한 배포 자동화

.env 폴더 내 및 postman, 브라우저에서 확인해야하는 정확한 주소는 http://ec2-54-180-128-249.ap-northeast-2.compute.amazonaws.com:8080 이다!!

hello spring world 잘 출력된다.

- 배포 자동화 - pipeline
    - code - github repo
    - build - codeBuild
    - deploy - codeDeploy


## 실습 - 환경 변수 설정

- 실습 내용
    - AWS CodeBuild 를 통해 환경 변수를 전달 
    - AWS Parameter Store, AWS CLI 를 통해 환경 변수를 전달
- 성공시 S3버킷 엔드포인트 주소 예상:
    - 로그인에 성공했습니다, 토큰을 정상적으로 받았습니다.
- 추가 내용
    - 이 실습엔 별도의 클라이언트를 구성하지 않았고, 이전 실습의 s3 클라이언트 배포 과정을 활용해 클라이언트와 연결할 수 있다.



## 실습 - github actions

- S3 CodeDeploy EC2



