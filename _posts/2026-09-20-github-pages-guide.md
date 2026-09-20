---
layout: post
title: "초보자를 위한 GitHub Pages 사용 가이드"
date: 2026-09-20 09:00:00 +0900
tags: [markdown, github]
---

GitHub Pages 공식 문서를 처음 보면 Jekyll, Markdown, front matter, publishing source 같은 단어가 한꺼번에 나와서 무엇부터 해야 할지 막막하다.

이 글은 이 레포에서 바로 첫 글을 쓰고 공개하는 것을 목표로 한다. 복잡한 테마 제작이나 로컬 Jekyll 설치는 뒤로 미루고, 글 파일 하나를 만들고 홈에 링크가 생겼는지와 글 페이지에서 제목·본문이 보이는지 확인하는 순서부터 익힌다.

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

현재 레포에 실제로 있는 핵심 파일은 다음과 같다.

```text
.
├── README.md
├── index.md
├── _config.yml
├── _posts/
    └── YYYY-MM-DD-post-slug.md
```

각 항목의 역할은 다음과 같다.

- `README.md`: 레포 설명을 적는 문서다.
- `index.md`: 사이트 홈 화면과 최근 글 목록을 담당한다.
- `_config.yml`: 사이트 제목과 설명처럼 사이트 전체에 적용되는 설정이다.
- `_posts/`: 날짜가 붙은 블로그 글을 넣는 특별한 폴더다.
- `assets/images/`: 이미지를 사용할 때 직접 만들 선택 폴더다.

`_posts`와 `assets/images`는 필요할 때 직접 만들 수 있다. 처음부터 `_layouts`, `Gemfile`, 복잡한 GitHub Actions 파일까지 만들 필요는 없다.

GitHub Pages는 보통 `index.html`, `index.md`, `README.md` 중 하나를 사이트의 첫 파일 후보로 사용한다. 이 레포에서는 루트의 `index.md`가 홈을 담당하고 `README.md`는 레포 설명 문서로 남아 있다.

날짜가 있는 블로그 글은 `_posts`에 넣고, 소개나 연락처처럼 날짜와 무관한 고정 페이지는 루트에 `about.md`처럼 만들면 된다. 포스트는 파일명 날짜와 `site.posts` 목록에 참여하지만, 고정 페이지는 필요할 때 직접 링크하거나 홈에서 직접 연결한다.

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
tags: [기록]
---

# 나의 첫 번째 글

오늘부터 GitHub Pages에 글을 쓰기 시작한다.

## 오늘 기록한 것

첫 글의 본문을 여기에 작성한다.
```

예시의 날짜는 설명용이므로 실제로 작성하는 날의 날짜와 시간으로 바꿔야 한다. 가장 중요한 규칙은 `---`로 둘러싸인 부분이 파일의 첫 줄부터 시작해야 한다는 것이며, 그 아래 한 줄을 비우고 본문 제목과 내용을 쓰면 된다.

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
| `published` | 글을 공개할지 여부 | 선택 사항이며 기본값은 공개다 |

### 제목

`title: "나의 첫 번째 글"`이 글 제목이다. `_config.yml`에 있는 `title`은 사이트 전체 제목이고, 포스트 파일의 `title`은 개별 글 제목이다.

`title`은 브라우저 제목, SEO 정보, 홈 목록에는 사용되지만 현재 이 레포의 실제 `layout: post` 화면은 본문 제목을 자동으로 보여 주지 않는다. 따라서 이 레포에서 화면에 큰 제목을 보이게 하려면 본문 첫 줄에 `# 나의 첫 번째 글`을 직접 적어야 하며, 다른 테마나 레이아웃을 사용하면 제목이 중복될 수 있으므로 배포된 페이지를 확인해야 한다.

### 날짜

날짜는 커밋한 시간이 자동으로 들어가는 값이 아니다. 파일 이름의 날짜가 기본 날짜로 사용되고, front matter에 `date`를 적으면 그 값이 우선한다.

