---
layout: post
title: "안드로이드 스택 관리"
date: 2017-11-24 10:46:00 +0900
categories: Android
description: 안드로이드 스택 관리
tag: [Android, Stack]
---
# 안드로이드 스택 관리

Intent를 이용해 Activity를 이동할때 이전 Activity가 Stack에 쌓이게 된다. 이 Stack을 적절히 조절하는 방법이다.

- 첫번째 방법

    Intent의 함수 setFlag를 이용하는 방법
    setFlags : 이전에 설정된 flag를 대체한다.

	{% highlight java %}
    Intent intent = new Intent(MainActivity.this, TestActivity.class);
    intent.setFlags(Intent.FLAG_ACTIVITY_STANDARD);
    startActivity(intent);
    {% endhighlight %}

- 두번째 방법

	Intent의 함수 addFlag를 이용하는 방법
    addFlags : 해당 Intent에만 Flag를 붙인다.

    {% highlight java %}
    Intent intent = new Intent(MainActivity.this, TestActivity.class);
    intent.addFlags(Intent.FLAG_ACTIVITY_STANDARD);
    startActivity(intent);
    {% endhighlight %}

## 자주 사용되는 Flags 종류

- FLAG_ACTIVITY_STANDARD

	아무 flags도 지정하지 않았을 때 STANDARD가 호출

	|--|--|--|
	|:--|:--|:--|
	|-|-|B|
	|C|B 호출->|C|
	|B|-|B|
	|A|-|A|

- FLAG_ACTIVITY_SINGLE_TOP

	동일한 Activity가 호출된다면 이전 Activity를 종료하고 새로운 Activity만을 남긴다.
	동일한 Activity가 연속적으로 사용되어야 적용되며
    연속적으로 사용되지 않는다면 계속 쌓인다.

	|--|--|--|
	|:--|:--|:--|
	|-|-|B|
	|A|B 호출->|A|
	|B|-|B|
	|A|-|A|

	|--|--|--|
	|:--|:--|:--|
	|-|-|-|
	|B|Flag적용->|-|
	|B|-|B|
	|A|-|A|

- FLAG_ACTIVITY_CLEAR_TOP

	기존에 Stack에 쌓여있던 Acivity의 동일한 Activity가 호출 되면 해당 Activity 상위에 쌓여있는 Activity를 제거하며, RootActivity는 제거되지 않는다.

	|--|--|--|
	|:--|:--|:--|
	|-|-|-|
	|B|Flag적용->|-|
	|B|-|B|
	|A|-|A|

	|--|--|--|
	|:--|:--|:--|
	|-|-|-|
	|A|Flag적용->|-|
	|B|-|-|
	|A|-|A|

	|--|--|--|
	|:--|:--|:--|
	|-|-|-|
	|E|C호출->|-|
	|D|-|-|
	|C|-|C|
	|B|-|B|
	|A|-|A|

- FLAG_ACTIVITY_REORDER_TO_FRONT

	기존에 Stack에 쌓여있던 Activity와 동일한 Activity가 호출되면 무조건 동일한 Activity를 최상위로 올림

	|--|--|--|
	|:--|:--|:--|
	|B|-|-|
	|C|Flag 적용->|B|
	|B|-|C|
	|A|-|A|

- FLAG_ACTIVITY_NO_HISTORY

	새로 생성되는 Activity를 Task에 보존하지 않아 자동적으로 제거하고 싶은 Activity가 있을 때 사용(제거되기 전까지 Stack에는 존재함.)
	B에서 속성을 적용하고 C를 호출하면 C는 Task에서 보존되지않고 제거 시점은 D가 제거되는 시점에서 C가 같이 제거됨.

	|--|--|--|
	|:--|:--|:--|
	|D|D 제거->|-|
	|C|Flag 적용->|-|
	|B|-|B|
	|A|-|A|