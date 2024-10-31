---
title: Chirpy 문법으로 블로그 게시글 작성하기
description: 글을 작성해보자
date: 2024-10-31 01:57:00 +0900
categories: [jekyll]
tags: [github pages, github, jekyll, chirpy]
---

## 1. Front Header (필수 작성)

```markdown
---
title:       Chirpy 문법으로 블로그 게시글 작성하기    # 게시글 제목
description: 고생하지마세요.                          # 게시글 설명
date:        2024-10-30 11:33:00 +0900               # 날짜 및 시간 (한국 시간은 +0900 적용)
categories:  [blog, post]                            # 카테고리 (2개 이상 작성시 트리 구조)
tags:        [github pages, github, jekyll]          # 태그 목록
pin:         true                                    # 게시글 고정
---

# 게시글 본문은 Markdown 문법으로 작성하면 된다.
```

## 2. 게시글 본문 작성하기

처음보는 것들을 주로 정리한다.

### 인용 (정보)

```markdown
> 테스트 인용 정보
{: .prompt-info}
```

> 테스트 인용 정보
{: .prompt-info}

### 인용 (팁)

```markdown
> 테스트 인용 팁
{: .prompt-tip}
```

> 테스트 인용 팁
{: .prompt-tip}

### 인용 (경고)

```markdown
> 테스트 인용 팁
{: .prompt-warning}
```

> 테스트 인용 경고
{: .prompt-warning}

### 인용 (위험)

```markdown
> 테스트 인용 팁
{: .prompt-danger}
```

> 테스트 인용 경고
{: .prompt-danger}

### 키보드 감싸기

```markdown
<kbd>감싸기</kbd>
```

<kbd>감싸기</kbd>

# 경로 변수 선언
```markdown
[변수사용한 url][example]  
[그냥 url](https://example.com)

// 변수 선언은 주로 맨 아래로 몰아서 선언한다
[example]: https://example.com
```

[변수사용한 url][example]  
[그냥 url](https://example.com)

# 이미지
```markdown
![img-description](/path/to/image){: w="512" h="512" }
_Image Caption_
```

![img-description](assets/img/uploads/test_image.png){: w="512" h="512" }
_Image Caption_

# 영상 임베드
{% raw %}
```liquid
{% include embed/{Platform}.html id='{ID}' %}
```
{% endraw %}

Platform 종류
- `youtube`
- `twitch`

{% include embed/youtube.html id='KvMY1uzSC1E' %}

[example]: https://example.com