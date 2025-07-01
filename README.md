# 📚 KT 걷다가서재 - AI 기반 자동 출간 및 구독 플랫폼

> 클라우드 네이티브 기반 전자책 자동 출간 및 구독 플랫폼  
> Spring Boot + React + Azure + Kafka 기반 마이크로서비스 프로젝트

---

## 🛠️ 프로젝트 개요

- 작가가 글을 작성하면 AI가 자동으로 표지 이미지를 생성하고 전자책으로 출간
- 구독자는 월정액으로 책을 열람하고, KT 고객은 포인트 혜택을 받을 수 있음
- 3회 이상 열람된 도서는 '베스트셀러'로 분류되어 추가 노출
- 실습 목표: 클라우드 네이티브 앱 개발 및 MSA 아키텍처 경험

---

## 📆 개발 기간

- **2025.06.25 (수) ~ 2025.07.04 (금)** / 총 8일

---

## 👥 팀원 (AI_04반_11조)

| 이름   | 역할             |담당 파트
|--------|------------------|------------------|
| 이헌준 | 조장              | (작성필요) |
| 김시훈 | 발표자 | AI 출간 자동화 담당 |
| 안도형 | PPT | 구독자 관리 |
| 박수연 | PPT | 서재 플랫폼 |
| 오현종 | 검토 | 집필 관리  |
| 양성현 | 검토 | 포인트 관리 |
| 김민서 | 검토 | 작가 관리  |
| 류근우 | 서기              | (작성필요) |

---

## 🗂️ 주요 일정 및 작업

- **1일차 (06.25)**: OT, 도메인 이해, 역할 분담, User Story, Event Storming
- **2일차 (06.26)**: 전략/전술 설계, 헥사고날 다이어그램
- **3일차 (06.27)**: 마이크로서비스 구현 시작 (Event 기반)
- **4일차 (06.30)**: Kafka 메시징, CQRS, 테스트 작성
- **5일차 (07.01)**: 프론트엔드 구현, Docker 이미지 생성 및 Push
- **6일차 (07.02)**: Azure 배포, 오케스트레이션(HPA, 무정지 배포)
- **7일차 (07.03)**: 서비스 메시 적용, 모니터링 & 로깅
- **8일차 (07.04)**: 배포 파이프라인 설계, Wrap-up, 발표

---

<br><br>

# 실습 방법

## Model
www.msaez.io/#/59328372/storming/93e55621aef16e5cfc7076f172bcdb3as

## Before Running Services
### Make sure there is a Kafka server running
```
cd kafka
docker-compose up
```
- Check the Kafka messages:
```
cd infra
docker-compose exec -it kafka /bin/bash
cd /bin
./kafka-console-consumer --bootstrap-server localhost:9092 --topic
```

## Run the backend micro-services
See the README.md files inside the each microservices directory:

- authormanage
- writemanage
- ai
- point
- libraryplatform
- subscribemanage
- outside


## Run API Gateway (Spring Gateway)
```
cd gateway
mvn spring-boot:run
```

## Test by API
- authormanage
```
 http :8088/authors authorId="authorId"name="name"loginId="loginId"password="password"isApproved="isApproved"portfolioUrl="portfolioUrl"
```
- writemanage
```
 http :8088/writings bookId="bookId"title="title"context="context"authorId="authorId"registration="registration"
```
- ai
```
 http :8088/coverDesigns id="id"updatedAt="updatedAt"title="title"imageUrl="imageUrl"generatedBy="generatedBy"createdAt="createdAt"bookId="bookId"
 http :8088/contentAnalyzers id="id"bookId="bookId"language="Language"maxLength="maxLength"classificationType="classificationType"requestedBy="requestedBy"
```
- point
```
 http :8088/points pointId="pointId"userId="userId"pointBalance="pointBalance"standardSignupPoint="standardSignupPoint"ktSignupPoint="ktSignupPoint"amount="amount"usedAt="usedAt"
```
- libraryplatform
```
 http :8088/libraryInfos bookId="bookId"bookTitle="bookTitle"bestseller="bestseller"author="author"selectCount="selectCount"publishDate="publishDate"summary="summary"classficationTpe="classficationTpe"bookimage="bookimage"
```
- subscribemanage
```
 http :8088/subscribers id="id"name="name"isMonthlySubscribed="isMonthlySubscribed"isKt="isKt"
 http :8088/subscribedBooks subscribedBookId="subscribedBookId"status="status"bookId="bookId"
```
- outside
```
```


## Run the frontend
```
cd frontend
npm i
npm run serve
```

## Test by UI
Open a browser to localhost:8088

## Required Utilities

- httpie (alternative for curl / POSTMAN) and network utils
```
sudo apt-get update
sudo apt-get install net-tools
sudo apt install iputils-ping
pip install httpie
```

- kubernetes utilities (kubectl)
```
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```

- aws cli (aws)
```
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

- eksctl 
```
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
sudo mv /tmp/eksctl /usr/local/bin
```
