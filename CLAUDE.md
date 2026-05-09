# Privacy Policy Apps

개인 개발 앱들의 개인정보 처리방침을 모아 관리하는 hub. Jekyll 기반 정적 사이트로 GitHub Pages 에서 호스팅됨 (theme: `jekyll-theme-cayman`).

- **Live URL**: https://no1joon.github.io/privacy-policy-apps/
- **Project Prefix**: `PPA`

## Commands

빌드·테스트 도구 없음. 마크다운을 수정하고 push 하면 GitHub Pages 가 약 1분 내 자동 빌드·배포.

- `git push origin main`: 변경사항 배포 (Pages 자동 빌드)
- `gh api repos/No1Joon/privacy-policy-apps/pages/builds/latest --jq .status`: 최신 빌드 상태 조회 (`built` / `building` / `errored`)
- `curl -I https://no1joon.github.io/privacy-policy-apps/<path>`: 라이브 URL 200 확인
- 로컬 미리보기 (선택): `bundle exec jekyll serve` (Ruby + jekyll-theme-cayman 설치 필요)

## Architecture

- `index.md`: 루트 랜딩 — 등록된 앱 목록
- `_config.yml`: Jekyll 설정 (title, description, theme)
- `README.md`: GitHub repo 페이지용 설명 (Pages 사이트엔 노출 안 됨)
- `<app-slug>/`: 앱 단위 디렉터리. 새 앱 추가 시 이 패턴으로 폴더만 생성
  - `<app-slug>/index.md`: 해당 앱 소개 + privacy 링크
  - `<app-slug>/privacy.md`: 한국어 개인정보 처리방침 (PIPA 준수)
  - `<app-slug>/privacy-en.md`: 영어 버전 (선택)

현재 등록된 앱: `jjteam/`

## Skills

- `.claude/skills/smart-commit/SKILL.md` — 스테이징된 변경에서 atomic 커밋 메시지 생성, 브랜치명에서 `PPA-<n>` 이슈 ID 추출

## References

See @README.md for repo overview and live URLs
