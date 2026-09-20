---
layout: post
title: "초보자를 위한 GitHub Pages 사용 가이드"
date: 2026-09-20 09:00:00 +0900
categories: [github-pages, jekyll]
tags: [markdown, github]
---

GitHub Pages 공식 문서를 처음 보면 Jekyll, Markdown, front matter, publishing source 같은 단어가 한꺼번에 나와서 무엇부터 해야 할지 막막하다.

이 글은 이 레포에서 바로 첫 글을 쓰고 공개하는 것을 목표로 한다. 복잡한 테마 제작이나 로컬 Jekyll 설치는 뒤로 미루고, 글 파일 하나를 만들고 배포가 성공했는지 확인하는 순서부터 익힌다.

> 이 글의 기준 레포는 `Dongju-Han/Dongju-Han.github.io`이고 사이트 주소는 [https://dongju-han.github.io/](https://dongju-han.github.io/)다.

## 0. 시작 전에 확인할 것

먼저 아래 네 가지가 준비되어 있으면 된다.

1. GitHub 계정으로 로그인할 수 있어야 한다.
2. `Dongju-Han.github.io` 레포에 글을 올릴 권한이 있어야 한다.
3. 레포를 내 컴퓨터에 내려받았거나 GitHub 웹 편집기를 사용할 수 있어야 한다.
4. 로컬에서 작업한다면 Git이 설치되어 있어야 한다.

현재 이 레포는 이미 GitHub Pages 사이트로 공개되어 있으므로, 당장 Jekyll을 컴퓨터에 설치하지 않아도 된다. 글을 작성한 뒤 GitHub에 push하면 GitHub가 빌드와 배포를 처리한다.

이 글에서는 Windows에서 레포를 로컬로 열고 글을 작성한 뒤 push하는 방법을 기준으로 설명한다. GitHub 웹 화면에서 파일을 직접 만들어도 파일 이름과 내용은 똑같다.

## 1. 이 레포에서 파일이 하는 일

현재 레포의 핵심 파일은 다음과 같다.

```text
.
├── README.md
├── index.md
├── _config.yml
├── _posts/
│   └── YYYY-MM-DD-post-slug.md
└── assets/
    └── images/
```

각 항목의 역할은 다음과 같다.

- `README.md`: 레포 설명을 적는 문서다.
- `index.md`: 사이트 홈 화면과 최근 글 목록을 담당한다.
- `_config.yml`: 사이트 제목과 설명처럼 사이트 전체에 적용되는 설정이다.
- `_posts/`: 날짜가 붙은 블로그 글을 넣는 특별한 폴더다.
- `assets/images/`: 글에 넣을 이미지와 같은 정적 파일을 보관할 폴더다.

`_posts`와 `assets`는 지금 없더라도 직접 만들 수 있다. 처음부터 `_layouts`, `Gemfile`, 복잡한 GitHub Actions 파일까지 만들 필요는 없다.

GitHub Pages는 보통 `index.html`, `index.md`, `README.md` 중 하나를 사이트의 첫 파일로 사용한다. 이 레포는 `index.md`를 사용해 홈 화면에 최근 글 목록을 보여 준다.

## 2. 첫 글을 만드는 가장 짧은 방법

첫 글은 다음 이름의 파일로 시작한다.

`_posts/2026-09-20-first-post.md`

파일 이름의 앞부분은 반드시 네 자리 연도, 두 자리 월, 두 자리 일 순서여야 한다. 뒤의 `first-post` 부분은 글 주소에 사용될 수 있으므로 공백 대신 영문 소문자와 하이픈을 사용하는 편이 안전하다.

파일을 만들고 아래처럼 작성한다.

```markdown
---
layout: post
title: "나의 첫 번째 글"
date: 2026-09-20 09:00:00 +0900
categories: [blog]
tags: [기록]
---

오늘부터 GitHub Pages에 글을 쓰기 시작한다.

## 오늘 기록한 것

첫 글의 본문을 여기에 작성한다.
```

가장 중요한 규칙은 `---`로 둘러싸인 부분이 파일의 첫 줄부터 시작해야 한다는 것이다. 그 아래 한 줄을 비우고 본문을 쓰면 된다.

## 3. 제목, 날짜, URL은 어디에서 정하는가

파일 맨 위의 `---` 사이에 있는 부분을 front matter라고 부른다. Jekyll은 이 영역을 읽어 글의 제목, 날짜, 레이아웃 같은 정보를 정한다.

| 항목 | 의미 | 처음부터 필요한가 |
| --- | --- | --- |
| `layout` | 글에 적용할 화면 틀 | `post`로 적는 것을 권장한다 |
| `title` | 글 제목 | 필요하다 |
| `date` | 글의 작성·게시 날짜와 시간 | 직접 적는 것을 권장한다 |
| `categories` | 글을 묶을 분류 | 선택 사항이다 |
| `tags` | 글을 찾기 위한 태그 | 선택 사항이다 |
| `permalink` | 글의 고정 주소를 직접 정하는 설정 | 선택 사항이다 |

### 제목

`title: "나의 첫 번째 글"`이 글 제목이다. `_config.yml`에 있는 `title`은 사이트 전체 제목이고, 포스트 파일의 `title`은 개별 글 제목이다.

`layout: post`를 사용하면 테마가 front matter의 제목을 화면에 출력하는 경우가 많으므로, 본문에 같은 제목을 다시 `# 나의 첫 번째 글`로 적지 않는 편이 깔끔하다. 본문 안에서 새로운 단락을 시작할 때는 `##`부터 사용하면 된다.

### 날짜

날짜는 커밋한 시간이 자동으로 들어가는 값이 아니다. 파일 이름의 날짜가 기본 날짜로 사용되고, front matter에 `date`를 적으면 그 값이 우선한다.

한국에서 작성한 글은 `2026-09-20 09:00:00 +0900`처럼 시간대까지 적으면 날짜가 다른 날로 바뀌는 문제를 줄일 수 있다. 나중에 글을 수정해도 원래 게시 날짜를 유지하고 싶다면 `date` 값을 바꾸지 않으면 된다.

### URL

기본 설정에서는 글 주소가 다음처럼 만들어진다.

```text
https://dongju-han.github.io/2026/09/20/first-post.html
```

기본 URL은 파일 이름의 날짜와 slug를 이용하지만, 사이트의 `permalink` 설정이나 글의 `permalink` 값에 따라 달라질 수 있다. 주소를 직접 정하고 싶을 때만 다음 항목을 front matter에 추가한다.

```yaml
permalink: /posts/first-post/
```

처음에는 permalink를 생략하고 기본 주소를 사용하는 것이 가장 단순하다.

## 4. Markdown, Jekyll, GitHub Pages의 관계

세 도구의 역할을 한 줄로 연결하면 다음과 같다.

```text
Markdown 글 + front matter
        ↓
Jekyll이 글을 HTML로 변환
        ↓
GitHub Pages가 결과를 웹사이트로 공개
```

- Markdown은 글을 쉽게 쓰기 위한 문법이다.
- Jekyll은 Markdown과 front matter를 읽어 웹페이지를 만드는 프로그램이다.
- GitHub Pages는 만들어진 웹페이지를 인터넷 주소에서 볼 수 있게 해 주는 GitHub 서비스다.
- Git은 파일의 변경 이력을 저장하고 GitHub로 보내는 도구다.

따라서 네가 매번 직접 HTML 파일을 만들 필요는 없다. `_posts`에 Markdown 파일을 만들고 내용을 작성하면 Jekyll이 변환하고, push하면 GitHub Pages가 공개한다.

## 5. 본문에서 자주 쓰는 Markdown 문법

### 제목과 문단

`#`의 개수로 제목의 단계가 정해진다. 포스트 제목은 front matter의 `title`이 담당하므로 본문에서는 보통 `##`부터 시작한다.

```markdown
## 큰 단락

여기에 설명을 쓴다.

### 작은 단락

여기에 더 구체적인 설명을 쓴다.
```

문단을 나누려면 빈 줄을 하나 넣는다. 줄만 바꾸고 빈 줄을 넣지 않으면 같은 문단처럼 보일 수 있다.

### 강조와 목록

```markdown
**굵게 표시할 문장**
*기울여 표시할 문장*

- 첫 번째 항목
- 두 번째 항목

1. 순서가 있는 첫 단계
2. 순서가 있는 두 번째 단계
```

### 링크와 인용

```markdown
[GitHub Pages 공식 문서](https://docs.github.com/en/pages)

> 기억해 둘 문장을 인용문으로 표시한다.
```

### 코드

짧은 코드나 파일 이름은 백틱 하나로 감싼다.

```markdown
`_posts` 폴더에 파일을 만든다.
```

여러 줄의 코드는 백틱 세 개로 감싼다. 첫 줄의 언어 이름을 적으면 문법 강조가 적용된다.

````markdown
```powershell
git status
```
````

## 6. 이미지와 코드 블록 넣기

이미지는 레포 안에 보관하고 Markdown에서 경로를 연결하는 방식이 가장 관리하기 쉽다.

먼저 다음처럼 폴더를 만든다.

```text
assets/images/first-post/screenshot.png
```

그다음 글에서 다음처럼 사용한다.

```markdown
![첫 글 화면 캡처](/assets/images/first-post/screenshot.png)
```

대괄호 안의 문장은 이미지가 보이지 않을 때 대신 표시되는 설명이다. 파일 이름에 공백이나 한글을 넣어도 되지만, 처음에는 영문 소문자와 하이픈을 사용하는 편이 오류를 줄인다.

코드 블록은 다음처럼 언어를 함께 적는다.

````markdown
```python
print("hello")
```
````

GitHub Pages는 코드 블록의 언어를 보고 색상을 입혀 준다. 언어 이름은 `python`, `javascript`, `powershell`, `bash`, `yaml`처럼 소문자로 적는다.

## 7. 저장하고 GitHub Pages에 공개하기

글을 작성한 뒤에는 다음 순서로 확인한다.

1. 파일 경로가 `_posts/YYYY-MM-DD-slug.md` 형식인지 확인한다.
2. front matter가 첫 줄의 `---`부터 시작하는지 확인한다.
3. 본문 Markdown과 이미지 경로를 확인한다.
4. 변경 내용을 커밋한다.
5. `main` 브랜치에 push한다.

PowerShell에서 작업한다면 명령은 다음처럼 실행할 수 있다.

```powershell
git add _posts/2026-09-20-github-pages-guide.md
git commit -m "Add GitHub Pages guide"
git push origin main
```

이미지까지 추가했다면 이미지 파일도 함께 추가해야 한다. 모든 변경을 한 번에 추가하려면 `git add .`를 사용할 수 있지만, 어떤 파일이 포함되는지 먼저 확인하는 습관을 들이는 것이 좋다.

GitHub 저장소에서 Settings → Pages → Build and deployment를 열면 배포 원본을 확인할 수 있다. 이 레포처럼 `main` 브랜치의 루트를 배포하도록 설정되어 있다면 `main`에 push한 변경이 사이트 빌드 대상이 된다.

배포가 끝났는지는 다음 세 가지로 확인한다.

1. 저장소의 Actions에서 Pages 빌드가 성공했는지 확인한다.
2. 글의 예상 URL에 접속해 글이 열리는지 확인한다.
3. 제목, 날짜, 본문, 이미지가 의도한 대로 보이는지 확인한다.

GitHub Pages는 push 직후 바로 보이지 않을 수 있다. 몇 분 기다린 뒤에도 문제가 있으면 Actions의 실패한 작업을 먼저 확인한다.

## 8. 홈 화면에 글 목록 만들기

새 글을 만들었다고 해서 Markdown 파일만으로 홈 화면에 글 목록이 자동으로 생기는 것은 아니다. 홈 화면을 담당하는 파일에 `site.posts`를 출력하는 Liquid 코드가 있어야 한다.

이 레포의 `index.md`는 `README.md` 대신 홈 화면의 내용이 되며, 최근 글의 제목과 날짜를 자동으로 보여 준다.

아주 단순한 글 목록은 다음처럼 만들 수 있다.

```markdown
---
layout: default
title: Home
---

## 최근 글

{% for post in site.posts %}
- [{{ post.title }}]({{ post.url | relative_url }}) — {{ post.date | date: "%Y-%m-%d" }}
{% endfor %}
```

이 코드는 `site.posts`에 들어 있는 글을 순서대로 돌면서 제목, 링크, 날짜를 출력한다. 글이 추가될 때마다 별도의 목록 수정 없이 홈 화면이 함께 갱신된다.

## 9. 자주 생기는 문제

### 글이 사이트에 나타나지 않는다

먼저 파일이 `_posts` 바로 아래에 있는지 확인한다. `_post`, `posts`, `drafts`처럼 이름이 다르면 일반 폴더로 취급될 수 있다.

파일 이름에 날짜가 빠졌거나 날짜 형식이 `2026-9-2`처럼 한 자리라면 Jekyll 포스트로 인식되지 않을 수 있다. `2026-09-02-title.md`처럼 월과 일을 두 자리로 적는다.

### 제목이 두 번 나온다

front matter의 `title`과 본문의 `# 제목`이 모두 출력되고 있을 가능성이 있다. 본문의 첫 번째 제목을 지우거나 `##` 단계로 낮춘다.

### 날짜가 생각과 다르다

파일 이름의 날짜와 front matter의 `date`가 서로 다른지 확인한다. 두 값이 모두 있으면 front matter의 `date`가 우선한다.

### 이미지가 깨진다

이미지 파일이 실제로 커밋되었는지 확인하고, Markdown 경로의 대소문자와 확장자가 실제 파일 이름과 같은지 확인한다. 이 사이트는 루트 주소에서 서비스되므로 `/assets/images/...`처럼 작성할 수 있다.

### push했는데 새 글이 안 보인다

Actions에서 빌드가 실패했는지 먼저 확인한다. 빌드가 성공했는데도 이전 화면이 보이면 몇 분 기다린 뒤 새로고침하고, 주소가 맞는지도 확인한다.

### `README.md`를 고쳤는데 글 목록이 생기지 않는다

`README.md`는 레포 설명 문서일 뿐이고, `_posts`의 글들을 자동으로 나열하는 코드를 포함하고 있지 않다. 홈의 글 목록은 `index.md`와 `site.posts` 반복문이 담당한다.

## 10. 앞으로의 추천 순서

처음에는 아래 순서만 반복하면 된다.

1. `_posts` 안에 날짜가 붙은 Markdown 파일을 만든다.
2. front matter에 제목과 날짜를 적는다.
3. 본문을 Markdown으로 쓴다.
4. 커밋하고 `main`에 push한다.
5. Actions 성공과 글 URL을 확인한다.

이제 글을 몇 개 더 쓴 다음에 테마와 CSS를 손보는 것이 좋다. 글쓰기와 디자인을 동시에 시작하면 어디에서 문제가 생겼는지 찾기 어려우므로, 먼저 글을 꾸준히 공개하는 흐름을 만드는 것이 우선이다.

로컬에서 사이트 모양을 미리 보고 싶을 때 Jekyll을 설치할 수 있지만, 첫 글을 쓰는 데 필수는 아니다. 지금은 GitHub에서 빌드가 성공하는지 확인하는 것만으로 충분하다.

## 참고 문서

- [GitHub Pages 공식 문서](https://docs.github.com/en/pages)
- [GitHub Pages에서 Jekyll로 콘텐츠 추가하기](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/adding-content-to-your-github-pages-site-using-jekyll)
- [GitHub Pages 배포 원본 설정하기](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)
- [Jekyll Posts](https://jekyllrb.com/docs/posts/)
- [Jekyll Front Matter](https://jekyllrb.com/docs/front-matter/)
