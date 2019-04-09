---
title: "AWS ec2에 LAMP스택을 설치해 봅시다."
categories: [aws]
tags: [ec2,lamp,web]
date: 2019-04-09 22:05:00 +0200
read_time: false
release_date: true
---
[참고문서](https://docs.aws.amazon.com/ko_kr/AWSEC2/latest/UserGuide/install-LAMP.html){:target='_blank'}

## 무엇을 할 것 인가?
1. aws콘솔에서 Amazon Linux AMI 인스턴스를 생성한다.
2. ssh클라이언트(putty)를 사용해서 생성한 인스턴스에 접속한다.
3. yum 패키지관리 프로그램을 업데이트 한다.
4. 각각의 패키지를 설치한다.
5. 보안규칙을 수정한다.
6. 아파치 작동 테스트
7. php 작동 테스트
8. mysql 작동 테스트

## ec2 인스턴스 생성
aws관리 콘솔의 ec2 항목에서 인스턴스 시작을 클릭하면, os를 선택하는 화면이 나온다. Amazon Linux AMI 를 선택

인스턴스 유형 선택 화면에서, 적당한 것을 선택(성능이 좋을수록 비싸다)

암호키를 새로 생성하고, 다운로드 받는다.

생성 완료

## putty 사용
[참고문서](https://docs.aws.amazon.com/ko_kr/AWSEC2/latest/UserGuide/putty.html){:target='_blank'}

참고문서를 차근차근 따라한다.(puttycm 을 사용하면 좀더 편하다.)

사용자 이름에 유의한다
![사용자이름](/assets/images/aws-ec2-username.PNG)

## yum 업데이트
모든 패키지를 최신버전으로 업데이트 한다.

{% highlight python %}
sudo yum update -y
{% endhighlight %}

## 패키지 설치
{% highlight python %}
sudo yum install -y httpd24 php70 mysql56-server php70-mysqlnd
{% endhighlight %}

>예시는 최신 버전이 아닐수 있다. 각자 알맞  버전을 선택하자.    
