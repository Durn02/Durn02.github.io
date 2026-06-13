---
title: "개발 블로그 만들기 with Github pages"
date: 2026-06-13
categories:
  - 기록
tags:
  - github-pages
  - jekyll
  - minimal-mistakes
  - 개발 블로그 만들기
toc_label: "목차"
comments: true
---

## GitHub Pages란?

GitHub Pages는 GitHub repository에 작성된 코드를 정적 웹사이트로 호스팅해주는 서비스입니다.
별도의 서버 비용 없이 무료로 사용할 수 있고, github에 `push`만 하면 자동으로 배포됩니다.

## Template

[Jekyll themes](https://jekyllthemes.io/jekyll-blog-themes)에서 원하는 템플릿을 골랐습니다. 그 중 minial-mistakes라는 테마를 골랐습니다.

## 왜 Jekyll, Minimal Mistakes인가?

정적 사이트 생성기에는 Jekyll, Hugo, Astro 등 여러 선택지가 있지만 Jekyll을 선택한 이유는 다음과 같습니다.

- GitHub Pages가 Jekyll을 공식 지원하여 별도 빌드 설정이 필요 없음. -> .github/workflows/deploy.yml을 만들 필요 없음.
- Minimal Mistakes 테마가 마음에 들었음.
- 이미 완성된 디자인 템플릿 덕분에 글 작성에 집중할 수 있음.

## 환경 준비

시작 전 아래 도구들이 설치되어 있어야 합니다. (* 은 필수 설치 항목)

- *Git
- *IDE (본인은 VScode를 사용하였음)
- Ruby (로컬에서 Jekyll을 실행하고 싶은 경우)

## 1단계: repository 생성

공식 repository를 fork합니다. jekyllthemes.io에서 원하는 템플릿의 git repository를 fork합니다.

![repository fork 화면](/assets/images/2026-05-30-how-is-this-blog-made/1.png)

위 빨간 네모 부분을 반드시 아래 형식으로 지정해야 합니다.

`{username}.github.io`

ex: `durn02.github.io`


## 2단계: github pages 설정

생성한 repository의 settings->pages에 들어가 아래 모습으로 설정합니다.
![github pages 설정](/assets/images/2026-05-30-how-is-this-blog-made/2.png)

## 3단계: _config.yml 설정

생성한 repository를 clone한 후 _config.yml을 편집합니다.

테마의 핵심 설정 파일입니다. 최소한 아래 항목은 본인 정보로 수정해야 합니다.

```yaml
title: "블로그 이름"
url: "https://{username}.github.io"
repository: "{username}/{username}.github.io"
timezone: "Asia/Seoul"
locale: "ko-KR"

author:
  name: "이름"
  bio: "한 줄 소개"
  location: "Seoul, Korea"
  links:
    - label: "GitHub"
      icon: "fab fa-fw fa-github"
      url: "https://github.com/{username}"
```

## 4단계: 첫 포스트 작성

예시가 궁금하시면 `_docs/_posts`를 참고하면 됩니다.

`_posts/` 폴더를 생성하고 아래 형식으로 파일을 만듭니다.

_posts/YYYY-MM-DD-제목.md

파일 상단에 아래 정보(Front Matter)를 작성합니다.

```yaml
---
title: "첫 번째 포스트"
date: 2026-05-30
categories:
  - 개발
tags:
  - jekyll
---

~~ 본문 내용 ~~
```

본 블로그의 예시:
```yaml
---
title: "개발 블로그 만들기 with Github pages"
date: 2026-05-30
categories:
  - 기록
tags:
  - github-pages
  - jekyll
  - minimal-mistakes
  - 블로그
toc_label: "목차"
comments: true
---
```


## 5단계: 배포

로컬에서 수정한 내용을 push하면 1~3분 안에 자동 반영됩니다.

```bash
git add .
git commit -m "첫 포스트 작성"
git push origin main
```

배포 결과는 저장소의 **Actions** 탭에서 확인할 수 있습니다.
초록색 체크면 성공, 빨간 X면 빌드 오류입니다.

## 기타 사항
1. 스크롤 시 목차를 고정하고 싶은 경우 _config.yml의 맨 밑 `defaults: -> values:` 부분에 `toc_sticky: true`를 추가하면 됩니다.
2. 정적 웹사이트란 그저 껍데기만을 보여주는 사이트를 의미합니다.

## 마치며

처음 설정하는 데 시간이 좀 걸리지만, 한 번 구성해두면 이후에는 마크다운 파일 하나만 추가하면 글이 올라갑니다.
꾸준히 기록하다 보면 어느새 나만의 개발 아카이브가 완성될 거라 생각합니다. 🚀