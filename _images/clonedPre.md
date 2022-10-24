---
---

- preProject/clonePre 에서 preProject mainProject 대비 혼자 연습
- preProject 는 스택오버플로우 클론

## 메모 (미정리)


1. aws 가입 및 루트계정 세팅

- 지메일 계정을 루트 계정으로 가입하였고 12month free tier 221023 가입.

- 요금 및 iam 은 중요하므로 잘 설정하고 기억하자!
- google auth 설정. pem 과 시크릿키 등은 certificate/AWS 폴더에 저장
- ec2.micro 우분투 생성 후 elasticIP 연결.
- 실수로 중요한 부분을 놓치지 않기 위해 https://webnautes.tistory.com/1480 의 글을 참고하였다.
- 

- 이후 ssh -i $(echo $aws1) 로 접속 가능하도록 ~/.zshrc 에 설정

2. IAM 역할 생성

- IAM>역할 에서 역할 생성.
- 코드스테이츠 챕터에 따라 5가지 권한 생성 후 다음
- 신뢰 정책 편집 수정
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "sts:AssumeRole"
            ],
            "Principal": {
                "Service": [
                    "ec2.amazonaws.com"
                ]
            }
        }
    ]
}
```
```
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Effect": "Allow",
			"Principal": {
				"Service": ["ec2.amazonaws.com", "codedeploy.ap-northeast-2.amazonaws.com"]
			},
			"Action": "sts:AssumeRole"
		}
	]
}
```

3. IAM 유저 생성

- EC2 에 IAM 역할을 부여하고
- seb40_pre_018 및 연습용으로 (같은이름)/(같은이름+팀이름cameCase) 로 IAM ID/PW 생성하였다. 이메일 보냄



