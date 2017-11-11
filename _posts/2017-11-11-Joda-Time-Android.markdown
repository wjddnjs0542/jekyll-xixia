---
layout: post
title: "Android JodaTime 사용방법"
img: nevada.jpg 
date: 2017-11-11 23:28:00 +0900
description: Android JodaTime 사용방법
tag: [Android, JodaTime, Joda]
---
# JodaTime

- Java의 Date 와 Calendar 클래스의 불편함을 해소하기 위해 나온 라이브러리

#### [Joda-Time-Android Github](https://github.com/dlew/joda-time-android)

## Android 사용방법

- Application 클래스 작성하기
###### Application 을 상속받는 클래스를 작성한다.
###### Application 을 상속받는 클래스의 onCreate에 Jodatime을 사용할 수 있도록 셋팅을 해준다.

    {% highlight java %}
    public class CustomApplication extends Application{

        @Override
        public void onCreate(){
            super.onCreate();
            JodaTimeAndroid.init(Context);
        }
    }
    {% endhighlight %}

- Manifest에 Application 클래스 등록하기

	{% highlight xml %}
    <application
    	android:name="packge.CustomApplication"/>
        ...
    </application>
    {% endhighlight %}

- 시간 등록하기


