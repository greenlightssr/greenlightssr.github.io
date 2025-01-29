---
layout: single
title: "스터디 사용법..."
date: 2025-01-17
last_modified_at: 2025-01-23
categories:
  - about
author: junoh_shin
sidebar:
  nav: "categories"
---

## 블로그 사용볍

보통 블로그는 페이지에 들어와서 글쓰기 버튼을 누르고 글을 작성합니다. <br>글 작성도 설정도 꾸미기도 다 페이지에 들어가서 합니다.<br><br>
하지만 이 블로그는 [Github Pages](https://pages.github.com)와 [Jekyll](https://jekyllrb-ko.github.io)을 사용하기 때문에<br>
**github에서 블로그 코드를 다운받고 파일에 내용을 직접 써야합니다.**<br><br>
기본적으로 블로그를 블로그처럼 만드는데 대부분의 기능은 지원이 되지만<br>
그걸 알아야 쓸 수 있기 때문에<br>
어떤 걸 할 수 있는지 하나씩 알아보려고 합니다.

### 0. 브랜치 설정

여러 명이 사용하는 레포지토리이기 때문에<br>
모두가 메인 브랜치를 사용하지 않고, 각자의 브랜치를 만들어서 사용합니다.<br>

#### 1) 클론하기

```Shell
git clone https://github.com/greenlightssr/greenlightssr.github.io
git checkout -b user/본인이름
```

이후 만들어진 브랜치에서 모든 작업을 실행하면 됩니다.<br>
앞으로의 모든 작업 본인 이름으로 만든 브랜치에서 실행하시면 됩니다.<br>
이후 [아래로](#1-글쓴이-정보-설정) 내려가서 글쓰기 혹은 정보 수정 작업 완료 하신 후, <br>
다시 여기로 돌아와서 커밋 남기고 이어서 작업하시면 됩니다.<br>

#### 2) 커밋 남기기

```Shell
git add .
git commit -m "커밋 메시지" # 쓰고 싶은 말 쓰시면 됩니다.
git push origin user/본인이름
```

글을 작성한 후, 커밋을 남기고 본인 이름으로 된 브랜치에 올리시면 됩니다.<br>
커밋 내용은 아무말이나 써도 되지만, 보통 본인이 어떤걸 했는지 작성합니다.<br>

#### 3) 풀 리퀘스트 보내기

이제 [깃허브](https://github.com/greenlightssr/greenlightssr.github.io)로 가서 <br>
풀리퀘스트 창으로 가서 New pull request 버튼을 누릅니다.<br>
혹은 push 이후 메인페이지를 보면<br>
![pull request](/assets/images/posts/about/pull-request.png)<br>
풀리퀘스트를 하라고 뜹니다. Compare & pull request 버튼을 눌러줍니다.<br>
<br>
![pull requests error](/assets/images/posts/about/pull-request-error.png)<br>
기분나쁜 빨간 글씨가 뜨는데, <br>
base repository를 `greenlightssr/greenlightssr.github.io`로 하면<br>
Able to merge가 뜹니다. (compare는 본인이 사용하던 branch를 선택합니다.)<br>
이제 여기에도 본인이 쓰고 싶은 말을 쓰고<br>
create pull request 버튼을 누르면 풀리퀘스트가 생성됩니다.<br>
이제 누군가가 pull request를 approve하면 포스팅이 완료됩니다.<br>

### 1. 글쓴이 정보 설정

여러명이 글을 쓰는 블로그이기 떄문에 각자 정보를 등록하고<br>
글을 쓸때 본인이 썼다고 이걸 보여줘야 합니다.

#### 1) /\_data/authors.yml에 본인 데이터 추가하기

![author help](/assets/images/posts/about/help-author.png)<br>
본명 안쓰시고 닉네임 쓰셔도 됩니다.

id: // 소문자, 언더스코어만 가능, 띄어쓰기 불가.<br>
// 띄어쓰기 두칸 씩 탭 잘 맞춰야 합니다.<br>
&nbsp;&nbsp;name: "" // 이름입니다.<br>
&nbsp;&nbsp;bio: "" // 설명입니다.<br>
&nbsp;&nbsp;avatar: "" // 프로필 이미지입니다. `/assets/images/` 안에 파일 넣고 경로 입력하시면 됩니다.<br>
&nbsp;&nbsp;&nbsp;&nbsp;links: // 각자 링크 형식에 맞춰 넣으시면 됩니다. 없으시면 입력 안하시면 됩니다.

#### 2) post header에 추가하기

![post header](/assets/images/posts/about/post-header.png)<br>
각 post header의 author에 authors.yml에 입력한 id를 입력해줍니다.

#### 3) 본인이 작성한 포스트 목록 보기

![add author.md](/assets/images/posts/about/add-author-md.png)<br>
`/_pages/users/`에 본인 이름으로 파일 하나 만드시고<br>
위와 같이 작성해주시면 됩니다.<br>
author와 premalink에는 본인 id를 정확히 입력하셔야 합니다.

### 2.`/_posts/`에 글 쓰기

`/_posts/` 폴더 아래에 yyyy-mm-dd-title.md 형식으로 파일을 만들어줍니다.<br>
yyyy-mm-dd는 작성 날짜이고 title은 주소가 됩니다.<br>
이 포스트의 경우, 주소는 [https://greenlightssr.github.io/about/about-blog/]가 됩니다.<br>

#### 1) post header 설정하기

위의 author 부분 말고 다른 부분도 직접 설정할 수 있습니다.<br>
![post header](/assets/images/posts/about/post-header.png)<br>
layout: `/_layout/` 폴더 아래에 있는 여러가지 layout을 사용할 수 있습니다.<br>
title: "" 사이트에서 보일 포스트의 제목입니다.<br>
date: 글을 최초 작성한 날짜입니다.<br>
last_modified_at: 글을 마지막으로 수정한 날짜입니다.<br>

`날짜들은 현재 날짜보다 미래를 설정하면 업로드가 되지 않을 수 있습니다. 새벽에 포스트를 업로드할 경우 바뀐 날짜로 업로드하면 업로드가 되지 않을 수 있습니다.`

categories: 여러개를 설정할 수 있습니다. 하나만 설정하는 것을 권장합니다.<br>
`/_pages/categories/` 아래에 카테고리를 만들 수 있습니다.<br>
tags: 여러개를 설정할 수 있습니다.<br>
`/_pages/tags/` 아래에 태그를 만들 수 있습니다.<br>
author: 글쓴이를 설정할 수 있습니다.<br>
sidebar: 포스트 왼쪽에 무엇을 표시할지 정할 수 있습니다. 글쓴이 정보는 기본으로 설정되어있습니다.<br>
&nbsp;&nbsp;nav: "category" 카테고리를 표시할 수 있습니다.<br>

#### 2) 내용 작성하기

이제 드디어 글을 작성하실 수 있습니다.<br>
그냥 글을 작성해도 되지만, 마크다운의 문법에 맞춰서 작성하면
좀 더 보기 좋은 글을 만들 수 있습니다.<br><br>
[마크다운 문법 & 테스트](https://markdown-it.github.io) 사이트에서<br>
마크다운 문법을 간단하게 확인하고 테스트 해볼 수 있습니다.

### 3. 어떻게 보이는지 실행해보기

글을 다 썼으면 다 쓴 글이 어떻게 보일지, 어떻게 생겼는지를 확인해보고 포스팅을 하고 싶을 수 있습니다.<br>
이걸 확인하는 방법이 몇 가지 있습니다.

#### 1) 마크다운 미리보기

![previewer icon](/assets/images/posts/about/markdown-previewer.png)<br>
vscode에서 미리보기 아이콘을 누르면 마크다운이 어떻게 표시 되는지 미리 확인할 수 있습니다.<br>
이 외에도 인터넷에 많은 마크다운 미리보기 사이트가 있습니다.

#### 2) 로컬에서 직접 실행해보기

미리보기로 볼 순 있지만 실제 사이트에 보이는 것과 미묘하게 일부 다른 부분이 있습니다.<br>
미리보기에는 글 내용만 보이지만 포스트의 헤더와 블로그의 나머지 부분이 적용된 건 볼 수 없습니다.<br>
Jekyll은 RubyGem이기 때문에 ruby가 설치되어 있어야 실행해볼 수 있습니다.<br>

##### 1. Ruby 설치

Mac OS는 기본적으로 ruby가 설치되어 있습니다. 하지만 버전이 낮아서 업데이트를 해야할 수도 있습니다.<br>
윈도우에는 그런거 없습니다. 설치해야 합니다.

##### 2. Bundler 설치

Bunder는 ruby의 패키지 의존성 관리 툴입니다.

```Shell
$ gem install bundler
```

Bundler를 설치해주고

```Shell
$ bundle install
```

을 통해 의존성을 설치해줍니다.<br>
만약 오류가 발생한다면, Gemfile에 의존성이 없는 것이기 때문에

```Shell
$ bundle add jekyll
```

로 Jekyll을 추가해줍니다.

##### 3. 실행

```Shell
# project root folder(/gieenlightssr.github.io)
$ bundle exec jekyll serve
```

를 통해 사이트를 서버에 올립니다.<br>
이제 127.0.0.1:4000에서 실제 블로그와 내 포스트가 어떻게 보일지를 확인 할 수 있습니다.
.<br>
이제 다시 [커밋 남기기](#2-커밋-남기기)로 돌아가서 포스팅을 완료할 수 있습니다.

> 계속 업데이트 중입니다...
