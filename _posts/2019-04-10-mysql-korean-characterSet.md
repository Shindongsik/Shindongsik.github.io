---
title: "mysql에 한글설정 하기"
categories: [mysql]
tags: [mysql,ubuntu]
date: 2019-04-10 16:05:00 +0200
read_time: false
---
>os는 우분투 라고 가정합니다.

## mysql을 설치 합니다.
{% highlight python %}
sudo apt-get install mysql-server-5.7
{% endhighlight %}

## 설정파일에 한글설정
{% highlight python %}
sudo vim /etc/mysql/my.cnf
{% endhighlight %}

다음을 추가해 줍니다.

{% highlight python %}
[client]
default-character-set=utf8mb4

[mysql]
default-character-set=utf8mb4

[mysqld]
collation-server = utf8mb4_unicode_ci
init-connect='SET NAMES utf8mb4'
character-set-server = utf8mb4
{% endhighlight %}

## 비번 설정
{% highlight python %}
sudo mysql -u root -p
{% endhighlight %}
>처음엔 비번설정이 안되있기 때문에, 비번입력칸에 그냥 엔터를 눌러줍니다.

{% highlight mysql %}
#생성된 db 리스트
show databsaes;
#mysql db를 사용
use mysql;
#비번 설정 쿼리
alter user 'root'@'localhost' identified with mysql_native_password by '비밀번호';
#권한 적용
flush privileges;
#사용할 db생성
CREATE DATABASE my_db DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
#쿼리콘솔에서 나간다
exit
{% endhighlight %}

## mysql 재시작
{% highlight python %}
sudo service mysql restart
{% endhighlight %}

>mysql을 설치하자 마자 설정하는 것을 권장합니다.(문자셋 설정을 나중에 하면, 난처한 일이 많이 발생합니다.)
