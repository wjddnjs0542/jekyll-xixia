---
layout: post
title: "안드로이드 화면 전환 애니메이션"
date: 2017-12-03 21:48:00 +0900
categories: Android
description: 안드로이드 화면 전환 애니메이션
tag: [Android, Animation]
---
# 안드로이드 화면 전환 애니메이션

## Activity 간 화면 전환이 될때 애니메이션을 추가하기

- 중요 함수
  * overridePendingTransition(int anim, int anim);

### Activity 시작 애니메이션 설정

#### 첫번째 방법 startActivity와 동시에 함수 호출

{% highlight java %}
 startActivity(new Intent(NowActivity.this, NextActivity.class));
 overridePendingTransition(NextActivity 등장 anim.xml, NowActivity 사라짐 anim.xml);
{% endhighlight %}

#### 두번째 방법 NextActivity의 OnCreate에 선언부에 함수 호출

{% highlight java %}
@Override
protected void onCreate(Bundle savedInstanceState){
    super.onCreate(saveInstanceState);
    overridePendingTransition(NextActivity 등장 anim.xml, NowActivity 사라짐 anim.xml);
}
{% endhighlight %}

- 주의사항
첫번째 방법에선 반드시 **Intent를 실행 후 함수를 호출하여야 동작**하므로 주의하여야 하고<br>두번째 방법에선 반드시 super 메서드 밑에 실행할 필요는 없지만, **안전하게 super 메서드 후에 선언**합시다.

### Activity 종료 애니메이션 설정

{% highlight java %}
@Override
public void finish(){
    super.finish();
    overridePendingTransition(NowActivity 등장 anim.xml, NextActivity 사라질 anim.xml);
}
{% endhighlight %}

- 주의사항
반드시 **super 메서드 후에 함수를 호출**하여야 동작함.<br>onDestroy 와 onStop 에서는 실행되지 않음.


### Activity 화면 전환 애니메이션 없애기

- 시작 애니메이션 호출 위치 혹은 종료 애니메이션 호출 위치에 anim대신 0을 파라미터로 보내게 되면
 애니메이션이 종료된다.

{% highlight java %}
overridePendingTransition(0, 0);
{% endhighlight %}

