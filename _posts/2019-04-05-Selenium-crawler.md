---
#layout: post
title: "Selenium을 이용한 크롤러 만들기"
categories: python
tags: python,selenium,PhantomJS
date: 2019-04-05 20:20:16
---

<h1>Selenium이란?</h1>
<p>주로 웹앱을 테스트하는데 이용하는 프레임워크다. webdriver라는 API를 통해 운영체제에 설치된 브라우저를 제어하게 된다.</p>

<h1>selenium 패키지 설치</h1>

{% highlight python %}
pip install selenium
{% endhighlight %}


<h1>PhantomJS 웹드라이버</h1>
<p>웹테스트를 위해 나온 headless browser이다. 우리가 사용하는 인터넷브라우저 처럼 보여지는 부분은 없다.
selenium이 사용하는 api를 제공하는 역활을 한다.</p>

다운로드링크
http://phantomjs.org/download.html

<h1>selenium으로 웹페이지 가져오기</h1>
<p>webdriver를 import 해준다.</p>
{% highlight python %}
from selenium import webdrver
{% endhighlight %}
