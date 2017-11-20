---
layout: post
title: "Android 캐시 & 데이터 삭제하기"
date: 2017-11-21 00:13:00 +0900
categories: Android
description: Android 캐시 & 데이터 삭제하기
tag: [Android, CacheDelete, DataDelete]
---
# Android 캐시 & 데이터 삭제방법

## Setting을 통해 지우는 방법

    직접 지우는 방법으로 지울수도 있다.
    하지만 코드로 지우고 싶다.

![Clear](/assets/images/2017-11-21-cache-data-clear.png)

## Code로 지우는 방법

- Cache 와 Data를 지울때 필요한 File Delete 함수를 작성.

	생성한 File이 Directory 일수도 있기 때문에 재귀함수를 통해 Directory안에
    File들도 Delete 할수있도록 작성

	{% highlight java %}
    public boolean deleteCache(File dir){
      //File이 Null 인지 Null이 아니라면 폴더인지 체크
      if(dir != null && dir.isDirectory()){
        //Null도 아니고 폴더도 아니라면 폴더안 파일 리스트를 호출
        String[] children = dir.list();
        //파일 리스트를 반복문으로 호출
        for(String child : children){
          //파일 리스트중 폴더가 존재할 수 있기 때문에 재귀호출
          boolean isSuccess = deleteCache(new File(dir, child));
          if(!isSuccess){
            return false;
          }
        }
      }
      return dir.delete();
    }
    {% endhighlight %}

- Cache Clear

	{% highlight java %}
    //Application 의 캐시 폴더를 호출한다.
    File dir = getApplicationContext().getCacheDir();
    //캐시폴더가 없거나 폴더가 아닐수 있기때문에 예외처리
    if(dir != null && dir.isDirectory()){
      //위에 작성해둔 Delete 재귀 함수 호출.
      deleteCache(dir);
    }
    {% endhighlight %}

- Data & Cache Clear

	{% highlight java %}
    //마찬가지로 캐시 폴더를 호출한다.
    File cache = getCacheDir();
    //Data까지 지우길 원하므로 캐시폴더의 부모폴더 까지 호출한다.
    File appDir = new File(cache.getParent());
    //부모폴더가 존재하는지 여부 확인
    if(appDir.exists()){
      //부모폴더가 존재한다면 부모폴더의 자식 파일리스트를 호출
      String[] children = appDir.list();
      //부모폴더의 자식 파일리스트를 반복문으로 호출해 삭제함수를 호출한다.
      for(String child : children){
        if(!TextUtils.equals(child, "lib")){
          deleteCache(new File(appDir, child));
        }
      }
    }
    {% endhighlight %}