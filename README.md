# 이단규

> - 한국외대 재학 중('21.03~)
> - 멋쟁이사자처럼(13기) 수료('25.03~'26.01)
> - 멋쟁이사자처럼(14기) 운영진('26.02~08)
> - BDAI 운영진(8기) 개발팀('26.02~08)

---

## 🛠 Tech Stack

**Languages**

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Java](https://img.shields.io/badge/Java-007396?style=for-the-badge&logo=openjdk&logoColor=white)
![Kotlin](https://img.shields.io/badge/Kotlin-7F52FF?style=for-the-badge&logo=kotlin&logoColor=white)

**Frameworks**

![Django](https://img.shields.io/badge/Django-092E20?style=for-the-badge&logo=django&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-6DB33F?style=for-the-badge&logo=springboot&logoColor=white)

**Database**

![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white)

**DevOps**

![AWS](https://img.shields.io/badge/AWS-232F3E?style=for-the-badge&logo=amazonwebservices&logoColor=white)
![Terraform](https://img.shields.io/badge/Terraform-7B42BC?style=for-the-badge&logo=terraform&logoColor=white)

---

## 🚀 Projects

### PETFORM
https://github.com/dangyulee/petform

- 기간: 2026.07 ~ 2026.08 (1개월)
- 소개: 반려동물 사진 한 장으로 3D 피규어 모델(STL) 생성부터 프린트샵 견적 비교까지 잇는 AI 3D 프린팅 서비스
- 성과: 멋쟁이사자처럼 대학 14기 중앙해커톤 입상 (상위 20%)
- 팀 구성: 5명(기획 1, 디자인 1, 프론트엔드 2, 백엔드 1)
- 기술: `Spring Boot 3.5.16` `Kotlin 2.2.0` `Java 21` `JPA` `MySQL` `S3` `CloudFront` `SQS`
- 아키텍처: `Client` → `Spring Boot` → `SQS FIFO` → `AI 서버 (RTX 4060)` → `S3 / CloudFront` → `Callback`
   <details>
   <summary>아키텍처 다이어그램</summary>

   <img src="https://raw.githubusercontent.com/dangyulee/petform/main/docs/architecture.png" width="700">
   </details>
- 담당:
   - 백엔드·AI 서버 단독 개발 (API 설계 · 데이터 모델링 · 인프라 · 배포)
   - **백엔드**
      - Creation 중심 계층형 REST API 설계
      - 생성 작업(Creation)과 3D 생성 시도(Job)를 1:N으로 분리 설계해 실패·재시도 이력 보존
      - SQS FIFO 기반 3D 모델 생성 비동기 잡 파이프라인 설계 (GPU 1대 환경에서 순차 처리 보장, jobId 중복 제거)
      - Presigned URL 업로드 · CloudFront 조회로 파일 트래픽을 애플리케이션 서버에서 분리
   - **AI 서버**
      - 로컬 GPU(RTX 4060, VRAM 8GB) 환경에서 TripoSG 기반 image → 3D(STL) 생성 워커 구축
      - SQS long polling으로 작업 소비 후 S3 업로드 · 백엔드 콜백
- **트러블슈팅**
   - [부스 운영 데이터와 외부 API 호출 실패](https://velog.io/@kikoky/비동기-처리와-부스-운영-데이터)
   - 이미지 변환 API 502 67건 → JPEG 세그먼트를 분석해, iOS HDR 사진의 게인맵(APP2)이 원인임을 규명 -> 클라이언트 재인코딩으로 해결 검증
   - 피크 시 대기 최대 15분 → 운영 로그로 도착률·처리율(이용률 81%, 피크 123%)을 분석해 병목을 수치화 -> 큐 대기 순번·예상 시간 노출
      
### BDAI-PICK

- 기간: 2026.06 ~ 2026.07 (4주)
- 소개: **BDAI 학회원 - 가게 제휴 서비스**
- 팀 구성: 6명(디자인 1, 프론트엔드 2, 백엔드 3)
- 기술: `Spring Boot 3.5.14` `Kotlin 2.3.21` `JPA` `MySQL` `Terraform`
- 아키텍처: `Hexagonal Architecture` | `Muti-module`
- 담당:
    - 기획 및 백엔드
    - Member 모듈 담당
        - 제휴 리스트 노출
        - QueryDSL, 페이지네이션 적용   
    - AI 기반 오류 대응 체제 구축
        - CloudWatch → SNS → SQS → Claude Code → Slack

### 대학생보호구역(DBGzone)

https://github.com/campus-local-app

- 기간: 2026.05 ~ 2026.07 (2개월)
- 소개: **학생회 제휴 활성화를 통한 대학 상권 내 가게 홍보 효율 극대화**
- 팀 구성: 7명(기획 1, 디자인 1, 프론트엔드 2, 백엔드 3)
- 기술: `Spring Boot 3.5.11` `Java 21` `JPA` `MySQL` `Redis`
- 아키텍처: `Layered Architecture`
- 담당:
    - 대표 겸 서비스 기획, 백엔드
    - 유저 인터뷰 및 시장 조사
    - 학생회 및 가게 섭외
    - 스프린트 별 기획 문서 작성
    - QA
    - 비용 절감을 위한 개발용 로컬 서버 구축 및 CICD 설계
    - 코드 리팩토링 및 컨벤션 정리
    - 테스트 코드 작성
 
---
[![Gmail](https://img.shields.io/badge/dg200101@gmail.com-EA4335?style=flat&logo=gmail&logoColor=white)](mailto:dg200101@gmail.com)
