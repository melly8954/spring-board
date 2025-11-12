# spring-board
Spring Boot + React 기반의 JWT 인증 게시판 시스템<br><br>


## 프로젝트 구성

| 구분 | 저장소 | 설명 |
|------|---------|------|
| 🎨 **Frontend** | [spring-board-react](https://github.com/melly8954/spring-board-react) | React 기반 SPA 게시판 클라이언트 |
| ⚙️ **Backend** | [sp-board](https://github.com/melly8954/sp_board) | Spring Boot 기반 REST API 서버 |
> JWT 인증 구조와 RESTful API 설계를 기반으로 React와 연동된 실무형 게시판 구현을 목표로 한 토이 프로젝트입니다.

<br>

## 기술 스택

| 구분             | 사용 기술                                   |
| -------------- | --------------------------------------- |
| **Frontend**   | React, vite                                   |
| **Backend**    | Spring Boot 3.4.9, Spring Security, JPA |
| **Database**   | MySQL                                   |
| **인증/토큰 관리**   | JWT, Redis                              |
| **API 테스트 도구** | Postman, Fiddler                        |

<br>

## 주요 기능

### 🔐 회원 관리
- 회원가입
- BCrypt 비밀번호 암호화
- 프로필 이미지 업로드(선택)
- username 중복 검사

### 🔑 로그인
- JWT 기반 로그인 (Access + Refresh Token)
- Redis를 통한 Refresh Token 저장 및 블랙리스트 관리
- 로그아웃 시 Refresh Token 만료 처리

### 📰 게시판
- 게시판 타입(`board_type_tbl`)별 분류
- 게시글 등록 / 수정 / 삭제 (논리 삭제)
- 첨부파일 등록 (`file_tbl`)
- 검색(제목·내용·작성자), 정렬, 페이징
- 조회수, 좋아요 수, 댓글 수 표시

### 💬 댓글
- 댓글 및 대댓글 (parent_id 기반 트리 구조)
- 재귀 조회로 children_comment 구조 제공
- 본인 댓글 수정/삭제 가능
- 논리 삭제 후 “삭제된 댓글입니다” 표시

### ❤️ 좋아요
- `like_tbl`로 관리 (related_type + related_id + member_id)
- 단일 좋아요 제한

### 🗂️ 파일 관리
- `file_tbl`을 통한 첨부 파일 통합 관리
- 저장 경로: `/sp_board/files/board 또는 member/{type}/`
- 파일명: `UUID_originalName.ext`

---

### Demo
| 기능 1 | 기능 2 |
|--------|--------|
| ![GIF1](https://private-user-images.githubusercontent.com/49448330/513221002-5221b547-fd06-4d49-9fa2-cabd3b798a79.gif?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NjI5NDAzNTUsIm5iZiI6MTc2Mjk0MDA1NSwicGF0aCI6Ii80OTQ0ODMzMC81MTMyMjEwMDItNTIyMWI1NDctZmQwNi00ZDQ5LTlmYTItY2FiZDNiNzk4YTc5LmdpZj9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTExMTIlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUxMTEyVDA5MzQxNVomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTEzZjM0ZDZlOGJjODJiZDgyZDM5MDQyYjk5NmM2ZDUxN2FmMGRjNDA1NzA5MTUyZmY1NWFlZTliMDg2Mjk4MGImWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.RonOSWsiOUdYiena_1gmqnRLA74F92AJrnOaY4rEpTc) | ![GIF2](https://private-user-images.githubusercontent.com/49448330/513221002-5221b547-fd06-4d49-9fa2-cabd3b798a79.gif?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NjI5NDAzNTUsIm5iZiI6MTc2Mjk0MDA1NSwicGF0aCI6Ii80OTQ0ODMzMC81MTMyMjEwMDItNTIyMWI1NDctZmQwNi00ZDQ5LTlmYTItY2FiZDNiNzk4YTc5LmdpZj9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTExMTIlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUxMTEyVDA5MzQxNVomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTEzZjM0ZDZlOGJjODJiZDgyZDM5MDQyYjk5NmM2ZDUxN2FmMGRjNDA1NzA5MTUyZmY1NWFlZTliMDg2Mjk4MGImWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.RonOSWsiOUdYiena_1gmqnRLA74F92AJrnOaY4rEpTc) |