한국에서 작성한 글은 `2026-09-20 09:00:00 +0900`처럼 시간대까지 적으면 날짜가 다른 날로 바뀌는 문제를 줄일 수 있다. 나중에 글을 수정해도 원래 게시 날짜를 유지하고 싶다면 `date` 값을 바꾸지 않으면 된다.

Jekyll은 기본적으로 미래 날짜의 글을 공개 목록과 생성 결과에서 제외할 수 있다. 빌드는 성공했는데 글이 보이지 않는다면 파일명 날짜와 `date`가 현재 한국 시간보다 미래인지 먼저 확인하고, 테스트 글은 현재 또는 과거 날짜로 설정한다.

### URL

기본 설정에서는 글 주소가 다음처럼 만들어진다.

```text
https://dongju-han.github.io/2026/09/20/first-post.html
```

기본 URL은 파일 이름의 날짜와 slug를 이용하지만, 기본 permalink 설정에 `:categories`가 포함되어 있으면 `categories` 값이 경로 앞에 붙을 수 있다. `tags`는 기본적으로 URL을 바꾸지 않으며, 사이트나 글의 `permalink` 설정에 따라서도 주소가 달라질 수 있다.

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

`#`의 개수로 제목의 단계가 정해진다. 현재 이 레포의 글 레이아웃은 front matter의 `title`을 본문 제목으로 자동 출력하지 않으므로, 글 본문에 보이는 제목이 필요하면 `# 글 제목`을 직접 적고 그 아래 단락부터 `##`를 사용한다.

```markdown
# 글 제목

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

{% raw %}
```markdown
![첫 글 화면 캡처]({{ '/assets/images/first-post/screenshot.png' | relative_url }})
```
{% endraw %}

대괄호 안의 문장은 이미지가 보이지 않을 때 대신 표시되는 설명이다. `relative_url`은 사이트가 루트 도메인이 아니라 `baseurl` 아래에 배포되는 경우에도 경로를 맞춰 주므로 범용 예시에 적합하다. 파일 이름에 공백이나 한글을 넣어도 되지만, 처음에는 영문 소문자와 하이픈을 사용하는 편이 오류를 줄인다.

코드 블록은 다음처럼 언어를 함께 적는다.

````markdown
```python
print("hello")
```
````

Jekyll은 코드 블록을 구문 강조용 HTML로 만들고 실제 색상은 테마와 CSS가 결정한다. 언어 이름은 `python`, `javascript`, `powershell`, `bash`, `yaml`처럼 소문자로 적는다.

## 7. 저장하고 GitHub Pages에 공개하기

글을 작성한 뒤에는 다음 순서로 확인한다.

1. 파일 경로가 `_posts/YYYY-MM-DD-slug.md` 형식인지 확인한다.
2. front matter가 첫 줄의 `---`부터 시작하는지 확인한다.
3. 본문 Markdown과 이미지 경로를 확인한다.
4. `git status`로 변경 파일을 확인한다.
5. 필요한 파일만 스테이징하고 staged diff를 확인한다.
6. 커밋한 뒤 Pages가 사용하는 브랜치에 push한다.

PowerShell에서 작업한다면 명령은 다음처럼 실행할 수 있다.

```powershell
git status
git add _posts/2026-09-20-first-post.md
git diff --cached
git commit -m "Add first post"
git push origin main
```

이미지까지 추가했다면 이미지 파일도 함께 스테이징해야 한다. 처음부터 `git add .`를 기본 명령으로 사용하면 설정 파일이나 비밀값까지 함께 추가할 수 있으므로, `git status`로 확인한 뒤 필요한 파일을 선택적으로 추가하는 편이 안전하다.

GitHub 저장소에서 Settings → Pages → Build and deployment를 열어 실제 배포 원본을 먼저 확인한다. `Deploy from a branch`가 선택되어 있으면 지정된 브랜치와 폴더에 push해야 하고, `GitHub Actions`가 선택되어 있으면 해당 workflow의 트리거 브랜치와 빌드·배포 단계가 실행되어야 한다.

배포가 끝났는지는 다음 세 가지로 확인한다.

1. 브랜치 배포라면 Pages 설정의 배포 상태를 확인하고, Actions 배포라면 해당 workflow가 성공했는지 확인한다.
2. 홈의 글 목록 링크 또는 생성된 실제 URL에 접속해 글이 열리는지 확인한다.
3. 제목, 날짜, 본문, 이미지가 의도한 대로 보이는지 확인한다.

GitHub Pages는 push 직후 바로 보이지 않을 수 있다. 몇 분 기다린 뒤에도 문제가 있으면 Actions의 실패한 작업을 먼저 확인한다.

## 8. 홈 화면에 글 목록 만들기

새 글을 만들었다고 해서 Markdown 파일만으로 홈 화면에 글 목록이 자동으로 생기는 것은 아니다. 홈 화면을 담당하는 파일에 `site.posts`를 출력하는 Liquid 코드가 있어야 한다.

이 레포의 `index.md`는 `README.md` 대신 홈 화면의 내용이 되며, 최근 글의 제목과 날짜를 자동으로 보여 준다.

아주 단순한 글 목록은 다음처럼 만들 수 있다.

{% raw %}
```liquid
---
layout: default
title: Home
---

