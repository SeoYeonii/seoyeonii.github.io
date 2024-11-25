---
layout: article
title: Jekyll + Github Pages로 개발 블로그 만들기
article_header:
  type: overlay
  theme: dark
  background_color: "#203028"
  background_image:
    gradient: "linear-gradient(135deg, rgba(34, 139, 87 , .4), rgba(139, 34, 139, .4))"
    src: /assets/images/banners/github_blog.webp
author: SeoYeonii
categories: github blog
tags: [github-pages, jekyll]
top: 1
# sidebar: []
---

> - Jekyll을 사용해서 쉽고 간편하게 블로그 만들기
> - Github Pages로 만들 블로그 호스팅 하기
> - 기본 템플릿을 수정하여 더 아름답게 블로그 바꾸기

어느 날 스스로에게 조금 더 동기부여를 하고 싶다는 생각이 강하게 들었습니다. 그래서 어떠한 것을 해볼까 고민을 하다가 계속 하고 싶었지만 과제와 업무에 치이며 하지 못했던 개발 블로그를 개설해보기로 했습니다.

## Why Jekyll + github pages?

개발을 하면서 Velog, Tistory 등 여러 개발 블로그들의 도움을 많이 받았습니다. 그래서 별다른 고민 없이 이들 중 깔끔해 보이는 Velog를 선택하려고 했습니다.
그런데 [Velog](https://velog.io/)를 둘러보던 중, 문득 내 마음대로 커스터마이징할 수 있는 블로그를 만들고 싶다는 열망이 생겼습니다.
그래서 대중적인 여러 방법 중, 커스터마이징이 가장 자유로운 방식인 Jekyll로 블로그를 만들고 GitHub Pages로 올리는 방법을 선택했습니다.

### GitHub Pages의 매력

GitHub Pages는 다음과 같은 이유로 매력적이었습니다:

1. **무료 호스팅 제공**: 프로젝트를 무료로 호스팅할 수 있음.
2. **기본 테마 제공**: GitHub Pages에서 제공하는 기본 테마를 사용해 블로그의 모양을 쉽게 설정할 수 있음.
3. **간편한 커스터마이징 가능성**: Jekyll을 통해 복잡한 기능과 독특한 디자인을 간편하게 추가할 수 있음.

### Jekyll 테마 선택하기

[Github Pages docs](https://docs.github.com/ko/pages/quickstart)를 읽어나가며, 굉장히 간단하게 나만의 페이지를 생성할 수 있다는 것을 알게 되었습니다.
[Github Pages가 설명하는 가장 기본 방식](https://docs.github.com/ko/pages/getting-started-with-github-pages/creating-a-github-pages-site)으로 사이트를 구성하면 한 3분안에 Jekyll의 기본 테마인 '[Minima](https://github.com/jekyll/minima)'가 적용된 사이트가 생성됩니다.
![Minima theme 기본 모습](/assets/images/post/github_blog/minima.png)

<p style="font-size: 8px; color: #999999; text-align: center">(생각보다 깔끔하고 이쁠지도..?)</p>

그러나 이 방법을 선택하면 404 page라든지, 게시글마다 어떤 레이아웃을 적용한다든지 이런 세세한 내용들도 전부 다 제가 설정을 해야하기 때문에 제가 생각하던 "조금 더 예쁘고, 최소한의 기능을 갖춘" 블로그를 만들기 위해서는 추가로 설정해야 할 부분이 너무 많아 보였습니다.

그래서 GitHub Pages의 공식 문서를 계속 읽어나가다 보니, Jekyll에서 제공하는 테마를 손쉽게 적용할 수 있다는 것을 알게 되었습니다.

- [GitHub Pages 사이트에서 “지원되는 테마”](https://pages.github.com/themes/)
- [Jekyll](https://jekyllrb-ko.github.io/docs/themes/) 에서 제공하는, 여러가지 테마를 볼 수 있는 사이트
  - [jamstackthemes.dev](jamstackthemes.dev)
  - [jekyllthemes.org](jekyllthemes.org)
  - [jekyllthemes.io](jekyllthemes.io)
  - [jekyll-themes.com](jekyll-themes.com)

이렇게 많은 테마 중에서, 저는 아래 기준에 부합하는 테마를 선택했습니다:

- 태그 및 카테고리 기능 제공: 블로그 관리의 필수 기능.
- 최근 업데이트된 테마: 유지보수가 잘 되고 있는지 확인.
- 디자인: 심플하면서도 보기 좋은 디자인.
- docs가 잘 되어있는 테마: jekyll에 익숙하지 않기 때문에 테마를 잘 활용할 수 있게끔 docs를 제공하는지 확인.

이 과정을 통해 [TeXt Theme](https://github.com/kitian616/jekyll-TeXt-theme)을 선택했습니다.

![TeXt Theme](/assets/images/post/github_blog/text.png)

사실 TeXt Theme에서 몇 가지 걸리는 점들이 있었지만 여러 테마들을 둘러본 결과 굉장히 훌륭한 [docs](https://kitian616.github.io/jekyll-TeXt-theme/docs/en/quick-start)를 가지고 있었기 때문에 큰 고민 없이 바로 선택을 할 수 있었습니다.

## Github Blog 만들기

이제 본격적으로 블로그를 만들어보도록 하겠습니다.

[TeXt Theme docs](https://kitian616.github.io/jekyll-TeXt-theme/docs/en/quick-start)를 보면, 이 theme을 설정하기 위해 일반적으로

1. github에 올려둔 소스를 clone 하거나,
2. 위 사이트에서 제공하는 파일들을 다운로드해서 직접 unzip해서 사용하거나,
3. github에 올려둔 소스를 fork해와서 본인의 repository에 `[본인 깃허브 아이디].github.io`로 repository name을 설정해서 사용하기.

3가지 방법을 추천한다고 나와있습니다.

저는 이 중에서 가장 간편해보이는 3번 방식을 사용해서 블로그를 구성했습니다.

![fork](/assets/images/post/github_blog/fork.png)

이제 받아온 파일 중 `__config.yml` 파일에 기본적인 설정만 마무리하면 "블로그를 만들어서 호스팅까지 하기"는 모두 완료입니다.

```yml
# __config.yml 중 일부

# ~~
## => Site Settings
##############################
text_skin: default # "default" (default), "dark", "forest", "ocean", "chocolate", "orange"
highlight_theme: "tomorrow-night" # "default" (default), "tomorrow", "tomorrow-night", "tomorrow-night-eighties", "tomorrow-night-blue", "tomorrow-night-bright"
url: "https://seoyeonii.github.io" # the base hostname & protocol for your site e.g. https://www.someone.com
baseurl: "" # does not include hostname
title: "서연's log" # 블로그 이름
description: > # this means to ignore newlines until "Language & timezone"

#   Your Site Description

#   ~~
```

저는 아직까지 크게 건들지는 않고, 필수적인 부분인 url과 블로그 이름, 그리고 스킨 정도만 config하고 push하니, 아래와 같은 블로그가 완성되었습니다!

![blog 기본 모습](/assets/images/post/github_blog/blog1.png)

---

## 후기

이제 개발 블로그를 드디어 개설했으니,
앞으로는 이곳에 `제가 관심을 가지고 학습하는 것들`과 또 `이 블로그를 더 아름답게 꾸며나가는 일지`등을 기록해 나갈 예정입니다.

매일 반복되는 바쁜 일상에 지쳐 약간의 매너리즘에 빠져있던 것 같은데, 한 걸음 한 걸음 다시 열심히 정진하고 발전하는 삶을 살 수 있도록 노력할 예정입니다.
