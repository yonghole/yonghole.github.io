---
title: "Semantic HTML"
date: 2021-01-06 03:05:44
categories: Web
---


# Semantic HTML

HTML5 이전에는 웹 페이지의 구조를 표현하는 태그가 없었기 때문에 구조화된 페이지를 만들기 어려웠다. <div>, <table> 등의 태그를 이용해 구조화된 것처럼 표현했지만, 막상 소스를 보면 구조의 파악이 힘들었다. 

구조화된 문서는 보기에 좋다는 장점도 있지만, 웹 페이지 내의 정보 탐색이 중요하다는 이유도 있다. 검색 엔진이 페이지 내의 정보를 잘 탐색할 수 있도록 구조화된 웹 사이트를 만들어야 한다. HTML5 이전의 태그는 부분 부분으로는 어떤 내용인지 표현할 수 있었지만 전체적인 구조를 표현할 수 없었다. 검색 엔진에게 페이지가 어떤 주제를 가지고 있는지, 목차는 어디에 있는지와 같은 정보를 알려주자면 전체적인 구조 정보, 즉 context를 알아야 한다. 

HTML5 에서는 이런 문제를 해결하기 위해 문서의 구조를 의미하는 태그를 추가하였다. 검색 엔진은 웹 페이지에서 <header> <nav> <section> <article> 등의 태그를 찾고, 이를 기반으로 다양한 검색 결과를 제공한다. 

Semantic HTML의 활용 예로, 애플의 watchOS는 article 태그를 이용해 페이지의 본문을 파악한다고 한다. 

*watchOS 5 brings web content to Apple Watch by rendering rich HTML in Messages and Mail. Gain insights into how watchOS maintains compatibility with existing web content, and find out what you can do to optimize your web content for Apple Watch.*

### Header

<header> 태그는 페이지나 섹션의 머리말을 표현하는 태그이다. 보통 페이지 제목, 페이지를 소개하는 간단한 설명이 들어간다. 

### Nav

<nav> 태그는 하이퍼링크들을 모아 놓은 특별한 섹션이다. 페이지 내의 목차를 위해 사용한다. 

### Section

<section> 태그는 문서의 chapter 역할을 한다. 일반적인 문서에 여러 장이 있는 것처럼 웹페이지에도 여러 section을 둘 수 있다. <section> 에는 heading tag로 section의 주제를 기재한다. 

### Article

<article> 태그는 독립적인 내용을 담는데 사용한다. article에 담을 내용이 많은 경우 여러 개의 section에 나누어 담을 수 있다. 

### Section vs Article

Section 과 article의 차이에 대해서는 여러 의견이 분분한 것 같다. 처음에는 section 안에 article 들을 넣는 것만 가능한 줄 알았다. 예를 들어, 

```html
<section>
	<article>
			<h3> Article 1 </h3>
	</article>
	<article>
			<h3> Article 2 </h3>
	</article>
	<article>
			<h3> Article 3 </h3>
	</article>
</section>
```

와 같은 방법으로만 사용할 수 있는 줄 알았다. 하지만 article 내에 section을 넣어서 사용할 수도 있다고 한다. 다만 분명히 해야 하는 것은, article은 독립적인 요소를 사용할 때, section은 논리적으로 관계 있는 문서 혹은 요소에 사용해야 한다는 것이다. 

>> 전체 맥락에서 보면 큰 단락(주제)를 독립된 <article> 들로 나누고 <article> 내부에서 독립된 소주제들을 <section> 으로 나누는 것이 더 적합하지 않은가 하는 생각이 드는데, 정답은 없는 것 같다. 다만 HTML5+CSS3+Javascript 웹 프로그래밍(황기태 저, 생능출판) 에서는 <section> 내에 <article> 이 들어가는 것으로 소개하였다. 

### Aside

사이드 바 역할을 하는 태그이다. 문서의 주요 흐름이나 부분에서 벗어난 내용을 담고, 오쪼ㅛㄱ이나 왼쪽에 주로 배치한다. 

### Footer

<footer>는 꼬리말 영역을 표시하는 태그로, 페이지나 <section> 내에 꼬리말을 담는다. 다만 반드시 문서의 말미에 배치되어야 할 필요는 없다. 

### Semantic Block Tags

**Figure**

본문에 삽입되는 사진, 차트, 삽화 등을 블록화 하는 시맨틱 태그이다. <figure> 태그를 통해 콘텐츠를 블록화 할 수 있다. 

![_2021-01-06__2 43 50](https://user-images.githubusercontent.com/55180768/103682162-d4ad1380-4fcb-11eb-9b2f-b7dc38804ad4.png)

**Details & Summary**

상세 정보를 담는 시맨틱 블록 태그이다. 토글 버튼이 나타나고, 클릭하여 확장할 수 있다. 

Summary 에는 제목이, details에는 제목을 눌렀을 때 나타날 내용이 들어간다. 

---

![_2021-01-06__2 45 57](https://user-images.githubusercontent.com/55180768/103682177-d8409a80-4fcb-11eb-8e9d-06b15748be18.png)

확장 전 

---

![_2021-01-06__2 46 14](https://user-images.githubusercontent.com/55180768/103682178-d8409a80-4fcb-11eb-93cb-fd04d349c845.png)

확장 후 

**인라인태그**

텍스트를 마크업 해 보기 쉽게 나타내주는 태그들도 존재한다. 직관적이기 때문에 코드와 결과만 봐도 이해할 수 있다. 

- mark
- time
- meter
- progress

![_2021-01-06__2 51 36](https://user-images.githubusercontent.com/55180768/103682179-d8d93100-4fcb-11eb-9f1e-3c2748ee8973.png)

![_2021-01-06__2 52 23](https://user-images.githubusercontent.com/55180768/103682180-da0a5e00-4fcb-11eb-8e7d-ab43161d8c7c.png)
