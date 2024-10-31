---
title: Jekyll Theme Chirpy로 Github 블로그 만들기
description: 고생하지마세요
date: 2024-10-31 01:57:00 +0900
categories: [jekyll]
tags: [github pages, github, jekyll, chirpy]
---

## 0. 알면 좋은 것  

나는 루비가 처음이여서 각 용어들이 너무 헷갈렸다.   
블로그를 만들면서 알아두면 좋을 것 같은 용어들을 정리했다.
- `Ruby` - 프로그래밍 언어
- `Gem`  - Ruby에서 제공하는 패키지 관리 도구
- `Jekyll` - 정적 사이트 생성기로 md를 html로 파싱해준다. Github 개발자가 개발함.
- `bundle` - Gem 설치 및 관리도구, Gemfile로 프로젝트 의존성을 관리

Javascript와 대응시켜 이해하자면

Ruby | Javascript
Gem | npm
Jekyll | Next.js
bundle | yarn, pnpm

_완전히 동일하지는 않지만_ 비슷한 느낌이라고 보면 된다.

## 1. 테마 다운로드 ( 레포지토리 생성 )

> Window 11에서 시도했을 때의 **수많은 에러**가 있었고, WSL을 이용해 `우분투` 환경에서 배포하는 방법을 선택했다.
{: .prompt-info}

