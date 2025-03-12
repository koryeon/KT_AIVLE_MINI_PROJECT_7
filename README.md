# KT_AIVLE_MINI_PROJECT_7

# 응급상황 인식 및 응급실 연계 서비스 포탈

## 프로젝트 개요

### 주제
응급상황 인식 및 응급실 연계 서비스 포탈

### 사전학습과목
데이터 처리, API, 언어모델 파인튜닝, Java, Spring, Web

### 데이터
- **출처**: 자체 제작
- **구분**: Text, 음성
- **문제 유형**: Classification, Recommendation, Web Service

### 중점사항
6차 미니 프로젝트 결과물 고도화

## 🔄 진행 절차

### Step 1 (1~3일차) - 개인 과제
- **진행 목표**: 기본 기능을 개인별로 직접 구현
- **추가교육**: 
  - 응급실 API, FastAPI로 구현
  - Azure 웹 서버 세팅
  - 웹 개발, Spring Boot
  - 조별 튜터링
- **사용기술**: 개인 결과물 제출(소스코드)
- **실습 도구**: Jupyter Notebook, VS Code

### Step 2 (4~6일차) - 조 과제
- **진행 목표**: 조별 추가 기능을 함께 구현하며 완성도를 높임
- **프로젝트**: 조 과제(기본 + 추가 요구사항)
- **사용기술**: 팀 결과물 제출(소스코드, URL, 결과보고서)
- **실습 도구**: Jupyter Notebook, VS Code, IntelliJ, Docker Desktop, MS Azure
<img width="633" alt="Image" src="https://github.com/user-attachments/assets/168b4344-a930-4d62-9aaa-2f2d631fc423" />

##  일자별 실습 목표

| 일자 | 실습 목표 | 실습 도구 |
|------|-----------|-----------|
| 1일차 | 오전 - 모듈화, 파인튜닝 모델 테스트<br>오후 - 관리 DB 작성 | Jupyter Notebook, VS Code |
| 2일차 | FastAPI를 사용하여 응급실 추천의 API화 (RestAPI 작성) | Jupyter Notebook, VS Code |
| 3일차 | 1) 2일차에 작성한 FastAPI(Dockerfile제공)<br>2) 제공된 Spring Boot 소스<br>위 두 가지 소스를 활용해서 Azure에 Docker 배포 | VS Code, IntelliJ, Docker Desktop, MS Azure |
| 4일차 | 웹 페이지 개발 및 고도화<br>역할분담, 조별과제 | Jupyter Notebook, VS Code, IntelliJ, Docker Desktop, MS Azure |
| 5일차 | 웹 페이지 개발 및 고도화<br>조별과제 | Jupyter Notebook, VS Code, IntelliJ, Docker Desktop, MS Azure |
| 6일차 | 오전 - 조별 과제, 조별 과제 제출<br>오후 - 조별 프로젝트 결과 발표, 셀프 테스트 | Jupyter Notebook, VS Code, IntelliJ, Docker Desktop, MS Azure |

## 시스템 구성도

### 구현할 시스템 구성

<img width="823" alt="Image" src="https://github.com/user-attachments/assets/c2b49c28-bc0e-485f-abca-c43c62439342" />

### 구성 요소

#### 1. 사용자 입력
- 사용자는 브라우저를 통해 시스템에 음성 메시지와 위치 정보를 입력
- 입력된 메시지는 "다쳤어요!"와 같은 응급 상황을 포함하며, 위치 정보는 응급실 추천을 위한 필수 데이터

#### 2. 프론트엔드
- **구성**: View Template Engine 기반으로 구현
- **프레임워크**: Spring Boot 사용
- **기능**:
  - 사용자로부터 음성 및 위치 데이터를 수집
  - 백엔드와 통신하여 응급실 추천 결과를 표시
- **배포**: Docker를 사용하여 컨테이너화

#### 3. 백엔드
- **구성**: Spring Boot와 FastAPI로 나누어진 마이크로서비스 구조
- **Spring Boot (Java)**:
  - 프론트엔드와 통신하는 역할
  - 사용자의 요청을 Python 기반 FastAPI 서비스로 전달
  - 추천된 응급실 데이터를 프론트엔드로 반환
  - 그 외 각종 추가기능 backend 요소
