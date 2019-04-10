---
title: "Ubnutu에 Django를 설치해보자"
categories: [python]
tags: [python,django,ubuntu]
date: 2019-04-10 12:55:00 +0200
read_time: false
---
## 무엇을 할것인가?
1. ubuntu 인스턴스 만들기
2. apt 업데이트
3. python 설치
4. django 설치
5. 테스트

## ubuntu 인스턴스 만들기
aws매니저콘솔의 서비스에서 ec2를 선택합니다.

인스턴스시작 에서 우분투를 선택합니다.

인스턴스생성이 완료되면, 보안그룹에서 8000번 포트를 오픈합니다.(장고의 테스트 웹서버에서 사용)

## apt 업데이트
apt의 관리패키지 리스트 업데이트

{% highlight python %}
sudo apt update
{% endhighlight %}

apt 패키지를 최신버전으로 업그레이드

{% highlight python %}
sudo apt upgrade
{% endhighlight %}

>중간에 나오는 질문은 y 또는 ok 해줍니다.

## 파이썬 설치
이미 설치 되어 있을수 있습니다. 확인해봅니다.

{% highlight python %}
python3 --version
{% endhighlight %}

설치되어 있지 않다면, 설치해 줍니다.(버전은 자신에게 알맞은 것으로 설치)

{% highlight python %}
sudo apt install python3.6
{% endhighlight %}

## 장고 설치
[참고문서1](https://tutorial.djangogirls.org/ko/django_installation/){:target='_blank'}

장고 폴더를 만들어 줍니다.

{% highlight python %}
mkdir django
cd django
{% endhighlight %}

가상환경 패키지를 설치 합니다.

{% highlight python %}
sudo apt install python3-venv
{% endhighlight %}

가상 환경을 만들어 줍니다.

{% highlight python %}
python3 -m venv my_venv
{% endhighlight %}

가상 환경 실행

{% highlight python %}
source my_venv/bin/activate
{% endhighlight %}

>콘솔의 프롬프트 앞에(my_venv)접두어가 붙어있다면 virtualenv가 시작되었음을 알 수 있습니다.

>가상환경 종료는 deactivate

pip 설치

{% highlight python %}
python3 -m pip install --upgrade pip
{% endhighlight %}

장고 설치

{% highlight python %}
pip install django==2.2
{% endhighlight %}

## 장고 테스트
[참고문서2](https://tutorial.djangogirls.org/ko/django_start_project/){:target='_blank'}

장고 프로젝트를 만듭니다.

{% highlight python %}
django-admin startproject mysite .
{% endhighlight %}

설정 변경

{% highlight python %}
sudo vim mysite/settings.py

#아래 내용을 에디터 안에서 수정
ALLOWED_HOSTS = ['퍼블릭ip', '퍼블릭dns']

LANGUAGE_CODE = 'ko-kr'

TIME_ZONE = 'Asia/Seoul'

STATIC_URL = '/static/'
STATIC_ROOT = os.path.join(BASE_DIR, 'static')
{% endhighlight %}

장고 웹서버 시작

{% highlight python %}
python manage.py runserver 0.0.0.0:8000
{% endhighlight %}

>웹브라우저로 접속해서, 장고 기본페이지가 보이면 성공입니다.
