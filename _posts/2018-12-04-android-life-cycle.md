---
layout: post
title: onResume, onStart 다른점
categories: Android
---

안드로이드 LifeCycle 중,
onResume 과 onStart의 다른점을 정리해보기로 하자.

먼저 life cycle 을 먼저 나열하자면,

onCreate -> onStart -> onResume
onPause -> onStop -> onDestroy

순으로 볼수있다.

<img src="{{ site.url }}/public/img/1204-android-lifecycle/image.png">

onStart 와 onResume 의 차이점은
onResume 일 때만, 유저와 상호작용이 가능하고
onStart  일 때는, 화면은 노출되나 상호작용이 불가능하다.

예를들어,

Dialog 가 띄워졌을 때, 호출되는 메소드는
onPause -> onResume 순이다.

새로운 액티비티가 올라갈때는
onPause -> onStop 순으로 진행된다.
