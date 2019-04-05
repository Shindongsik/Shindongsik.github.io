---
title: "Django로 db에 저장하기"
categories: [python]
tags: [python,django,crawling]
date: 2019-04-05 23:17:00
read_time: false
---
## Django 환경 불러오기
<p>장고환경을 불러오기 위해, 코드의 상단에 추가합니다.</p>
<p>
{% highlight python %}
import os
#DJANGO_SETTINGS_MODULE이라는 환경 변수에 현재 프로젝트의 settings.py파일 경로를 등록합니다.
os.environ.setdefault("DJANGO_SETTINGS_MODULE", "websaver.settings")
#이제 장고를 가져와 장고 프로젝트를 사용할 수 있도록 환경을 만듭니다.
import django
django.setup()
{% endhighlight %}
</p>
>코드를 단독 실행하더라도 Django를 통해 구동한 것 처럼 동작합니다.

## 크롤링한 결과를 object에 넣기
<p>크롤링한 결과를 딕셔너리로 만들어 array에 넣습니다. </p>
<p>
{% highlight python %}
array_items = []  #딕셔너리를 담을 array
for item in items:
    data = {}   #파싱한 값을 넣을 딕셔너리
    data['rank'] = item.find(class_='rank').get_text().replace(".","")
    data['title'] = item.find(class_='game-name col').get_text()
    data['score'] = item.find(class_='score col-auto').get_text()
    data['platform'] = item.find(class_='platforms col-auto').get_text()
    release_date = parse(item.find(class_='first-release-date col-auto').get_text()).date()
    data['release_date'] = release_date.strftime("%Y-%m-%d")
    array_items.append(data) #array에 추가한다
{% endhighlight %}
</p>

## 모델 객체를 사용해 db에 저장한다
<p>
{% highlight python %}
#위에서 생성한 array를 사용
for item in array_items:
    #모델객체의 파라미터로 각 컬럼의 값을 할당합니다.
    Gamescore(rank=item['rank'],title=item['title'],score=item['score'], \
    platform=item['platform'],release_date=item['release_date']).save()
{% endhighlight %}
</p>
>\는 코드가 길어져서 줄바꿈 했음을 나타냅니다.
