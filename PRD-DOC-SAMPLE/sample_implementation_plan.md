Update this rule if user requested changes to the project requirement, etc.

# Implementation Plan

## Phase 1: Environment Setup

1. **Prevalidation**  
   - 기존 프로젝트 구조(`/admission-ui`, `/admission-api`, `/common-utils`)가 존재하는지 확인합니다.

2. **Repository Directories Creation**  
   - `/admission-ui`: 원서 접수 및 입학처 직원 UI 관리  
   - `/admission-api`: 접수 및 평가 관련 백엔드 API  
   - `/common-utils`: 공통 기능 유틸 (파일 업로드, 인증 등)

3. **Frontend Tools Setup**  
   - Node.js 및 npm 설치 (`node -v`, `npm -v`)  
   - CRA + TypeScript 기반 UI 설정

4. **Backend Tools Setup**  
   - JDK 21 이상, Spring Boot 기반  
   - Gradle 사용, `gradle -v`로 확인

5. **Database Setup**  
   - PostgreSQL 설치 및 `psql --version` 확인  
   - ERD에 따른 초기 스키마 구성

6. **CI/CD & Container Tools**  
   - Docker 설치 확인, GitHub Actions 템플릿 준비

## Phase 2: Frontend Development (admission-ui)

1. **지원서 접수 데이터 점검 UI (`REQ-001`)**  
   - `/admission-ui/src/pages/DataCorrection.tsx`  
   - 비정상 접수 데이터에 대한 필터링 및 수정 인터페이스 제공

2. **지원서 출력 화면 (`REQ-002`)**  
   - `/admission-ui/src/pages/ApplicationPrint.tsx`  
   - 프린터 프렌들리 PDF 형식 출력 기능 포함

3. **성적 업로드 화면 (`REQ-003`)**  
   - `/admission-ui/src/pages/ScoreUpload.tsx`  
   - 엑셀 업로드, 템플릿 다운로드 기능 포함

4. **지원자 목록 조회 (`REQ-004`)**  
   - `/admission-ui/src/pages/ApplicantList.tsx`  
   - 검색, 필터, 페이징 기능 포함

5. **라우팅 구성**  
   - `App.tsx`에 위 페이지 라우팅 추가

6. **UI 검증**  
   - `npm start`로 확인, 페이지별 렌더링 확인

## Phase 3: Backend Development (admission-api)

1. **접수 데이터 점검 API (`REQ-001`)**  
   - `/admission-api/controller/DataCheckController.java`  
   - 이상 데이터 조회 및 수정 API 구현

2. **지원서 출력 데이터 API (`REQ-002`)**  
   - `/ApplicationController.java`  
   - 접수자별 지원서 내용 조회 및 PDF 변환

3. **성적 업로드 기능 (`REQ-003`)**  
   - `/ScoreUploadController.java`, `/ExcelUploadService.java`  
   - 엑셀 파싱 및 유효성 검사 처리

4. **지원자 목록 API (`REQ-004`)**  
   - `/ApplicantController.java`  
   - 모집 시기별 일괄 조회 지원

5. **성적 기반 평가 관리 (`REQ-005`)**  
   - `/EvaluationController.java`, `/EvaluationRuleService.java`  
   - 평가 요소, 가중치 적용, 점수 산정 로직 포함

6. **Validation**  
   - JUnit + MockMvc로 단위/통합 테스트 구현  
   - Postman으로 각 API 테스트

## Phase 4: Integration

1. **Frontend ↔ Backend 연동**  
   - `api.ts` 및 `uploadService.ts` 파일에서 API 연동 구현

2. **CORS 구성 및 예외 처리**  
   - 전역 CORS 필터 설정  
   - 예외 발생 시 사용자 메시지 반환

3. **End-to-End 검증**  
   - 원서 접수 → 목록 조회 → 출력까지의 흐름 테스트  
   - 로그 DB에 저장되는지 확인

## Phase 5: Deployment

1. **Dockerfile 작성**  
   - `/admission-ui`, `/admission-api` 각각 작성

2. **CI/CD 구성**  
   - `.github/workflows`에 push 시 자동 배포 설정

3. **Kubernetes 매니페스트 구성**  
   - `/infra/k8s/` 하위에 서비스, 디플로이먼트 구성

4. **PostgreSQL 배포**  
   - Docker 이미지 기반 배포  
     ```bash
     docker run --name postgres-admission -e POSTGRES_PASSWORD=admpwd -d postgres:15
     ```

## Final Validation and Testing

1. **사용자 수용 테스트 (UAT)**  
   - 입학처 직원이 접수, 조회, 출력 시나리오를 검증

2. **보안 및 성능 테스트**  
   - 파일 업로드 검증, 대용량 목록 조회 성능 측정

3. **최종 배포 및 URL 공유**  
   - 안정성 확인 후 프로덕션 클러스터로 배포

4. **운영자 교육 자료 제공 및 프로젝트 인수인계**