## 최근 글

{% for post in site.posts %}
- [{{ post.title }}]({{ post.url | relative_url }}) — {{ post.date | date: "%Y-%m-%d" }}
{% endfor %}
```
{% endraw %}

위 코드의 보호용 raw 태그는 이 가이드 안에서 Liquid 예시가 실행되지 않고 문자 그대로 보이게 하는 장치다. 실제 `index.md`에 복사할 때는 보호용 raw 태그를 넣지 않아야 한다.

각 표현의 역할은 다음과 같다.

| 표현 | 의미 |
| --- | --- |
| `{% raw %}{% for post in site.posts %}{% endraw %}` | 사이트의 포스트 모음을 하나씩 반복하기 시작한다. |
| `site.posts` | `_posts`에서 만들어진 공개 포스트 모음이다. 미래 날짜나 `published: false`인 글은 기본적으로 빠질 수 있다. |
| `post` | 반복 중인 현재 글을 가리키는 변수다. |
| `{% raw %}{{ post.title }}{% endraw %}` | 현재 글의 front matter `title`을 출력한다. |
| `{% raw %}{{ post.url | relative_url }}{% endraw %}` | 현재 글의 주소를 가져와 사이트의 `baseurl`을 고려한 링크로 만든다. |
| `{% raw %}{{ post.date | date: "%Y-%m-%d" }}{% endraw %}` | 현재 글의 날짜를 지정한 형식으로 바꾼다. |
| `{% raw %}{% endfor %}{% endraw %}` | 반복을 끝낸다. |

이 코드는 `site.posts`에 들어 있는 글을 순서대로 돌면서 제목, 링크, 날짜를 출력한다. 글이 추가될 때마다 별도의 목록 수정 없이 홈 화면이 함께 갱신된다.

## 9. `_config.yml`의 사이트 제목과 설명

현재 `_config.yml`에는 다음 설정이 있다.

```yaml
title: dongju's page
description: 개발 블로그
```

`title`은 사이트 전체 이름으로 테마, 브라우저 제목, SEO 정보에 사용될 수 있다. 포스트 front matter의 `title`은 개별 글 제목이므로 둘은 서로 다른 값이다.

`description`은 화면 본문에 자동으로 찍히는 소개문이 아니다. 현재 사이트에서는 HTML의 `<head>` 안에 `meta description`, 공유 미리보기용 `og:description`, 구조화된 데이터의 `description`으로 들어가며, 검색엔진이나 SNS가 페이지를 요약할 때 참고한다.

포스트 페이지는 front matter의 별도 설명이 없으면 본문 첫 문단을 페이지 설명으로 사용할 수 있으므로, `_config.yml`의 `description`이 모든 글의 화면에 그대로 보인다고 생각하면 안 된다.

홈 본문에 `개발 블로그`를 직접 보이게 하려면 `index.md`에서 사이트 전역 변수인 `site.description`을 출력해야 한다.

{% raw %}
```liquid
> {{ site.description }}
```
{% endraw %}

이 코드를 `index.md`에 넣으면 홈 화면에 인용문 형태로 설명이 표시된다. 가이드 안에서만 Liquid 예시가 실행되지 않게 raw 태그로 감쌌고, 실제 홈 파일에 복사할 때는 raw 태그를 제외한다.

## 10. 자주 생기는 문제

### 글이 사이트에 나타나지 않는다

먼저 파일이 `_posts` 바로 아래에 있는지 확인한다. `_post`, `posts`, `drafts`처럼 이름이 다르면 일반 폴더로 취급될 수 있다.

파일 이름에 날짜가 빠졌거나 날짜 형식이 `2026-9-2`처럼 한 자리라면 Jekyll 포스트로 인식되지 않을 수 있다. `2026-09-02-title.md`처럼 월과 일을 두 자리로 적고, 파일명과 front matter의 날짜가 미래인지도 확인한다.

### 제목이 두 번 나온다

현재 이 레포에서는 front matter의 `title`이 본문 제목으로 자동 출력되지 않으므로, front matter만 적고 본문에 H1을 쓰지 않으면 글 화면에 제목이 없을 수 있다. 반대로 제목을 자동 출력하는 테마나 레이아웃으로 바꾼 뒤 H1을 직접 남겨 두면 제목이 두 번 나올 수 있으므로 실제 글 화면에서 확인한다.

### 날짜가 생각과 다르다

파일 이름의 날짜와 front matter의 `date`가 서로 다른지 확인한다. 두 값이 모두 있으면 front matter의 `date`가 우선한다.

### 이미지가 깨진다

이미지 파일이 실제로 커밋되었는지 확인하고, Markdown 경로의 대소문자와 확장자가 실제 파일 이름과 같은지 확인한다. 현재 사용자 사이트에서는 `/assets/images/...`도 작동하지만, 프로젝트 사이트까지 고려하면 `relative_url`을 사용하는 방식이 안전하다.

### push했는데 새 글이 안 보인다

먼저 Settings → Pages에서 배포 원본과 브랜치를 확인하고, Actions 방식이면 해당 workflow가 실패했는지 확인한다. 빌드가 성공했는데도 이전 화면이 보이면 몇 분 기다린 뒤 새로고침하고, 홈 목록 링크가 가리키는 실제 주소인지도 확인한다.

### `README.md`를 고쳤는데 글 목록이 생기지 않는다

현재 이 레포에서는 `index.md`가 `README.md`보다 우선하는 홈 진입 파일이고, 홈의 글 목록은 `index.md`와 `site.posts` 반복문이 담당한다. 다른 레포에서 `index.md`가 없으면 `README.md`가 Pages 진입 파일 후보가 될 수 있으므로, 파일 구조를 먼저 확인해야 한다.

### YAML이나 front matter 오류가 난다

front matter는 파일 첫 줄의 `---`로 시작해야 하며 그 안의 내용은 유효한 YAML이어야 한다. 콜론 뒤 값에 특수문자가 있으면 따옴표를 사용하고, 들여쓰기를 임의로 섞지 않으며, Windows 편집기에서 UTF-8 BOM이 붙지 않았는지도 확인한다.

### 가이드의 Liquid 예시가 실제 글 목록으로 실행된다

Jekyll은 포스트 안의 Liquid도 처리하므로, 문서에서 Liquid 문법을 보여 줄 때는 예시 앞뒤를 raw 태그로 감싸야 한다. 실제 `index.md`에서 실행할 코드는 raw 태그 없이 작성한다.

### 공개하면 안 되는 정보가 들어갔다

GitHub Pages와 저장소는 공개 인터넷에 노출될 수 있으므로 API 키, 비밀번호, 개인정보, 내부 문서를 커밋하지 않는다. push 전에 `git status`와 `git diff --cached`로 스테이징된 파일과 내용을 확인한다.

## 11. 앞으로의 추천 순서

처음에는 아래 순서만 반복하면 된다.

1. `_posts` 안에 날짜가 붙은 Markdown 파일을 만든다.
2. front matter에 제목과 날짜를 적는다.
3. 본문을 Markdown으로 쓴다.
4. Pages 설정에서 확인한 배포 브랜치에 push한다.
5. 브랜치 배포 상태 또는 Actions 성공과 글 URL을 확인한다.

글이 몇 개 쌓인 다음에는 `about.md` 같은 고정 페이지, `_drafts`와 `published: false`를 이용한 초안, 태그·카테고리 목록, 테마와 CSS를 차례로 추가하는 것이 좋다. `tags`나 `categories`를 front matter에 적는 것만으로 목록 페이지가 자동으로 생기는 것은 아니므로 별도의 Liquid 템플릿이나 테마 지원이 필요하다.

`_drafts` 안의 글은 보통 날짜 없는 파일로 만들고 일반 배포에서 제외하며, 특정 포스트 front matter에 `published: false`를 적어도 공개 목록에서 숨길 수 있다. 초안을 로컬에서 보려면 Jekyll의 drafts 또는 unpublished 옵션이 필요하므로 첫 게시 흐름과 섞지 않는 편이 쉽다.

로컬에서 사이트 모양을 미리 보고 싶을 때 Jekyll을 설치할 수 있지만, 첫 글을 쓰는 데 필수는 아니다. 나중에 로컬 미리보기를 설정할 때는 GitHub Pages와 같은 의존성을 사용해야 온라인 결과와 로컬 결과의 차이를 줄일 수 있다.

## 12. 로컬 실시간 미리보기

지금까지 설명한 방식은 파일을 수정하고 commit·push한 뒤 GitHub Pages가 빌드할 때까지 기다리는 공개 배포 흐름이다. 글을 쓰는 동안 매번 push하지 않고 바로 확인하려면 내 컴퓨터에서 Jekyll 서버를 실행하고 `http://localhost:4000`을 열면 된다.

