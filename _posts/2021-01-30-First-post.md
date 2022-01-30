---
layout: post
title: "How to use jekyll library easily(1)?"
categories: Web
toc: true
---

* This blog is built soley dependent on Jekyll.

* This post refers to following pages
- <https://iingang.github.io/posts/windows-github-set/>

# From installing Jekyll to using Jekyll.
지금부터 이어지는 내용은 Window x64 기준으로 Jekyll을 사용하는 법을 서술한 내용이다.

***
## What is Jekyll(지킬)?
- Jekyll은 text 파일을 기반으로 정적 웹페이지를 만들 수 있는 서비스이다.
- Ruby 기반으로 실행되며, github page(github.io)와 연동이 잘 된다는 장점이 있다.
- 일반적으로 markdown 기반의 post를 배포한다.

***
## How to install Jekyll?
- Jekyll은 기본적으로 ruby, ruby-rails에 dependent하다. 버전의 안정성을 위하여 Ruby 2.6.0을 선정하는 것을 추천한다. 다음의 블로그를 참고하여 설치를 진행하였다.

1. Ruby installer로 설치 (v. 2.6.0)
2. Ruby install이 완료되었다면, <u> "Start command with Ruby Script </u> 를 열어 다음과 같은 명령어를 입력한다.
(gem은 python의 pip와 비슷한 기능을 하는 놈이라고 생각하면 된다.)

```Bash
gem install jekyll
gem install minima
gem install bundler
gem install jekyll-feed
gem install tzinfo-data
```

3. 위의 과정이 완료되었다면 다음을 입력한다.
```Bash
jekyll -v
```
jekyll version이 제대로 표시되었다면 설치가 완료된 것이다.

- [Install Jekyll](https://shryu8902.github.io/jekyll/jekyll-on-windows/)

***

## Jekyll Theme Download

Jekyll의 또다른 장점은 
bootstrap과 같이 이미 예쁘게 짜여진 template을 제공한다는 점이다.

[Jekyll Theme Page](http://jekyllthemes.org/)에 가서 마음에 드는 theme을 골라보자.

1. 마음에 드는 theme의 github page에 방문한 후 url을 복사한다.
2. 개인 github repository에서 {user_name}.github.io의 repository를 생성한다.
3. 이 때 `import your project to github`을 눌러서, 1에서 복사한 url을 붙여넣는다.
4. `Begin Import`를 하면, github이 해당 repository를 만들기 위한 optimizing 과정을 거친다.
5. {user_name}.github.io 도메인에 해당 홈페이지가 나타나는 것을 확인한다.
***

## Customize your blog 
1. 위에서 설정한 repository의 url을 기반으로 git clone을 받는다. 
{username}.github.io의 폴더가 나타날 것이다.
2. 해당 폴더로 이동
```Bash
cd {username}.github.io
```
3. 다음 명령어를 순차적으로 실행
```Bash
gem install tzinfo
gem install tzinfo-data
bundle install
bundle update
bundle install
```

bundle update는 GemLock 안에 써져 있는 내용을 기반으로 새로운 GemLock을 만들어내는 과정이다.

4. 다음 명령어를 실행하여 로컬 홈페이지를 열자
```Bash
bundle exec jekyll s
```

5. http://127.0.0.1:4000으로 접속

## Reflect change to your domain

1. github commit 후 push를 하면 당신의 도메인에 로컬에서 진행한 변경사항들이 반영된다.