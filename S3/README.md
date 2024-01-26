# S3

## 1. S3 버킷 생성 및 설정

#### 1. 버킷명 및 지역 설정
![image](https://github.com/soungjin/aws_study/assets/96867509/22ac8258-340c-4a8f-93c2-5fda657c00bd)

#### 2. 객체 소유권 설정
![image](https://github.com/soungjin/aws_study/assets/96867509/801627f3-6cb5-4b10-a8ae-67306c0f6ddc)
이번 코드에서는 ACL을 사용하지 않을 예정이므로 비활성화한다.

#### 3. 퍼블릭 액세스 차단 설정
![image](https://github.com/soungjin/aws_study/assets/96867509/fca8a0e9-4d4d-401c-a6ca-3bd2b33e7dfa)
S3에 저장되어 있는 이미지나 비디오 파일을 html상에서 url을 통해 바로 띄울 예정이므로 퍼플릭 액세스를 열어놓는다.
나머지 설정들은 기본값으로 설정하여 버킷을 생성한다.

#### 4. 버킷 정책 설정
생성된 버킷의 '권한-버킷 정책'을 편집한다.
![image](https://github.com/soungjin/aws_study/assets/96867509/71de6d72-be1f-4127-8f04-bb70a17d8ca0)
정책 생성기에 다음과 같이 입력을 해준다. Actions는 파일을 받기만 할 예정이므로 GetObject만 선택해준다.
![image](https://github.com/soungjin/aws_study/assets/96867509/a63989f5-be53-4bf8-aefc-f0fb732991f4)
생성된 JSON을 입력해준다. 이 때, Resource에 입력된 arn의 끝에 파일 경로 (여기서는 /*)를 추가로 입력해준다

## 2. Spring Boot 설정

#### 1. build.gradle 설정
build.gradle의 dependencies에 aws 라이브러리를 추가해준다.
```
implementation 'org.springframework.cloud:spring-cloud-starter-aws:2.2.6.RELEASE'
```

#### 2. application.properties 설정
AWS cloudFormation 설정, S3 지역 설정, spring boot 업로드 용량 최대값 설정, properties include 설정을 입력해준다
```
# AWS cloud false
cloud.aws.stack.auto=false

# AWS S3 Service bucket
cloud.aws.region.static=ap-northeast-2

# upload file size limit
spring.servlet.multipart.max-file-size=100MB
spring.servlet.multipart.max-request-size=100MB

#profile
spring.profiles.include = apikey
```
#### 3. application-apikey.properties 설정
AWS IAM access key, 버킷명 및 url을 입력해준다. 해당 값들은 자신의 계정에 해당하는 값을 입력한다.
```
# AWS IAM key
cloud.aws.credentials.accessKey=
cloud.aws.credentials.secretKey=

# AWS S3 Bucket name
cloud.aws.s3.bucket=
```
