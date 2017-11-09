---
layout: post
title: "안드로이드 DataBinding"
date: 2017-11-08 00:22:00 +0900
categories: Android
tags: [Android, DataBinding, Bye FindViewById]
description: 안드로이드 DataBinding
---

# 안드로이드 데이터(View / ViewGroup)를 변수에 바인딩 하는 방법 - 심화!!

1. 우선 Gradle 설정부터

    App 디렉터리 밑 Gradle에 다음과 같이 dataBinding을 사용하기 위한 준비를 한다.

    ```
    android {
        dataBinding {
            enabled = true
        }
    }
    ```

2. XML의 최상위를 layout 태그로 감싸준다.

    아래는 테스트로 작성한 XML 입니다.

    ``` XML
    <layout
        xmlns:android="http://schemas.android.com/apk/res/android">

        <LinearLayout
            android:id="@+id/linear_layout"
            android:layout_width="match_parent"
            android:layout_height="match_parent">

            <TextView
                android:id="@+id/text_view"
                android:layout_width="match_parent"
                android:layout_height="match_parent"/>

        </LinearLayout>

    </layout>
    ```

3. 알아서 Binding 해주는 객체를 받아 사용한다.

    아래는 테스트로 작성한 Activity 코드 중 onCreate 부분입니다.

    ``` Java
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        ActivityBindingTextBinding binding = DataBindingUtil.setContentView(this, R.layout.activity_binding_test);
        binding.textView.setText("텍스트뷰");
    }

    ```

이때 알아서 Binding 되는 객체의 클래스 명은 작성한 xml 이름과 같다.
※ 중간에 _ 기호가 들어가 있으면 다음 알파벳은 대문자가 된다 [파스칼 표기법]

아래 FindViewById를 사용하여 데이터 바인딩을 사용했을 때보다 훨씬 코드가 간결한 볼 수 있다.

``` Java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_binding_test);
    LinearLayout linearLayout = (LinearLayout) findViewById(R.id.linear_layout);
    TextView textView = (TextView) findViewById(R.id.text_view);
    textView.setText("텍스트뷰");
}
```
