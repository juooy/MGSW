# MGSW 회사 홈페이지 개발 세팅 — 설계

- 날짜: 2026-07-11
- 상태: 승인됨 (브레인스토밍 인터뷰로 확정)

## 확정된 방향

| 항목 | 결정 |
|---|---|
| 스택 | 순수 HTML/CSS (빌드 도구 없음) |
| 호스팅 | GitHub Pages (`juooy/MGSW`, main 브랜치 루트) |
| 콘텐츠 | 회사 소개 + 제품 목록, 블로그/소식, 앱 지원 페이지, 문의 |
| 동적 기능 | 외부 서비스 연동 (문의 폼 = Formspree, 연결 전까지 mailto) |
| 블로그 목록 | 수작업 관리 — 글 추가 시 목록 페이지 갱신을 Claude가 담당 |
| 이번 범위 | 개발 환경 + 빈 골격까지. 디자인·실제 콘텐츠는 다음 작업 |

## 폴더 구조

```
MGSW/
├── index.html            # 홈 — 회사 소개
├── products/index.html   # 제품 목록
├── support/index.html    # 앱 지원 허브 (앱별 개인정보처리방침이 하위로)
├── blog/index.html       # 블로그 글 목록 (글은 blog/YYYY-MM-DD-slug.html)
├── contact.html          # 문의 — Formspree 폼 자리
├── assets/css/style.css  # 공통 스타일 1개
├── assets/img/           # 이미지
├── 404.html
└── CLAUDE.md             # 리포 규약
```

## 핵심 규약

- **상대경로 링크**: 프로젝트 페이지 base path(`/MGSW/`) 때문에 모든 내부 링크는 상대경로. 예외는 `404.html` 하나 — GitHub Pages가 임의 깊이 경로에서 서빙하므로 절대경로(`/MGSW/`) 사용, 커스텀 도메인 전환 시 이 파일만 수정.
- **공통 헤더/푸터**: 템플릿 엔진이 없으므로 동일 마크업 패턴을 모든 페이지에 복제. 변경 시 전 페이지 일괄 수정 (Claude 담당).
- **블로그 글 추가**: 새 글 파일 생성 + `blog/index.html` 목록 갱신은 항상 한 세트.

## 개발 환경

- 로컬 프리뷰: `python -m http.server 8000`
- 검증: 편집 후 로컬 서버 + gstack `/browse`로 링크·렌더링 확인
- 배포: main push = GitHub Pages 자동 배포 → `https://juooy.github.io/MGSW/`
- 커스텀 도메인: 범위 밖. 필요 시 CNAME 파일 추가 + 404.html 링크 수정

## 마무리 작업

- 배포 후 실제 Pages URL 접속 검증
- `my` 위키에 `projects/mgsw-homepage.md` 신규 등록
