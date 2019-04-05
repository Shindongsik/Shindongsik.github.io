---
title: "Telegram 챗봇을 연결해보자"
categories: [python]
tags: [python,django,crawling]
date: 2019-04-05 23:17:00 +0200
read_time: false
---
[참조링크](https://beomi.github.io/gb-crawling/posts/2017-04-20-HowToMakeWebCrawler-Notice-with-Telegram.html){: target="_blank" }

## 무엇을 할것인가?
1. 텔레그램 봇을 만든다.
2. 웹크롤러를 만든다.
3. 웹크롤러와 텔레그램봇을 연결한다.
4. 크론텝으로 주기적으로 작동하게 한다.

## 텔레그램 봇 만들기
[참조링크](https://blog.psangwoo.com/coding/2016/12/08/python-telegram-bot-1.html){: target="_blank" }
<p>차근차근 따라하며, API token을 발급받는 부분까지 진행한다.</p>
> 토큰은 xxxxx:aaaaaaaaaaaaaaaaaaaaaaaaa 의 형태이다.

## python-telegram-bot 설치
<p>pip 설치한다.</p>
{% highlight python %}
pip install python-telegram-bot
{% endhighlight %}

## 크롤링 해서 첫번째글 파일에 저장
{% highlight %}
# 파일의 위치
BASE_DIR = os.path.dirname(os.path.abspath(__file__))

#클리앙 장터
req = requests.get('https://www.clien.net/service/board/sold')
req.encoding = 'utf-8' #Clien에서 encoding 정보를 보내주지 않아 encoding옵션을 추가해줘야합니다.

html = req.text
soup = BeautifulSoup(html, 'html.parser')
posts = soup.select('span.subject_fixed')
latest = posts[0].text  #셀렉트 한 것중 첫번째

with open(os.path.join(BASE_DIR, 'latest.txt'), 'r+', encoding='utf8') as f_read:
    before = f_read.readline()
    f_read.close()
    #저장된 글과 최신글이 다르면, 새글이 등록된것으로 판단한다.
    #새로운 글을 저장한다.
    if before != latest:
        bot.sendMessage(chat_id=chat_id, text='새 글이 올라왔어요.\n' + latest)
        with open(os.path.join(BASE_DIR, 'latest.txt'), 'w+', encoding='utf8') as f_write:
            f_write.write(latest)
            f_write.close()
{% endhighlight %}

## 코드에 텔레그램 봇 추가
{% highlight %}
import telegram

#텔레그램 봇
bot = telegram.Bot(token='xxxxxxx:aaaaaaaaaaaaaaaaaaaaaaaaaaaa')
#가장 마지막으로 bot에게 말을 건 사람의 id를 지정
#만약 IndexError 에러가 난다면 봇에게 메시지를 아무거나 보내고 다시 테스트
chat_id = bot.getUpdates()[-1].message.chat.id
{% endhighlight %}
