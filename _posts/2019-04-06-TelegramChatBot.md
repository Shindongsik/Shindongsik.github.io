---
title: "Django로 db에 저장하기"
categories: [python]
tags: [python,django,crawling]
date: 2019-04-05 23:17:00 +0200
read_time: false
---
<p>참조링크: https://beomi.github.io/gb-crawling/posts/2017-04-20-HowToMakeWebCrawler-Notice-with-Telegram.html </p>

## 무엇을 할것인가?
1. 텔레그램 봇을 만든다.
2. 웹크롤러를 만든다.
3. 웹크롤러와 텔레그램봇을 연결한다.
4. 크론텝으로 주기적으로 작동하게 한다.

## 텔레그램 봇 만들기
<p>참조링크: https://blog.psangwoo.com/coding/2016/12/08/python-telegram-bot-1.html </p>
<p>차근차근 따라하며, API token을 발급받는 부분까지 진행한다.</p>
> 토큰은 xxxxx:aaaaaaaaaaaaaaaaaaaaaaaaa 의 형태이다.

## python-telegram-bot 설치
<p>pip 설치한다.</p>
{% highlight python %}
pip install python-telegram-bot
{% endhighlight %}
