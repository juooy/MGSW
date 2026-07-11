# MGSW — MariGoldSoftWare 회사 홈페이지

순수 HTML/CSS 정적 사이트. 빌드 도구 없음. GitHub Pages(main 브랜치 루트)로 자동 배포된다.

- 배포 URL: https://juooy.github.io/MGSW/
- 설계 문서: `docs/superpowers/specs/2026-07-11-homepage-setup-design.md`

## 구조

```
index.html            # 홈 — 회사 소개
products/index.html   # 제품 목록
support/index.html    # 앱 지원 허브 (앱별 문서는 support/<app-slug>/privacy.html)
blog/index.html       # 블로그 글 목록 (글은 blog/YYYY-MM-DD-slug.html)
contact.html          # 문의 (Formspree 연동 전까지 mailto)
assets/css/style.css  # 공통 스타일 — 유일한 CSS 파일
assets/img/           # 이미지
404.html
```

## 규약

- **내부 링크는 반드시 상대경로.** 프로젝트 페이지 base path(`/MGSW/`) 때문에 절대경로는 깨진다. 유일한 예외는 `404.html` — 임의 깊이 경로에서 서빙되므로 절대경로(`/MGSW/`) 사용. 커스텀 도메인 전환 시 `404.html`의 경로만 수정하면 된다.
- **공통 헤더/푸터는 마크업 복제.** 템플릿 엔진이 없으므로 네비게이션·푸터를 수정할 때는 모든 페이지를 일괄 수정한다 (`grep`으로 대상 확인).
- **블로그 글 추가는 한 세트**: ① `blog/YYYY-MM-DD-slug.html` 생성 ② `blog/index.html` 목록 맨 위에 항목 등록 (최신순). 둘 중 하나만 하면 안 된다.
- 새 페이지는 기존 페이지의 헤더/푸터 마크업을 복사해 시작하고, 해당 깊이에 맞게 상대경로를 조정한다.
- 문서·커밋 메시지는 한국어.

## 개발 절차

- **로컬 프리뷰**: `python -m http.server 8000` → http://localhost:8000
- **검증**: 페이지 편집 후 로컬 서버를 띄우고 gstack `/browse`로 렌더링·링크를 확인한 뒤 커밋한다.
- **배포**: main에 push하면 GitHub Pages가 자동 배포 (약 1분 소요). push 후 배포 URL에서 확인.

## 남은 일 (다음 작업 후보)

- 디자인·실제 콘텐츠 (회사 소개 문구, 제품 목록)
- Formspree 계정 생성 후 `contact.html` 폼 활성화 (파일 내 주석 참조)
- 필요 시 커스텀 도메인 (CNAME 추가 + `404.html` 경로 수정)
