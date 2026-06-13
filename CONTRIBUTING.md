# 개발 가이드

[← README로 돌아가기](README.md)

## 사전 요구사항

- Node.js 20 이상
- npm
- Docker (선택)

## 로컬 환경 구성

1. 저장소 클론

   ```bash
   git clone https://github.com/dev-montyoh/frontend-payment.git
   cd frontend-payment
   ```

2. 의존성 설치

   ```bash
   npm install
   ```

3. 환경변수 파일 생성

   프로젝트 루트에 `.env.local` 파일을 생성하고 아래 항목을 설정합니다.

   ```env
   # 백엔드 API 서버 주소
   API_BASE_URL=http://localhost:8080

   # KG이니시스
   INICIS_MID=...

   # 나이스페이
   NICEPAY_CLIENT_ID=...
   NICEPAY_SECRET_KEY=...
   ```

4. 서버 실행

   ```bash
   # 로컬 환경 (NODE_ENV=local)
   npm run local

   # 개발 환경 (nodemon)
   npm run dev
   ```

5. 브라우저에서 확인

   ```
   http://localhost:3000
   ```

---

## Docker 실행

```bash
docker build -t frontend-payment .
docker run -p 8081:8081 --env-file .env.prod frontend-payment
```

---

## 브랜치 전략

```
origin
  ├── master
  └── feature/
        ├── branch1
        └── branch2
```

1. `master` 기준으로 `feature/branch-name` 브랜치 생성
2. 개발 완료 후 `master`로 Pull Request 생성
3. GitHub Actions — Docker Image 빌드 성공 확인 후 Merge

---

## 커밋 메시지 규칙

[Conventional Commits](https://www.conventionalcommits.org/) 규칙을 따릅니다.

```
<type>: <subject>
```

### Type

| type | 설명 |
|---|---|
| `feat` | 새로운 기능 또는 PG 연동 추가 |
| `fix` | 오류 수정 |
| `refactor` | 기능 변경 없이 코드 구조 개선 |
| `chore` | 설정, 의존성 등 유지보수 |
| `docs` | README, CONTRIBUTING 등 문서 수정 |

### 예시

```
feat: 나이스페이 결제창 연동 추가
fix: 이니시스 리다이렉트 URL 오류 수정
refactor: 공통 Axios 인스턴스 분리
chore: dotenv-flow 의존성 추가
docs: 로컬 환경 구성 가이드 작성
```
