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

- 시간 클래스 가져오기

	{% highlight java %}
    //현재 시간 가져오기
    DateTime nowTime = DateTime.now();
    //특정 시간 가져오기
    DateTime time = new DateTime("2017-06-26T09:48:53.000Z");
    //UnixTime 으로 시간 가져오기
    DateTime unixTime = new DateTime(unixTimeStapm*1000);
    {% endhighlight %}

- 시간 가져오기

	{% highlight java %}
    //년 가져오기
    nowTime.year().get()
    nowTime.get(DateTimeFieldType.year())
    nowTime.getYear();

    //월 가져오기
    nowTime.monthOfYear().get()
    nowTime.get(DateTimeFieldType.monthOfYear())
    nowTime.getMonthOfYear();

    //일 가져오기
    nowTime.dayOfMonth().get()
    nowTime.get(DateTimeFieldType.dayOfMonth())
	nowTime.getDayOfMonth();

    //시 가져오기
    nowTime.hourOfDay().get()
    nowTime.get(DateTimeFieldType.hourOfDay())
    nowTime.getHourOfDay();

    //분 가져오기
    nowTime.minuteOfHour().get()
    nowTime.get(DateTimeFieldType.minuteOfHour())
    nowTime.getMinuteOfHour();

    //초 가져오기
    nowTime.secondOfMinute().get()
    nowTime.get(DateTimeFieldType.secondOfMinute())
    nowTime.getSecondOfMinute();

    {% endhighlight %}

- 기타 시간 가져오기

	{% highlight java %}
    //기원 전 후 가져오기
    nowTime.era().get()

    //세기 가져오기
    nowTime.centuryOfEra().get()

    //세기에 포함된 년 가져오기
    nowTime.yearOfCentury().get()

    //기원 후 년 가져오기
    nowTime.yearOfEra().get()

    //년도 가져오기
    nowTime.weekyear().get()

    //해당년도 몇번째 주?
    nowTime.weekOfWeekyear().get()

    //그 년에 몇번째 일
    nowTime.dayOfWeek().get()

    //그 주에 몇번째 일
    nowTime.dayOfYear().get()

    //그 날의 몇 분째
    nowTime.minuteOfDay().get()

    //그 날의 몇 초째
    nowTime.secondOfDay().get()

	{% endhighlight %}

- 가져오고 싶은 패턴대로 가져오기
###### DateTimeFormat에 Pattern을 원하는 입맛대로 등록(패턴은 아래 표 참조)
###### DateTime 객체의 toString메서드에 Format을 넣어 반환 받기
###### 원하는 Format의 시간을 구할 수 있음.
###### ※응용하면 Format으로 년 월 일 시 분 초 (AM/PM) 등도 따로 분리할 수 있음

	{% highlight java %}
    DateTimeForamt ff = DateTimeFormat.forPattern("yyyy.MM.dd aa hh:mm:ss")
    now.toString(ff)
    {% endhighlight %}

- 패턴 표

![symbol](/assets/images/jodatime-symbol.png)

<!-- | Symbol | Meaning | Presentation | Example | -->
<!-- |--------|--------|--------|--------| -->
<!-- | G | era | text | AD | -->
<!-- | C | century of era | number | 20 | -->
<!-- | Y | year of era | year | 2017 | -->
<!-- | x | weekyear | year | 2017 | -->
<!-- | w | week of weekyear | number | 27 | -->
<!-- | e | day of week | number | 2 | -->
<!-- | E | day of week | text | Tuesday; Tue | -->
<!-- | y | year | year | 2017 | -->
<!-- | D | day of year | number | 189 | -->
<!-- | M | month of year | month | July; Jul; 07 | -->
<!-- | d | day of month | number | 10 | -->
<!-- | a | halfday of day | text | PM | -->
<!-- | K | hour of halfday(0~11) | number | 0 | -->
<!-- | h | clockhour of halfday (1~12) | number | 12 | -->
<!-- | H | hour of day(0~23) | number | 0 | -->
<!-- | k | clockhour of day | number | 24 | -->
<!-- | m | minute of hour | number | 30 | -->
<!-- | s | second of minute | number | 55 | -->
<!-- | S | fraction of second | number | 978 | -->
<!-- | z | time zone | text | Pacific Standard Time; PST | -->
<!-- | Z | time zond offset/id | zone | -0800; -08:00; America/Los_angeles| -->
<!-- | T | 날짜/시간 구분자 | text | yyMMddTHHmmss | -->

