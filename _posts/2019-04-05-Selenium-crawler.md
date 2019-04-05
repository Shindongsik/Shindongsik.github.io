---
#layout: post
title: "Selenium을 이용한 크롤러 만들기"
categories: [python]
tags: [python,selenium,PhantomJS]
date: 2019-04-05
---

<h3>Selenium이란?</h3>
<p>주로 웹앱을 테스트하는데 이용하는 프레임워크다. webdriver라는 API를 통해 운영체제에 설치된 브라우저를 제어하게 된다.</p>

<h3>selenium 패키지 설치</h3>
<p>
{% highlight python %}
pip install selenium
{% endhighlight %}
</p>

<h3>PhantomJS 웹드라이버</h3>
<p>웹테스트를 위해 나온 headless browser이다. 우리가 사용하는 인터넷브라우저 처럼 보여지는 부분은 없다.
selenium이 사용하는 api를 제공하는 역활을 한다.</p>
<p>[phantomJS 다운로드링크](http://phantomjs.org/download.html)</p>

<h3>selenium으로 웹페이지 가져오기</h3>
<p>webdriver를 import 해준다.</p>
<p>
{% highlight python %}
from selenium import webdriver
{% endhighlight %}
</p>
<p>webdriver 객채를 만들어준다.</p>
<p>
{% highlight python %}
#아까 받은 PhantomJS의 위치를 지정해준다.
driver = webdriver.PhantomJS('/home/ubuntu/django/phantomjs/bin/phantomjs')
#크롤링할 url입력
driver.get('https://www.opencritic.com/browse/all/2019/score')
html = driver.page_source
#bs4를 사용해 파싱
soup = BeautifulSoup(html, 'html.parser')
{% endhighlight %}
</p>

>크롤링에 성공했다면, bs4를 이용한 파싱은 이전과 같다.

>phantimJS를 사용한 코드를 실행하면 deprecated 경고가 뜨는데 작동은 잘한다. 그래도 찜찜하니, 다음번엔 크롬 웹드라이버를 사용한 크롤링을 해보자.