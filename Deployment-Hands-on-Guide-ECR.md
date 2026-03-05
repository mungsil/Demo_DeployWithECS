# ECR 실습

Docker 이미지를 빌드한 뒤 **Amazon ECR에 업로드하고 ECS에서 사용하기 위한 기본 실습**입니다.

## Table of Contents

- [Prerequisites](#prerequisites)
- [ECR 실습](#ecr-실습)
- [다음으로](#다음으로)
---

# Prerequisites

다음 조건이 준비되어 있어야 합니다.

* AWS CLI 설치
* Docker 설치
* `AdministratorAccess` 권한이 있는 IAM User의 **Access Key가 로컬 AWS CLI에 설정**
---

# ECR 실습

## Step 1. Docker Image Build

Dockerfile을 이용해 이미지를 빌드합니다.

```bash
docker build -t test .
```

---

## Step 2. ECR Login

ECR 레지스트리에 로그인합니다.

```bash
aws ecr get-login-password \
--region ap-northeast-2 \
| docker login \
--username AWS \
--password-stdin ACCOUNT_ID.dkr.ecr.ap-northeast-2.amazonaws.com
```

---

## Step 3. Docker Image Tagging

로컬 이미지를 **ECR repository 주소로 태깅**합니다.

```bash
docker tag test:latest ACCOUNT_ID.dkr.ecr.ap-northeast-2.amazonaws.com/test:latest
```

---

## Step 4. Image Push to ECR

태깅한 이미지를 ECR에 업로드합니다.

```bash
docker push ACCOUNT_ID.dkr.ecr.ap-northeast-2.amazonaws.com/test:latest
```

---

## 참고 자료

* YouTube Tutorial
  [https://www.youtube.com/watch?v=zs3tyVgiBQQ](https://www.youtube.com/watch?v=zs3tyVgiBQQ)

---

## 추가 설명

### Docker Tagging이 필요한 이유

Docker는 이미지를 **레지스트리 주소 기반으로 업로드**합니다.

즉 다음 형식이어야 push가 가능합니다.

```
[registry]/[repository]:[tag]
```

ECR 예시

```
101645635368.dkr.ecr.ap-northeast-2.amazonaws.com/test:latest
```

그래서 **로컬 이미지 → ECR 주소로 태깅** 과정이 필요합니다.

## 다음으로
[ECS 실습](Deployment-Hands-on-Guide-ECS.md)
