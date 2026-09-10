# blog-assets

`missed-money.blogspot.com` (놓친 돈 노트) 의 **본문 이미지 호스팅**.

## 왜 별도 저장소인가

Blogger API v3 에는 미디어 업로드 메서드가 **하나도 없다** (discovery 문서 실측, 2026-09-10).
`posts.insert` 는 HTML 만 받으므로 이미지는 밖에 두고 URL 로 참조해야 한다.
로컬 경로를 그대로 두면 발행된 글의 이미지가 전부 깨진다.

## 규칙

- 경로: `assets/<run-id>/<이름>.png`
- 공개 URL: `https://danielkkkk12.github.io/blog-assets/assets/<run-id>/<이름>.png`
- `raw.githubusercontent.com` 은 쓰지 않는다 — GitHub 이 CDN 용도를 권하지 않는다
- **검수를 통과한 글의 이미지만 올라온다.** 파이프라인 `45-host` 가 `40-review` 뒤에 있다
- 반려된 글의 `run-id` 디렉터리는 지운다. 지우기 전에 그 URL 을 쓰는 공개 글이 없는지 확인한다

## 업로드 방식

git 클론·푸시를 쓰지 않고 **GitHub Contents API** 로 올린다.
이 머신의 git 은 system 설정(`/etc/gitconfig`)에 `osxkeychain` 이 걸려 있고,
**키체인은 TTY 없이 안 열린다**(`AGENTS.md` §8) — 매일 07:00 스케줄은 TTY 가 없다.
Contents API 는 `gh` 토큰(파일 기반)만 쓰므로 헤드리스에서 돈다.

**이 저장소를 비공개로 바꾸면 발행된 모든 글의 이미지가 깨진다.**
