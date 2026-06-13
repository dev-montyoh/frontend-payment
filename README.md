<br/>

<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/nodejs/nodejs-original.svg" alt="Node.js" width="72" />

# frontend-payment

[![Push Workflow](https://github.com/dev-montyoh/frontend-payment/actions/workflows/push-master.yml/badge.svg)](https://github.com/dev-montyoh/frontend-payment/actions/workflows/push-master.yml)
[![Build Workflow](https://github.com/dev-montyoh/frontend-payment/actions/workflows/pull-request-master.yml/badge.svg)](https://github.com/dev-montyoh/frontend-payment/actions/workflows/pull-request-master.yml)

**결제 PG 연동 테스트를 위한 프론트엔드 서버**

---

Node.js + Express 기반의 결제 테스트용 프론트엔드 서버입니다. KG이니시스, 나이스페이 등 국내 PG사와의 연동 흐름을 직접 확인하기 위해 만들었습니다. HTMX를 사용해 페이지 리로드 없이 결제 탭을 전환하고, 각 PG사의 결제창 호출 및 콜백 처리를 검증합니다.

> 실제 결제 처리 로직(결제 승인 · 조회 · 내역 관리 등)은 **[backend-api-server](https://github.com/dev-montyoh/backend-api-server)** 에 구현되어 있습니다.

---

## 사용 기술

- Node.js, Express 5
- HTMX
- Axios
- dotenv-flow
- Docker

---

## 주요 특징

- **PG 연동** — KG이니시스 · 나이스페이 결제창 호출 및 콜백 처리
- **HTMX 기반 UI** — 페이지 전환 없이 결제 탭 전환 및 partial 렌더링
- **환경 분리** — dotenv-flow로 `local` / `dev` / `prod` 환경 구분
- **컨테이너 배포** — Docker 이미지 빌드 및 OCI 인스턴스 배포

---

## 프로젝트 구조

```
/
├── app.js                  # Express 앱 설정 및 라우터 등록
├── bin/
│   └── www                 # 서버 실행 엔트리포인트
├── routes/                 # 라우팅 모듈
│   ├── view.js             # 페이지 뷰 라우터
│   ├── payment.js          # 공통 결제 라우터
│   ├── inicis.js           # KG이니시스 라우터
│   └── nicepay.js          # 나이스페이 라우터
├── public/                 # 정적 파일
│   ├── views/              # HTMX partial HTML
│   │   ├── inicis/         # 이니시스 결제 탭 뷰
│   │   ├── nicepay/        # 나이스페이 결제 탭 뷰
│   │   └── popup/          # 팝업 방식 결제창 뷰
│   ├── javascripts/        # 클라이언트 JS
│   └── stylesheets/        # CSS
├── common/                 # 공통 유틸
│   └── axios.js            # Axios 인스턴스
├── Dockerfile
└── package.json
```

---

## CI/CD

GitHub Actions를 통해 배포 파이프라인을 구성합니다.

- **push → master**: Docker Image 빌드 및 OCI 인스턴스 배포

---

## 문서

- **[개발 가이드 →](CONTRIBUTING.md)** — 로컬 실행 · 환경변수 · 브랜치 전략 · 커밋 규칙