기본적인 방법은 [jekyll-theme-chirpy](https://chirpy.cotes.page/posts/getting-started/)를 따라간다.

### 1.1 Option1의 경우 (쉬움, 권장)

Option1은 starter라는 레포지토리를 이용하는 방법이다.
단순히, 글을 빠르게 작성하는 환경을 만들고 싶다면, 이 방법을 추천한다고 한다.

1. [**starter**](https://github.com/cotes2020/chirpy-starter)로 이동한다
2. <kbd>Use this template</kbd>를 클릭하여 새로운 레포지토리를 만든다.
3. 레포지토리 이름은 `<github-id>.github.io` 형식으로 생성한다.

그후, _posts 폴더 내부에 `YYYY-MM-DD-post_name.md`와 같은 형식으로 파일을 만들어 글을 작성한다.

> 글을 작성하는 더 자세한 방법은 [jekyll에 글을 작성하는 법][how-to-write] 을 참고
{: .prompt-tip}

### 1.2 Option2의 경우 (우리가 할 것)
추후 chirpy 테마가 업데이트 되었을 때 직접 업데이트해야하고 의존성 관리를 직접해야하므로 권장하지 않는다고 하지만 나는 이걸로 골랐다.  

1. [fork][fork]로 이동해 Fork한다.
2. 레포지토리 이름은 `<github-id>.github.io` 형식으로 생성한다.

## 2. 환경 설정
> 레포지토리를 복사(생성)했다면 로컬에서 Jekyll을 관리할 수 있는 환경을 만들어야한다.

> WSL Ubuntu 22.04.4 LTS에서 진행하였다.
{: .prompt-info}

### 2.1 Ruby, Jekyll, Bundle, Node.js 설치

어떤 방법으로든 자신의 운영체제에 Ruby를 설치해야한다.

**`rbenv`**를 이용해서 설치해보자.

> Jekyll 공식에서 `apt-get install ruby-full`을 이용하는 방법은 ruby 버전이 2.x.x가 깔려서 chirpy와 호환이 되지 않았다 ...  
{: .prompt-warning}
<br/>
```terminal
$ sudo apt install git curl libssl-dev libreadline-dev zlib1g-dev autoconf bison build-essential libyaml-dev libreadline-dev libncurses5-dev libffi-dev libgdbm-dev
$ curl -sL https://github.com/rbenv/rbenv-installer/raw/main/bin/rbenv-installer | bash -
$ echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.zshrc
$ echo 'eval "$(rbenv init -)"' >> ~/.zshrc
$ source ~/.zshrc
```
<br/>
> `~/.zshrc` 부분은 만약 기본 셸이나 다른 셸을 사용하고 있다면 경로를 바꾸면 된다. 기본 셸은 `~/.bashrc`로 설정한다.  
필자는 zsh를 설치했기 때문에 `~/.zshrc`를 적어주었다.
{: .prompt-info}
<br/>
> `source ~/.zshrc`에서 에러가 발생했었지만, 무시해도 됐었다. docker 관련 에러였다.
{: .prompt-tip}
<br/>
```terminal
$ rbenv -v
```
rbenv가 설치가 되었는지 한번 확인해준다.

```terminal
$ rbenv install --list
```
설치 가능한 루비버전을 보여준다. 2024-10-31 기준, 나는 3.3.5버전을 선택했다.

```terminal
$ rbenv install 3.3.5
$ rbenv global 3.3.5
```

```terminal
$ echo 'export GEM_HOME="$HOME/gems"' >> ~/.zshrc
$ echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.zshrc
$ source ~/.zshrc
```
이번에는 Gem에 대한 경로를 설정해준다.

```terminal
$ gem install bundler jekyll
```

jekyll과 bundler를 설치한다.

마지막으로 Node.js도 설치해준다. Node.js의 설치는 여기서는 설명하지 않겠다.

### 2.2 로컬에 레포지토리 복사

```terminal
$ git clone [fork 한 레포지토리 주소]
```

### 2.3 테마 초기화

레포지토리 루트 경로에서 아래 명령어를 실행한다

```terminal
$ bash tools/init.sh
```

스크립트가 자동으로 초기화를 해준다.

### 2.4 로컬에서 Jekyll 서버 실행

```terminal
bundle
bundle exec jekyll s
```

위 명령어를 사용하면, 로컬 서버를 실행할 수 있다.
`bundle`은 레포지토리를 복사하고 한번 실행했다면 한번 더 실행할 필요는 없다.

이제 앞으로 `bundle exec jekyll s`를 통해서 로컬서버를 실행시킬 수 있다.

## 3. 기본 (필수) 설정

> 대부분의 설정은 _config.yml을 통해 진행된다.

url, avatar, timezone, lang 정도는 설정 해놓고, 다른 설정들은 비교적 간단(단순한 이름 입력, 이메일 입력)하다.

```yaml
# The Site Configuration

# Import the theme
theme: jekyll-theme-chirpy

# The language of the webpage › http://www.lingoes.net/en/translator/langcode.htm
# If it has the same name as one of the files in folder `_data/locales`, the layout language will also be changed,
# otherwise, the layout language will use the default value of 'en'.
lang: en

# Change to your timezone › https://kevinnovak.github.io/Time-Zone-Picker
timezone: Asia/Seoul

# jekyll-seo-tag settings › https://github.com/jekyll/jekyll-seo-tag/blob/master/docs/usage.md
# ↓ --------------------------

title: R3pic # the main title

tagline: Picsonic # it will display as the subtitle

description: >- # used by seo meta and the atom feed
  blog for me

# Fill in the protocol & hostname for your site.
# E.g. 'https://username.github.io', note that it does not end with a '/'.
url: "https://r3pic.github.io"
```

필요에 따라서 설정하면 된다.

> 하지만 **url**은 반드시 설정해야한다. 위의 단계를 따라 했다면, `https://레포지토리이름`형식으로 채워넣자.
{: .prompt-tip}

## 4. 배포

```terminal
git add .
git commit -m "chore: edit config"
git push origin master
```

이제 push하면 자동으로 배포가 진행되며 `https://자신의_깃허브_아이디.github.io`로 접속시 Chirpy가 적용된 블로그가 보이게 된다.

[how-to-write]: {{ site.baseurl }}/posts/how-to-write-post-with-chirpy
[fork]: https://github.com/cotes2020/jekyll-theme-chirpy/fork