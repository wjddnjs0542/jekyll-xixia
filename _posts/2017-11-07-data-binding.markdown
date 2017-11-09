---
layout: post
title: "안드로이드 DataBinding - 기본"
date: 2017-11-07 21:00:00 +0900
categories: Android
tags: [Android, DataBinding, FindViewById]
description: 안드로이드 DataBinding - 기본
---

# 안드로이드 데이터(View / ViewGroup)를 변수에 바인딩 하는 방법 - 기본편!!

아래는 테스트로 작성한 XML 입니다.

{% highlight xml %}
<LinearLayout
    android:id="@+id/linear_layout"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <TextView
        android:id="@+id/text_view"
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>
</LinearLayout>
{% endhighlight %}

아래는 테스트로 작성한 Activity 코드 중 onCreate 부분입니다.

``` Java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_binding_test);
}

```

onCreate 의 setContentView 이후

즉 Activity에 XML layout이 붙었을 경우 작성.

``` Java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_binding_test);
    LinearLayout linearLayout = (LinearLayout) findViewById(R.id.linear_layout);
    TextView textView = (TextView) findViewById(R.id.text_view);
}
```


