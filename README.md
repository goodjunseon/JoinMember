
# 🧑‍💻 Spring Boot 회원 관리 웹 애플리케이션

Spring Boot와 Spring Data JPA를 기반으로 한 회원 관리 시스템입니다.  
회원 가입, 로그인, 정보 수정, 삭제, 이메일/비밀번호 찾기 등 **기초적인 회원 기능**을 웹 페이지 기반으로 제공합니다.

---

## ✅ 프로젝트 개요

- **프로젝트명**: Member Web Application 
- **백엔드 프레임워크**: Spring Boot 3.4.4
- **템플릿 엔진**: Thymeleaf
- **DB 연동 방식**: Spring Data JPA
- **기술 스택**: Java 17, Spring Boot, JPA, Lombok, MySQL

---

## 🏗️ 전체 아키텍처

```
[Browser]
   ↓ 요청 (HTTP)
[Controller] → [Service] → [Repository] → [DB]
   ↑ 뷰 렌더링 (HTML)
```

- **Controller**: 사용자 요청을 처리하고 뷰를 반환
- **Service**: 비즈니스 로직 처리
- **Repository**: JPA 기반 DB CRUD 처리
- **DTO/Entity**: 데이터 전달 및 테이블 매핑

---

## 📁 주요 클래스 설명

### 📌 Controller
| 클래스 | 설명 |
|--------|------|
| `HomeController` | 메인 페이지 (`/`) 처리 |
| `MemberController` | 회원 가입, 로그인, 조회, 수정 등 처리 |

### 📌 Service
| 클래스 | 설명 |
|--------|------|
| `MemberService` | 회원 로직 처리: 저장, 로그인, 수정, 삭제 등 |

### 📌 Repository
| 클래스 | 설명 |
|--------|------|
| `MemberRepository` | 이메일, 이름+전화번호+생일 등으로 회원 검색 기능 포함 |

### 📌 Entity / DTO
| 클래스 | 설명 |
|--------|------|
| `MemberEntity` | `@Entity`, DB 테이블 매핑 |
| `MemberDTO` | Controller ↔ Service 간 데이터 전달 객체 |
| `LoginResultDTO` | 로그인 결과 상태 및 사용자 정보 전달 DTO |
| `LoginStatus` | 로그인 상태 Enum (성공, 이메일 오류, 비밀번호 오류) |

---

## 📦 주요 기능

- ✅ 회원 가입 (`/member/save`)
- ✅ 로그인 / 로그아웃 (`/member/login`, `/member/logout`)
- ✅ 회원 목록 조회 (`/member/`)
- ✅ 회원 상세 조회 (`/member/{id}`)
- ✅ 회원 정보 수정 (`/member/update`)
- ✅ 회원 삭제 (`/member/delete/{id}`)
- ✅ 이메일 찾기 (`/member/find-email`)
- ✅ 비밀번호 찾기 (`/member/find-password`)

---

## 🧭 주요 흐름 설명

### ✅ 회원가입
1. 사용자가 `/member/save`에서 폼 제출
2. `MemberController.save()` → `MemberService.save()` 호출
3. `MemberDTO` → `MemberEntity` 변환 후 저장

### ✅ 로그인
1. 로그인 정보 입력 → `/member/login` POST 요청
2. `MemberService.login()` 호출 → `LoginResultDTO` 반환
3. 성공 시 세션 저장, 실패 시 오류 메시지

### ✅ 회원 정보 수정
1. 세션에서 이메일로 사용자 정보 조회 (`updateForm`)
2. 폼에 정보 표시 → 수정 후 저장

---

## ⚙️ 사용 기술 및 설정

- **Spring Boot 3.44**
- **Spring Data JPA**
- **Lombok**: `@Getter`, `@Setter`, `@RequiredArgsConstructor` 등 사용
- **MySQL**
- **Session 기반 로그인 유지**
- **DTO ↔ Entity 변환 메서드 사용**

---

## 🔐 추가 개발 계획 (Optional)

- Spring Security 적용 (권한, 인증)
- REST API 형태로 변경 (SPA 대응)
- 이메일 인증 / 비밀번호 암호화 (BCrypt)
- 예외 처리 및 유효성 검증 (`@Valid` 등)

---

## 🗂️ 패키지 구조 예시

```
com.JunseonPark.member
├── controller
│   ├── HomeController.java
│   └── MemberController.java
├── dto
│   ├── LoginResultDTO.java
│   └── MemberDTO.java
├── entity
│   └── MemberEntity.java
├── repository
│   └── MemberRepository.java
├── service
│   └── MemberService.java
├── enums
│   └── LoginStatus.java
└── MemberApplication.java
```

---

## 📎 참고사항

- HTML 템플릿 파일 (예: `login.html`, `save.html`, `list.html`, `update.html`)은 `resources/templates`에 위치
- 데이터베이스 설정은 `application.yml`에 포함
