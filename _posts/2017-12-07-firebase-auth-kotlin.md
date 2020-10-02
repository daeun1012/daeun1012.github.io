---
layout: post
title:  Firebase Auth Kotlin 으로 적용
tags: [Android]
comments: true
---

## Firebase Auth With Kotlin

서버 개발 기간 단축을 위해 Firebase 를 이용하기로 했다.

제일 먼저 회원관리를 위한 auth 를 적용했다.

[!Firebase Auth 가이드](https://firebase.google.com/docs/auth/?hl=ko) 를 참조하면 매우 친절한 예제와 방법이 나와있다.
추가로 안드로이드 스튜디오에서도 바로 적용가능하다.

#### 안드로이드 스튜디오 적용방법
##### 1. menu -> tools -> Firebase 클릭<br>
![firebase-auth1]({{ site.url }}/public/img/firebase-auth-kotlin/screen1.png)

##### 2. Authentication 확장 후 Email and password authentication 클릭<br>
![firebase-auth2]({{ site.url }}/public/img/firebase-auth-kotlin/screen2.png)

##### 3. 이제 Firebase 계정과 연결해주자! Connect to Firebase 클릭!!!!<br>
![firebase-auth3]({{ site.url }}/public/img/firebase-auth-kotlin/screen3.png)

##### 4. 프로젝트 정보 기입 후 적용하면 !!!! Firebase 프로젝트 생성 완료!!!! (빠름빠름빠름~)<br>
![firebase-auth4]({{ site.url }}/public/img/firebase-auth-kotlin/screen4.png)

##### 5. 이제 소스상에서 Firebase 를 추가해주자. Accept Changes 클릭하면 자동 Build ~~ <br>
<img src="{{ site.url }}/public/img/firebase-auth-kotlin/screen5.png" width="50%">
<br><br>
<p>직접 문서보면서 추가하는 것보다는 훨씬 손쉽고 편하다.<br>
문서보면서 최초 작성해보고 그 이후에는 스튜디오로 적용하는게 좋을거같다.
</p>

#### 그리고 이제 초기 설정이 완료되었으면 코틀린을 이용해 auth 를 구현해보자!!!
아래 코드는 AAC 를 적용한 auth를 구현중인 코드이다<br>
현재는 이메일 가입만 구현해놓았으며, 추후 기타 firebase 에서 지원하는 로그인 연동 방식을 구현할 예정이다.

<script src="https://gist.github.com/daeun1012/679602cd73bc3b0ad445ced94287fc26.js"></script>
