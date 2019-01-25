https://gist.github.com/ihoneymon/652be052a0727ad59601

This is a H1
============
This is a H2
------------
# This is a H1
## This is a H2
### This is a H3
#### This is a H4
##### This is a H5
###### This is a H6
####### This is a H7

> This is a first blockqute.
>> This is a second blockqute.
>>> This is a third blockqute.

> ### This is a H3
>> * List
>>> code

1. 첫번째
3. 세번째
2. 두번째


* 빨강
  * 녹색
    * 파랑

+ 빨강
  + 녹색
    + 파랑

- 빨강
  - 녹색
    - 파랑

* 1단계
    - 2단계
    	+ 3단계
            = 4단계

This is a normal paragraph:

    This is a code block.
end code block.

* * *

***

*****

- - -

---------------------------------------

[link keyword][id]
[id]: URL "Optional Title here"

Link: [Google][googlelink]
[googlelink]: https://google.com "Go google"

syntax: [Title](link)

<http://example.com/>
<address@example.com>

*single asterisks*
_single underscores_
**double asterisks**
__double underscores__
++underline++
~~cancelline~~

![Alt text](/path/to/img.jpg)
![Alt text](/path/to/img.jpg "Optional title")

사이즈 조절 기능은 없기 때문에 <img width="" height=""></img>를 이용한다.

https://heropy.blog/2017/09/30/markdown/

이텔릭체는 *별표(asterisks)* 혹은 _언더바(underscore)_를 사용하세요.
두껍게는 **별표(asterisks)** 혹은 __언더바(underscore)__를 사용하세요.
**_이텔릭체_와 두껍게**를 같이 사용할 수 있습니다.
취소선은 ~~물결표시(tilde)~~를 사용하세요.
<u>밑줄</u>은 `<u></u>`를 사용하세요.

1. 순서가 필요한 목록
1. 순서가 필요한 목록
  - 순서가 필요하지 않은 목록(서브) 
  - 순서가 필요하지 않은 목록(서브) 
1. 순서가 필요한 목록
  1. 순서가 필요한 목록(서브)
  1. 순서가 필요한 목록(서브)
1. 순서가 필요한 목록

- 순서가 필요하지 않은 목록에 사용 가능한 기호
  - 대쉬(hyphen)
  * 별표(asterisks)
  + 더하기(plus sign)


  
HEROPY
Tech
31%
MarkDown 사용법 총정리
September / 2017

html asciidoc md markdown 
마크다운(MarkDown)에 대해서 알고 계신가요?
파일 확장자가 .md로 된 파일을 보셨나요?
웹 개발을 하면서 아마 README.md라는 이름의 파일을 한 번은 보셨을텐데, 이 파일이 마크다운 문법으로 작성된 파일 입니다.

사용법이 매우 쉽고, 빠르게 문서를 정리할 수 있습니다.
물론 모든 HTML 마크업을 대신할 수 없기 때문에 지나친 의존보다는 쉽고 빠르게 작성하는 용도로 사용하세요.
마크다운과 비슷한 형태로 문법이 좀 더 복잡하지만 확장자가 .adoc인 AsciiDoc 문법도 있습니다. 좀 더 다양한 형태의 문서를 만들 수 있지만, 문법이 좀 더 복잡하고 지원 플랫폼이 적습니다.

우선 문법이 쉽고 다양한 플랫폼을 지원하는 마크다운 문법을 배우세요.
30분이면 충분합니다.

마크다운(MarkDown)에 대해서
마크다운의 장점
문법이 쉽다.
관리가 쉽다.
지원 가능한 플랫폼과 프로그램이 다양하다.
마크다운의 단점
표준이 없어 사용자마다 문법이 상이할 수 있다.
모든 HTML 마크업을 대신하지 못한다.
마크다운의 사용
메모장부터 전용 에디터까지 많은 곳에서 활용할 수 있습니다.
문법이 쉽기 때문에 꼭 전용 에디터를 사용할 필요는 없습니다만, 마크다운 코드의 하이라이트 효과를 원한다면 전용 에디터가 좋은 선택이 될 것 같네요.
저는 평소 Atom을 사용하고 있습니다.
혹은 마크다운 문법을 지원하는 모든 곳에서 사용할 수 있으며, 일반 블로그나 워드프레스 외 Slack이나 Trello 같은 서비스에서 메세지를 작성하듯 사용할 수도 있습니다.
화면에 표현되는 스타일(CSS)은 설정에 따라 달라집니다.
HTML과 마찬가지로 눈에 보이는 스타일은 무시하고 각 문법의 의미로 사용하세요.

