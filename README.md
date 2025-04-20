# burger-shift-manager

> 개발 동기 : 직원이 많은 가게의 직원 스케쥴링을 위한 개발

# 스마트 스케줄러 프로젝트

## 프로젝트 개요
**직원 가용시간 기반 자동 스케줄러**  
직원들의 가용시간을 최대한 존중하면서, 매장 운영에 필요한 모든 제약조건을 충족하는 최적의 근무표를 자동으로 생성합니다.

---

## 핵심 요구사항
### 운영 시간
- **매일 오전 8시 ~ 익일 새벽 2시**

### 인력 배치 규칙
- **모든 시간대 최소 2명 이상 배치**
- **각 시간대 시니어(이상) 1명 필수**
- **최소 1시간 30분 연속 근무 보장**

### 근무시간 제한
- **일반 직원**: 1주 15시간 미만
- **매니저**: 1일 9시간 이하

### 결과물
- 직원 기준 스케줄 표
- 인력 부족 시간대 별도 표시
- 엑셀 내보내기
- 파일 관리 시스템

---

## 데이터 모델 (간소화)
### 직원(Employee)
```
class Employee {
    Long id
    String name
    EmployeeLevel level // JUNIOR/SENIOR/MANAGER
    int maxWeeklyHours
}
```

### 가용시간(Availability)
```
class Availability {
DayOfWeek day
LocalTime start
LocalTime end
}
```
### 스케줄(Schedule)
```
class Schedule {
LocalDate date
LocalTime start
LocalTime end
ScheduleStatus status // DRAFT/PUBLISHED
}
```
### 파일(ScheduleFile)
```
class ScheduleFile {
Long id
String fileName
String fileType
LocalDateTime uploadDate
byte[] data
String description
Employee uploader
}
```
---

## 시스템 구성요소
- **스케줄 생성 엔진**  
  `가용시간 분석 → 근무 블록 생성 → 인력 배치 최적화`
- **제약조건 검증**  
  `규칙 체크 → 미충족 시간대 표시`
- **엑셀 내보내기**  
  `엑셀 생성 → 색상 구분 적용`
- **파일 관리 시스템**  
  `파일 업로드/다운로드 → 검색 및 필터링 → 메타데이터 관리`

---

## 기술 스택
### 백엔드
- Spring Boot 3.2.x
- Spring Data JPA
- Spring Security
- MySQL
- Lombok
- Apache POI
- Spring File Upload

### 프론트엔드
- Thymeleaf
- Bootstrap 5
- jQuery (FullCalendar, DataTables, Dropzone.js)

---

## 개발 로드맵
1. **설계 및 환경 구축** (1주)  
   DB 설계 · 환경 세팅 · 보안 설정

2. **기본 기능 개발** (2주)  
   직원/가용시간 관리 · 인증 시스템

3. **스케줄링 엔진** (3주)  
   자동 스케줄 생성 · 제약조건 검증

4. **UI 개발** (2주)  
   스케줄 뷰 · 관리 화면 · 파일 관리 인터페이스

5. **파일 관리 시스템** (1주)  
   파일 업로드/다운로드 · 마이페이지 통합

6. **마무리** (1주)  
   엑셀 내보내기 · 통합테스트

---

## 주요 차별점
- **가용시간 중심 스케줄링**
- **최소 연속근무시간 보장(1시간 30분)**
- **시니어 필수 배치**
- **미충족 시간대 명확 표시**
- **개인화된 파일 관리 시스템**

---

## 파일 관리 시스템 상세
### 주요 기능
- **마이페이지 통합**: 사용자별 파일 저장소 제공
- **스케줄 버전 관리**: 여러 버전의 스케줄 저장 및 비교
- **파일 공유**: 특정 직원 또는 그룹과 파일 공유
- **메타데이터**: 파일 설명, 태그, 생성일 등 관리
- **검색 및 필터링**: 날짜, 키워드, 상태 등으로 파일 검색

### 사용자 인터페이스
- **드래그 앤 드롭**: 간편한 파일 업로드
- **미리보기**: 스케줄 파일 미리보기 기능
- **파일 목록**: 정렬 및 필터링 가능한 파일 목록
- **권한 관리**: 파일별 접근 권한 설정

---

## 확장 아이디어
- 모바일 앱 연동
- 실시간 알림
- 근무 통계 대시보드
- AI 기반 인력 배치 예측
- 파일 기반 데이터 분석

---
