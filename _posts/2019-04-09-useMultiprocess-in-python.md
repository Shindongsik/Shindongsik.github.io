---
title: "크롤링에 멀티프로세스를 이용해 보자"
categories: [python]
tags: [python,multiprocess,crawling]
date: 2019-04-09 13:55:00 +0200
read_time: false
---
[참고문서](https://beomi.github.io/gb-crawling/posts/2017-07-05-HowToMakeWebCrawler-with-Multiprocess.html){:target='_blank'}

## 멀티프로세스?
<p>간단하게 말해서, 멀티프로세스란 프로그램을 여러개 실행하는 것입니다.</p>
<p>예를 들어 크롤링 해야하는 페이지가 1000 페이지 라고 할때, 동시에 5개의 프로그램을 실행해서 각각 200 페이지씩 크롤링 한다면, 좀더 효과적이고 빠르게 완료 할수 있다는 개념 입니다.</p>

## 하나씩 크롤링 하기
<p> 먼서 리스트에서 링크를 추출해서, 각각의 상세 페이지를 파싱하는 프로그램입니다.</p>
<p>
{% highlight python %}
import requests
from bs4 import BeautifulSoup
import time

#리스트에서 링크를 추출합니다.
def get_links():
    req = requests.get('https://www.clien.net/service/board/sold?category=%ED%8C%90%EB%A7%A4')
    req.encoding = 'utf-8' # Clien에서 encoding 정보를 보내주지 않아 encoding옵션을 추가해줘야합니다.
    html = req.text
    soup = BeautifulSoup(html, 'html.parser')
    table = soup.find(class_="content_list")
    posts = table.find_all(class_="list_item symph_row")

    links = []
    for post in posts:
        links.append(post.find('a', class_='list_subject').get('href'))

    return links

#상세페이지를 크롤링 합니다.
def get_content(link):
    abs_link = 'https://www.clien.net' + link
    req = requests.get(abs_link)
    html = req.text
    soup = BeautifulSoup(html, 'html.parser')
    #여기서는 그냥 제목만 출력
    print(soup.find(class_='post_subject').get_text().replace('판매\n',''))

if __name__ == '__main__':
    start_time = time.time()

    #멀티프로세스 안 사용
    links = get_links()
    for link in links:
        get_content(link)

    print('--- %s seconds ---' %(time.time() - start_time))
{% endhighlight %}
</p>
<p> 실행 환경 마다 다르겠지만, 저의 경우 약 6.0초가 걸렸습니다. </p>

## multiprocess 크롤링 하기
<p>이번에는 멀티프로세스를 사용해서 크롤링을 병렬화 해봅시다.</p>
<p>파이썬의 multiprocessing 패키지에서 Pool 을 import 해 줍니다.</p>
<p>
{% highlight python %}
import requests
from bs4 import BeautifulSoup
import time
from multiprocessing import Pool

#리스트에서 링크를 추출합니다.
def get_links():
    req = requests.get('https://www.clien.net/service/board/sold?category=%ED%8C%90%EB%A7%A4')
    req.encoding = 'utf-8' # Clien에서 encoding 정보를 보내주지 않아 encoding옵션을 추가해줘야합니다.
    html = req.text
    soup = BeautifulSoup(html, 'html.parser')
    table = soup.find(class_="content_list")
    posts = table.find_all(class_="list_item symph_row")

    links = []
    for post in posts:
        links.append(post.find('a', class_='list_subject').get('href'))

    return links

#상세페이지를 크롤링 합니다.
def get_content(link):
    abs_link = 'https://www.clien.net' + link
    req = requests.get(abs_link)
    html = req.text
    soup = BeautifulSoup(html, 'html.parser')
    #여기서는 그냥 제목만 출력
    print(soup.find(class_='post_subject').get_text().replace('판매\n',''))

if __name__ == '__main__':
    start_time = time.time()

    #멀티 프로세스 사용
    pool = Pool(processes=4)    #4개의 프로세스 사용
    pool.map(get_content, get_links())  #map(실행메소드, 파라미터)
    pool.close()    #리소스 낭비 방지
    pool.join()     #작업완료 대기

    print('--- %s seconds ---' %(time.time() - start_time))

{% endhighlight %}
</p>
<p>약 1.7초, 3배정도 성능이 향상 되었습니다.</p>

>멀티프로세싱으로 크롤링 할 때, Pool 생성시 processes의 개수를 계속 늘린다고 속도가 계속 빨라지는 것은 아닙니다.

>웹사이트 공격으로 인식되어 차단 될수 있습니다.