마크다운 문법(syntax)
제목(Header)
<h1>부터 <h6>까지 제목을 표현할 수 있습니다.

# 제목 1
## 제목 2
### 제목 3
#### 제목 4
##### 제목 5
###### 제목 6
제목1(h1)과 제목2(h2)는 다음과 같이 표현할 수 있습니다.

제목 1
======

제목 2
------
강조(Emphasis)
각각 <em>, <strong>, <del> 태그로 변환됩니다.

밑줄을 입력하고 싶다면 <u></u> 태그를 사용하세요.

이텔릭체는 *별표(asterisks)* 혹은 _언더바(underscore)_를 사용하세요.
두껍게는 **별표(asterisks)** 혹은 __언더바(underscore)__를 사용하세요.
**_이텔릭체_와 두껍게**를 같이 사용할 수 있습니다.
취소선은 ~~물결표시(tilde)~~를 사용하세요.
<u>밑줄</u>은 `<u></u>`를 사용하세요.
이텔릭체는 별표(asterisks) 혹은 언더바(underscore)를 사용하세요.
두껍게는 별표(asterisks) 혹은 언더바(underscore)를 사용하세요.
이텔릭체와 두껍게를 같이 사용할 수 있습니다.
취소선은 물결표시(tilde)를 사용하세요.
밑줄은 <u></u>를 사용하세요.

목록(List)
<ol>, <ul> 목록 태그로 변환됩니다.

1. 순서가 필요한 목록
1. 순서가 필요한 목록
  - 순서가 필요하지 않은 목록(서브) 
  - 순서가 필요하지 않은 목록(서브) 
1. 순서가 필요한 목록
  1. 순서가 필요한 목록(서브)
  1. 순서가 필요한 목록(서브)
1. 순서가 필요한 목록

- 순서가 필요하지 않은 목록에 사용 가능한 기호
  - 대쉬(hyphen)
  * 별표(asterisks)
  + 더하기(plus sign)
순서가 필요한 목록
순서가 필요한 목록
순서가 필요하지 않은 목록(서브)
순서가 필요하지 않은 목록(서브)
순서가 필요한 목록
순서가 필요한 목록(서브)
순서가 필요한 목록(서브)
순서가 필요한 목록
순서가 필요하지 않은 목록에 사용 가능한 기호
대쉬(hyphen)
별표(asterisks)
더하기(plus sign)
링크(Links)
<a>로 변환됩니다.

[GOOGLE](https://google.com)

[NAVER](https://naver.com "링크 설명(title)을 작성하세요.")

[상대적 참조](../users/login)

[Dribbble][Dribbble link]

[GitHub][1]

문서 안에서 [참조 링크]를 그대로 사용할 수도 있습니다.

다음과 같이 문서 내 일반 URL이나 꺾쇠 괄호(`< >`, Angle Brackets)안의 URL은 자동으로 링크를 사용합니다.
구글 홈페이지: https://google.com
네이버 홈페이지: <https://naver.com>

[Dribbble link]: https://dribbble.com
[1]: https://github.com
[참조 링크]: https://naver.com "네이버로 이동합니다!"

![대체 텍스트(alternative text)를 입력하세요!](http://www.gstatic.com/webp/gallery/5.jpg "링크 설명(title)을 작성하세요.")

![Kayak][logo]

[logo]: http://www.gstatic.com/webp/gallery/2.jpg "To go kayaking."

[![Vue](/images/vue.png)](https://kr.vuejs.org/)

`background`혹은 `background-image` 속성으로 요소에 배경 이미지를 삽입할 수 있습니다.

인용문(blockQuote)

> 남의 말이나 글에서 직접 또는 간접으로 따온 문장.
> _(네이버 국어 사전)_

BREAK!

> 인용문을 작성하세요!
>> 중첩된 인용문(nested blockquote)을 만들 수 있습니다.
>>> 중중첩된 인용문 1
>>> 중중첩된 인용문 2
>>> 중중첩된 인용문 3

<u>마크다운에서 지원하지 않는 기능</u>을 사용할 때 유용하며 대부분 잘 동작합니다.

<img width="150" src="http://www.gstatic.com/webp/gallery/4.jpg" alt="Prunus" title="A Wild Cherry (Prunus avium) in flower">

![Prunus](http://www.gstatic.com/webp/gallery/4.jpg)

---
(Hyphens)

***
(Asterisks)

___
(Underscores)

동해물과 백두산이 마르고 닳도록 
하느님이 보우하사 우리나라 만세   <!--띄어쓰기 2번-->
무궁화 삼천리 화려 강산<br>
대한 사람 대한으로 길이 보전하세