로컬 미리보기는 공개 사이트를 바꾸지 않는다. 파일을 저장하면 로컬 서버가 사이트를 다시 만들고 브라우저를 새로고침할 뿐이며, 다른 사람에게 공개하려면 최종적으로 기존처럼 commit과 push를 해야 한다.

### 준비할 것

로컬 Jekyll 미리보기에는 Ruby, RubyGems, Bundler가 필요하다. GitHub Pages와 최대한 비슷한 환경을 만들기 위해 이 레포에서는 Jekyll 자체보다 `github-pages` gem을 Bundler로 설치하는 방식을 사용한다.

현재 레포에는 아직 `Gemfile`이 없으므로, 레포 루트에 `Gemfile`이라는 파일을 새로 만들고 다음 내용을 넣는다.

```ruby
source "https://rubygems.org"

gem "github-pages", group: :jekyll_plugins
```

`Gemfile`은 어떤 Ruby 패키지를 사용할지 적는 파일이다. 이 파일을 만들었다고 해서 글이 공개되는 것은 아니며, 로컬 도구의 의존성만 정하는 설정이다.

### 설치하고 서버 실행하기

레포 폴더에서 PowerShell을 열고 다음 순서로 실행한다.

```powershell
bundle install
bundle exec jekyll serve --livereload
```

