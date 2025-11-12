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
| 회원가입 및 로그인 | 게시글 등록 |
|--------|--------|
| ![GIF1](https://private-user-images.githubusercontent.com/49448330/513239764-7d43b931-21d7-4466-ac7b-12df8e1d4f69.gif?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NjI5NDIzNTgsIm5iZiI6MTc2Mjk0MjA1OCwicGF0aCI6Ii80OTQ0ODMzMC81MTMyMzk3NjQtN2Q0M2I5MzEtMjFkNy00NDY2LWFjN2ItMTJkZjhlMWQ0ZjY5LmdpZj9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTExMTIlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUxMTEyVDEwMDczOFomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPWEyM2ZmYjU4NzFlMzUxNzA5M2ViODBlNmQ4Nzc1MzFmYWJhZjc0OTFhMmI0ZjA3NDQxOWJkOTUwN2IzYTkwYWYmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.Kik0x5iRwXJva3_pSoxhZ1M5uOwHhleAzSw7DhWBJDI) | ![GIF2](https://private-user-images.githubusercontent.com/49448330/513239547-4d1c8f97-6e15-40a0-9d2c-312c0cec56af.gif?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NjI5NDIzNTgsIm5iZiI6MTc2Mjk0MjA1OCwicGF0aCI6Ii80OTQ0ODMzMC81MTMyMzk1NDctNGQxYzhmOTctNmUxNS00MGEwLTlkMmMtMzEyYzBjZWM1NmFmLmdpZj9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTExMTIlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUxMTEyVDEwMDczOFomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPWVjNjdjODcyNzZhYmE5M2E2YmZmY2M0ZGJiYmQ4ZDA4NDZjMzAyZWE4MzlhYjkyZTMzZjdjMjYyOTMzYWI1YmYmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.MDO5OndpUJhN-O2j8isLu6GFcyd-7z377QvL7-g-fHE) |

<br>

| 게시글 수정 및 삭제 | 댓글 등록 |
|--------|--------|
| ![GIF1](https://private-user-images.githubusercontent.com/49448330/513241887-37edb9f6-e255-4fd5-8af3-3b985d311b03.gif?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NjI5NDI2MzYsIm5iZiI6MTc2Mjk0MjMzNiwicGF0aCI6Ii80OTQ0ODMzMC81MTMyNDE4ODctMzdlZGI5ZjYtZTI1NS00ZmQ1LThhZjMtM2I5ODVkMzExYjAzLmdpZj9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTExMTIlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUxMTEyVDEwMTIxNlomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTZhZmU3ZDE1MzcwYTc0N2QyMmQ5Zjg1MTFlZGM5OGMyMzA2MDI4NjcyYzkyYTlkODFmNWZhODg0MzViOTVhNjcmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.gMKTNi-JiBNzoXMSjtnRI1-bscwXGKqMQpElyjDJK8M) | ![GIF2](https://private-user-images.githubusercontent.com/49448330/513239705-962edb5e-3938-4ecc-95b1-d16b9c7a290c.gif?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NjI5NDI2MzYsIm5iZiI6MTc2Mjk0MjMzNiwicGF0aCI6Ii80OTQ0ODMzMC81MTMyMzk3MDUtOTYyZWRiNWUtMzkzOC00ZWNjLTk1YjEtZDE2YjljN2EyOTBjLmdpZj9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTExMTIlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUxMTEyVDEwMTIxNlomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPWViNTgwOGI1NDJhNGIxOWRjNWY4ZGE2YWMyNWY4ZDhhMWJjZTAzZDZmZTI5NGY3ZTM2ZWZjODE3M2RlYWRhMjkmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.zEdzJh7fao1yNRAO6tSDafQE54H3mt59DoQ4tw0qsrM) |


