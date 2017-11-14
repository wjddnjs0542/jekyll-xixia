---
layout: post
title: "Android JodaTime 시간 비교하기"
img: nevada.jpg
date: 2017-11-12 14:14:00 +0900
description: Android JodaTime 시간 비교하기
tag: [Android, JodaTime, Joda]
---
# JodaTime 시간 비교하기

지난 포스트에 이어 시간 클래스 가져오기1

[JodaTime - 이전 포스트](./2017/11/11/Joda-Time-Android.html)

- DateTime 클래스 생성

	{% highlight java %}
    //현재 시간 가져오기
    DateTime nowTime = DateTime.now();
    //특정 시간 가져오기
    DateTime time = new DateTime("2017-06-26T09:48:53.000Z");
    //UnixTime 으로 시간 가져오기
    DateTime unixTime = new DateTime(unixTimeStapm*1000);
    {% endhighlight %}