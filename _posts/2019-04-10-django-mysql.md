---
title: "django에 mysql 연결하기"
categories: [django]
tags: [django,mysql,ubuntu]
date: 2019-04-10 17:15:00 +0200
read_time: false
---
>ubuntu에 mysql이 설치 되있어야 합니다.

## django mysql 연동패키지 설치
{% highlight python %}
sudo apt-get install python3-dev libmysqlclient-dev
sudo pip3 install mysqlclient

#pip3설치가 안된경우
sudo apt-get install python3-pip
{% endhighlight %}

[장고공식문서](https://docs.djangoproject.com/en/2.2/ref/databases/#mysql-db-api-drivers){:target='_blank'}

## django 설정파일 수정
{% highlight python %}
sudo vim /home/ubuntu/django/mysite/setting.py
{% endhighlight %}

>기존의 sqlite3는 주석처리

{% highlight python %}
DATABASES = {
    'default': {
        #'ENGINE': 'django.db.backends.sqlite3',
        #'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'my_db', # DB명
        'USER': 'root', # 데이터베이스 계정
        'PASSWORD': 'pw1234', # 계정 비밀번호
        'HOST': 'localhost', # 데이테베이스 주소(IP)
        'PORT': '3306', # 데이터베이스 포트(보통은 3306)
        'OPTIONS': {
            'init_command': 'SET sql_mode="STRICT_TRANS_TABLES"'
        }
    }
}
{% endhighlight %}

## 마이그레이션하고, 장고서버 시작
{% highlight python %}
python manage.py migrate
python manage.py runserver 0.0.0.0:8000
{% endhighlight %}