- **FastAPI (Python)**:
  - REST API를 통해 음성 인식, 텍스트 요약 및 분류 처리
  - AI 모델 (BERT, ChatGPT, Whisper) 활용

## 요구사항 및 목표

### 목표
- 응급 요청에 적합한 응급실 연계 서비스 포털 구축하기
- 지금까지 배운 기술들을 하나로 엮은 시스템 구축

### 활용 기술
- **AI모델**: LLM, 언어모델 파인튜닝
- **API**: OpenAI, Naver Maps
- **H/W**: 클라우드 웹 서버
- **DB**: JPA, SQLite3(향후 다양한 DBMS연동)
- **S/W**: Spring Boot, FastAPI

### 구현 범위
### ① 로컬 환경 모델 테스트 및 관리 DB 준비
-  로컬 가상환경 생성
  - VS Code의 터미널을 이용해서 가상환경을 만들고 필요한 라이브러리 설치
- 로컬 환경에서 응급 연계 모델 통합 테스트
  - 미프 6차에서 구축한 응급 연계 모델에 대해서, 로컬 환경에서 통합테스트 수행
-  관리용 DB 구축
  - SQLite3 DB를 생성하고, 관리용 정보를 기록할 테이블 구조 정의
  - 입력(요청) 및 최종 결과를 테이블에 입력하는 함수 생성 및 기존 모듈 수정
  - 저장할 내용: 입력시간, 좌표, 변환(STT) 된 text, 연계된 병원 3 곳 정보 등
-  관리용 정보 추가 도출 및 테이블 구성
  - 기본 기록 용 테이블 외에 추가로 관리가 필요한 정보를 정의하고 테이블 구성
  - 추가 정보 입력을 위한 코드 수정

### ② 응급실 데이터의 API화
-  REST API 작성
  - 응급실 목록을 추천하는 API를 FastAPI를 사용하여 구현
  - 음성, 위치가 request로 들어오면 응급실 추천 목록을 response로 응답
  - Json 형태로 제공
-  응급실 목록
  - 응급실 3개 추천 -> 동적 개수 추천으로 업그레이드
  - Bert fine tuning 통한 성능 개선

### ③ 응급실 추천 구현
-  응급실 추천
  - FastAPI로 만든 REST API 호출 하여 응답
  - Spring Boot에서 FeignClient등을 사용하여 REST API 호출
  - 사용자 요청(증상,위치) 후 추천 응급실을 보여준다.
-  화면 꾸미기
  - CSS 사용하여 간단하게 꾸미기

### ④ 배포
-  배포
  - MS Azure / Docker 사용

## 팀 과제 요구사항

### ① 응급실 목록 추천
-  응급실 추천 (Spring Boot 사용)
  - 응급실 3개가 아닌 동적 갯수를 변수로 받게 변경
  - 사용자 요청(증상,위치) 후 추천
-  포털 형식 제작 (Spring Boot 사용)
  - 홈페이지/포털의 형태가 되게 만들기
  - 응급실을 가는 경로 네비게이션 형태로 보여주기
  - 로그인/ 게시판(파일 업로드) 기능 등
  - 조별로 아이디어를 만들어 각종 추가 기능 제공

### ② 사용자 화면
-  사용자 화면
  - 반응형 사이트 (PC, 모바일)
  - 음성과 위치를 받아서 추천응급실을 보여주게 구현
-  사용자 화면
  - 홈페이지/포털의 형태가 되게 만들기
  - 응급실 가는 경로 네비게이션 형태로 보여주기

### ③ 관리자 페이지
-  관리자 화면 (Spring Boot 사용)
  - 응급상황 요청 이력 조회
    - 전체 이력 표 형태로 조회
    - 조회 조건: 기간
    - 안내된 병원
  - 대시보드 구성, 예상이동시간, 실제이동시간 기록
    - 대시보드 구성
    - 응급실 추천 경로 중 예상이동시간 기록
    - 실제 이동시간 기록: 관리자가 작성할 수 있게 하고 실제라고 생각하고 저장
    - 예상시간과 실제 시간을 대시보드로 표현

### ④ 웹 서버
-  웹 서버
  - Docker 사용
  - 웹서버에 SQLite3 DB 저장
  - 간단한 방화벽 설정 등으로 IP를 통해서 사이트를 전 세계에 공개
  - Microsoft Azure 사용
