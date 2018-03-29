---
layout: post
title:  Android Studio 3.0 ProductFlavor Error
categories: Android
---

안드로이드 스튜디오가 3.0으로 업데이트 되었다.

고로 나도 업데이트를 했다.

그러나 기존에 github 에 존재하는 대다수의 프로젝트는 3.0으로 컨버팅 되어있지 않다.

그래서 발생하는 오류 ProductFlavor Error 를 처리해보자

매우 간단한다.

<pre>
  <code>
      android {
          ...
          flavorDimensions "default"
          ...
      }
  </code>
</pre>