터미널에 서버 주소가 표시되면 브라우저에서 [http://localhost:4000](http://localhost:4000)을 연다. `--livereload`를 붙이면 Jekyll이 파일 변경을 감지한 뒤 페이지를 다시 만들고 브라우저도 자동으로 새로고침한다([Jekyll 공식 Quickstart](https://jekyllrb.com/docs/)).

서버를 실행한 터미널은 계속 켜 둔 채 `_posts`의 글이나 `index.md`, `_config.yml`을 수정하고 저장한다. 자동 갱신이 되지 않으면 먼저 Jekyll이 변경을 감지했는지 터미널을 확인하고 브라우저를 수동으로 새로고침한다.

로컬 서버를 끄려면 실행 중인 터미널에서 `Ctrl+C`를 누른다. Jekyll이 만든 `_site` 폴더는 생성 결과물이므로 보통 저장소에 커밋하지 않는다.

### 현재 레포에서 경로가 어긋날 때

`_config.yml`에 `baseurl`이 설정되어 있으면 로컬 주소에 저장소 하위 경로가 붙어 링크와 이미지가 어긋날 수 있다. 이 사용자 사이트처럼 `baseurl`이 없는 구성에서는 기본 명령을 사용하고, 하위 경로 때문에 문제가 생길 때만 `bundle exec jekyll serve --livereload --baseurl=""`로 시험한다.

### 자주 만나는 로컬 오류

| 증상 | 확인하거나 실행할 것 |
| --- | --- |
| `ruby` 또는 `bundle` 명령을 찾을 수 없음 | Ruby와 Bundler를 설치한 뒤 새 터미널을 연다. |
| `Gemfile`을 찾을 수 없음 | 명령을 레포 루트에서 실행하고 `Gemfile` 파일이 있는지 확인한다. |
| Ruby 3 이상에서 `webrick` 오류가 발생함 | `bundle add webrick`을 실행한 뒤 서버를 다시 시작한다. |
| 4000번 포트가 이미 사용 중임 | `bundle exec jekyll serve --livereload --port 4001`처럼 다른 포트를 사용한다. |
| 로컬과 공개 사이트 모양이 다름 | `github-pages` gem을 업데이트하고 테마·플러그인 버전을 확인한다. |

GitHub 공식 문서도 Bundler로 의존성을 관리하고 `bundle exec jekyll serve`로 로컬 사이트를 실행하는 방식을 안내한다([GitHub Pages 로컬 테스트 문서](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/testing-your-github-pages-site-locally-with-jekyll)).

## 13. 게시 전 최종 점검표

- [ ] 파일이 `_posts/YYYY-MM-DD-slug.md` 형식이고 `_posts` 바로 아래에 있다.
- [ ] front matter가 파일 첫 줄의 `---`부터 시작하고 YAML 문법이 올바르다.
- [ ] 파일명 날짜와 `date`가 현재 또는 과거이며 시간대가 의도와 맞다.
- [ ] 본문에 필요한 경우 `# 글 제목`을 직접 적었다.
- [ ] 이미지 파일과 Markdown 경로의 대소문자가 일치한다.
- [ ] 로컬 미리보기에서 저장 후 제목, 날짜, 본문, 이미지가 의도대로 보인다.
- [ ] Liquid 예시를 설명하는 문서는 raw 태그로 보호했고 실제 실행 파일에는 raw 태그가 없다.
- [ ] `git status`로 변경 파일을 확인했고 staged diff에 민감정보가 없다.
- [ ] Settings → Pages에서 실제 배포 원본과 브랜치를 확인했다.
- [ ] push 뒤 Actions 또는 Pages 배포가 성공했다.
- [ ] 홈 목록 링크와 글의 실제 URL을 직접 열어 제목, 날짜, 본문을 확인했다.

## 참고 문서

- [GitHub Pages 공식 문서](https://docs.github.com/en/pages)
- [GitHub Pages에서 Jekyll로 콘텐츠 추가하기](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/adding-content-to-your-github-pages-site-using-jekyll)
- [GitHub Pages 배포 원본 설정하기](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)
- [GitHub Pages 사이트 생성하기](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site)
- [GitHub Pages와 Jekyll](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/about-github-pages-and-jekyll)
- [Jekyll Posts](https://jekyllrb.com/docs/posts/)
- [Jekyll Front Matter](https://jekyllrb.com/docs/front-matter/)
- [Jekyll Liquid 필터](https://jekyllrb.com/docs/liquid/filters/)
- [Jekyll Permalinks](https://jekyllrb.com/docs/permalinks/)
- [Jekyll 빌드 오류 해결](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/troubleshooting-jekyll-build-errors-for-github-pages-sites)
