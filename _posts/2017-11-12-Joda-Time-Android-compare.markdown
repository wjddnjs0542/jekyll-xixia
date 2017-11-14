---
layout: post
title: "Android JodaTime 시간 비교하기"
img: nevada.jpg
date: 2017-11-12 14:14:00 +0900
description: Android JodaTime 시간 비교하기
tag: [Android, JodaTime, Joda]
---
# JodaTime 시간 비교하기

[JodaTime - 이전 포스트](/2017/11/11/Joda-Time-Android.html)

지난 포스트에 이어 시간 클래스 가져오기

- #### DateTime 클래스 생성

	{% highlight java %}
    //현재 시간 가져오기
    DateTime nowTime = DateTime.now();
    //특정 시간 가져오기
    DateTime time = new DateTime("2017-06-26T09:48:53.000Z");
    //UnixTime 으로 시간 가져오기
    DateTime unixTime = new DateTime(unixTimeStapm*1000);
    {% endhighlight %}

- #### 비교 대상 시간 가져오기

	##### 시간 비교하기 위한 클래스 중 Duration 클래스를 설명
    ###### 2개의 시간 차이를 비교하기 위해 사용하는 클래스
    ###### 생성 방법은 다음과 같이 사용할 수 있다.
    ###### ex) new Duration((long)이전시간, (long)현재시간)
    ###### ex2) new Duration((ReadableInstant)이전시간, (ReadableInstant)현재시간)
    ###### 이전시간, 현재시간을 뒤집어 사용하면 값이 음수로 나올 수 있음.

	{% highlight java %}
    //DateTime 객체를 활용한 생성
    Dutation duration = new Duration(DateTime, DateTime);
    //DateTime의 toInstant 메서드를 활용한 생성
    Duration duration = new Duration(time.toInstant(), DateTime.now().toInstant());
    //long 형태의 시간을 활용한 생성
    Duration duration = new Duration(123456, 456789);
    {% endhighlight %}

- #### 비교할 시간 가져오기

	##### 비교한 시간의 일(day), 시간(hour), 분(minute), 초(second)의 차이를 가져올 수 있다.

	{% highlight java %}
    //일(Day) 차이 가져오기
    duration.toStandardDays().getDays();
    //시(Hour) 차이 가져오기
    duration.toStandardHours().getHours();
    //분(Minute) 차이 가져오기
    duration.toStandardMinutes().getMinutes();
    //초(Second) 차이 가져오기
    duration.toStandardSeconds().getSeconds();
    {% endhighlight %}

- #### 다른 방법으로 비교할 시간 가져오기

	##### Duration 객체를 생성하지 않고 Static 함수를 이용해 비교 시간을 가져오는 방법
    ###### Years, Months, Days, Hours, Minutes, Seconds 의 Between 메서드를 활용해 가져오는 방법

	{% highlight java %}
    //년도(Year) 차이 가져오기
    Years.yearsBetween();
    //월(Month) 차이 가져오기
    Months.monthsBetween();
    //일(Day) 차이 가져오기
    Days.daysBetween();
    //시간(Hour) 차이 가져오기
    Hours.hoursBetween();
    //분(Minute) 차이 가져오기
    Minutes.minutesBetween();
    //초(Second) 차이 가져오기
    Seconds.secondsBetween();
    {% endhighlight %}