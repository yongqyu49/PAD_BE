# PAD Backend (PAD_BE)

PAD(Personal Art Display) 백엔드 서버는 사용자들이 자신의 작품을 공유하고 소통할 수 있는 커뮤니티 플랫폼의 백엔드 API 서버입니다.

## 📋 프로젝트 개요

이 프로젝트는 Spring Boot 3.x 기반의 RESTful API 서버로, 회원 관리, 게시판, 공지사항, 즐겨찾기 등의 기능을 제공합니다.

## 🛠 기술 스택

### Backend Framework
- **Spring Boot** 3.2.1-SNAPSHOT
- **Java** 17
- **Gradle** 빌드 도구

### 주요 라이브러리
- **Spring Web** - RESTful API 구현
- **Spring Security** - 인증/인가 처리
- **Spring JDBC** - 데이터베이스 연동
- **MyBatis** 3.0.3 - SQL 매핑 프레임워크
- **Lombok** - 코드 간소화
- **Oracle JDBC** - Oracle 데이터베이스 연결

### 데이터베이스
- **Oracle Database** 21c (with Wallet 지원)

## 📦 프로젝트 구조

```
src/
├── main/
│   ├── java/com/pad/dev/
│   │   ├── controller/       # REST API 컨트롤러
│   │   │   ├── BoardController.java
│   │   │   ├── MemberController.java
│   │   │   └── NoticeController.java
│   │   ├── service/          # 비즈니스 로직
│   │   ├── serviceImpl/      # 서비스 구현체
│   │   ├── dao/              # 데이터 접근 인터페이스
│   │   ├── daoImpl/          # DAO 구현체
│   │   └── vo/               # Value Objects
│   │       ├── boardVO/
│   │       ├── memberVO/
│   │       ├── notiVO/
│   │       ├── cateVO/
│   │       ├── imgVO/
│   │       └── favVO/
│   └── resources/
│       ├── mapper/           # MyBatis XML 매퍼
│       ├── static/           # 정적 리소스
│       └── configuration.xml # 설정 파일
└── test/                     # 테스트 코드
```

## 🚀 시작하기

### 사전 요구사항

- Java 17 이상
- Gradle 7.x 이상
- Oracle Database 21c
- Oracle Wallet 파일 (데이터베이스 연결용)

### 설치 및 실행

1. **저장소 클론**
   ```bash
   git clone https://github.com/yongqyu49/PAD_BE.git
   cd PAD_BE
   ```

2. **데이터베이스 설정**
   - Oracle Wallet 파일 설정
   - `application.yml` 파일에 데이터베이스 연결 정보 입력
   - 프로젝트 루트의 `application.yml`은 `.gitignore`에 포함되어 있으므로 직접 생성 필요

3. **빌드**
   ```bash
   ./gradlew build
   ```

4. **실행**
   ```bash
   ./gradlew bootRun
   ```

   또는

   ```bash
   java -jar build/libs/dev-0.0.1-SNAPSHOT.war
   ```

5. **서버 확인**
   - 서버는 기본적으로 **8800 포트**에서 실행됩니다
   - 콘솔에 "Server running... PORT : 8800" 메시지 확인

## 📡 API 엔드포인트

### 회원 관리 (`/proxy/member`)

| 메서드 | 엔드포인트 | 설명 |
|--------|-----------|------|
| POST | `/proxy/member/SignUp` | 회원가입 |
| POST | `/proxy/member/SignIn` | 로그인 |
| POST | `/proxy/member/Logout` | 로그아웃 |
| POST | `/proxy/member/MyInfo` | 내 정보 조회 |
| POST | `/proxy/member/Update` | 회원정보 수정 |
| POST | `/proxy/member/Delete` | 회원 탈퇴 |
| POST | `/proxy/member/MyFavorite` | 내 즐겨찾기 목록 |
| POST | `/proxy/member/MyFavoriteCount` | 즐겨찾기 개수 |
| POST | `/proxy/member/fav` | 즐겨찾기 추가 |
| POST | `/proxy/member/favCancle` | 즐겨찾기 취소 |
| POST | `/proxy/member/session` | 세션 정보 조회 |

### 게시판 (`/proxy/board`)

| 메서드 | 엔드포인트 | 설명 |
|--------|-----------|------|
| POST | `/proxy/board` | 게시글 목록 조회 (페이징) |
| POST | `/proxy/board/category` | 카테고리별 게시글 조회 |
| POST | `/proxy/board/cate` | 카테고리 목록 조회 |
| POST | `/proxy/board/watch` | 게시글 상세 조회 |
| POST | `/proxy/board/Write` | 게시글 작성 |
| POST | `/proxy/board/Update` | 게시글 수정 |
| POST | `/proxy/board/Delete` | 게시글 삭제 |
| POST | `/proxy/board/myBoard` | 내 게시글 목록 |
| POST | `/proxy/board/myBoardCount` | 내 게시글 개수 |
| POST | `/proxy/board/count` | 전체 게시글 개수 |
| POST | `/proxy/board/image` | 이미지 업로드 |
| POST | `/proxy/board/latestBoard` | 최신 게시글 조회 |

### 공지사항 (`/proxy/notice`)

| 메서드 | 엔드포인트 | 설명 |
|--------|-----------|------|
| POST | `/proxy/notice/mainNotice` | 공지사항 목록 조회 |

## ⚙️ 설정

### 데이터베이스 연결

Oracle Wallet을 사용한 보안 연결을 지원합니다. `application.yml` 파일에서 다음 정보를 설정하세요:

```yaml
spring:
  datasource:
    url: jdbc:oracle:thin:@<your-database-url>
    username: <your-username>
    password: <your-password>
```

### 이미지 저장 경로

게시판 이미지는 `/images` 디렉토리에 저장됩니다. 필요에 따라 `BoardController.java`에서 경로를 수정할 수 있습니다.

### 세션 설정

- 세션 유지 시간: 1800초 (30분)
- 세션은 로그인 시 자동 생성되며, 로그아웃 시 무효화됩니다

## 🔐 보안

- **Spring Security**를 사용한 인증/인가 처리
- **PasswordEncoder**를 통한 비밀번호 암호화
- 세션 기반 사용자 인증

## 📝 개발 가이드

### 새로운 API 추가

1. `vo` 패키지에 Value Object 생성
2. `dao` 인터페이스와 `daoImpl` 구현체 작성
3. `mapper` 디렉토리에 MyBatis XML 매퍼 작성
4. `service` 인터페이스와 `serviceImpl` 구현체 작성
5. `controller`에 REST API 엔드포인트 추가

### 코드 스타일

- Lombok을 활용한 보일러플레이트 코드 최소화
- `@RequiredArgsConstructor`를 통한 의존성 주입
- `@Log4j2`를 활용한 로깅

## 🧪 테스트

```bash
./gradlew test
```

## 📦 배포

### WAR 파일 생성

```bash
./gradlew build
```

생성된 WAR 파일은 `build/libs/` 디렉토리에서 확인할 수 있습니다.

### Docker 배포

프로젝트에 `Dockerfile`이 포함되어 있습니다 (`.gitignore`에서 제외됨).

## 🤝 기여

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 라이선스

이 프로젝트는 개인 프로젝트입니다.

## 👥 개발자

- **yongqyu49** - [GitHub](https://github.com/yongqyu49)

## 📞 문의

프로젝트 관련 문의사항은 GitHub Issues를 통해 남겨주세요.
