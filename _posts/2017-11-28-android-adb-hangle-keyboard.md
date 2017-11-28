---
layout: post
title:  "[Android] 에뮬레이터 한글 키보드 사용 방법"
categories: [android, 한글키보드, adb, hangle-keyboard]
excerpt: "구글 플레이스토어가 에뮬레이터에서도 된다!!!!!!!!!!!!!! 이거다!!!!!!!!!"
comments: true
image:
  feature: adb-hangle-keyboard/screen7.png
---

# 에뮬레이터 한글 키보드 사용법

글 작성 시점으로 현재 아이폰7을 사용중이다. 앞으로도 그럴거 같다...<br>
안드로이드 개발자면서 아이폰쓴다고 뭐라하지만 아이폰이 좋다...<br>
그래도 개인적으로 안드로이드 개발용 폰 [Google Nexus 6P]를 구입하여 개발시에 유용하게 사용하고 있다.<br>
이정도면 아이폰 써도도ㅐ...^^<br>
<br>
단지 개인 폰이 아니어서 깜빡할 때가 있다.<br>
그래서 안드로이드 에뮬레이터를 가끔 사용하고는 하는데, 기본적으로 한글 키보드를 지원하지 않는다... 또르르...<br>
<br>
이리저리 구글링을 하여 한글 키보드 apk 를 다운받아서 adb에 설치해보았지만<br>
에러코드... <font color="red">INSTALL_FAILED_NO_MATCHING_ABIS</font>
또 구글링 해보니 cpu/abi를 x86 이 아닌 armxxx 로 변경하라 한다.<br>
그냥 맘에 안든다.<br>
그래서 에뮬레이터 보다가 발견한 방법.<br>
<br>
구글 플레이스토어가 에뮬레이터에서도 된다!!!!!!!!!!!!!! 이거다!!!!!!!!!<br>
<br>
## 1. Android Studio Virtual Devices 를 연다. (제일 끝 귀여운(?) 빼꼼이 안드로이드 버튼)
![hangle-keyboard1]({{ site.url }}/img/adb-hangle-keyboard/screen1.png)

## 2. Play Store 탭이 생겼다...!! 하단 create virtual devices 클릭!! (전 이미 만들었어요)
![hangle-keyboard3]({{ site.url }}/img/adb-hangle-keyboard/screen3.png)

## 3. Play Store 지원 에뮬레이터 만들기
![hangle-keyboard4]({{ site.url }}/img/adb-hangle-keyboard/screen4.png)

## 4-1. (선택) 에뮬레이터 실행 후 설정으로 이동. 설정 메뉴 찾기 귀찮다. 빨리 찾자.
<img src="{{ site.url }}/img/adb-hangle-keyboard/screen10.png" width="30%">

## 4-2. language 쓰기도 귀찮. lan ... ^^
<img src="{{ site.url }}/img/adb-hangle-keyboard/screen11.png" width="30%">

## 4-3. Languages & input -> Languages 클릭
<img src="{{ site.url }}/img/adb-hangle-keyboard/screen12.png" width="30%">

## 4-4. Add a language 클릭
<img src="{{ site.url }}/img/adb-hangle-keyboard/screen13.png" width="30%">

## 4-5. 한국어를 찾아야하는데 가장 하단에 있다. 귀찮다.
<img src="{{ site.url }}/img/adb-hangle-keyboard/screen14.png" width="30%">

## 4-6. Korean 검색어 입력!!
<img src="{{ site.url }}/img/adb-hangle-keyboard/screen15.png" width="30%">

## 4-7. 대한민국 클릭. ...... 고조... 우리 동포들 안드로이드 개발 같이하시렵니까?... 같이 할수 있는 날이 올까...? 오자...!
<img src="{{ site.url }}/img/adb-hangle-keyboard/screen16.png" width="30%">

## 4-8. 언어 순서 변경
<img src="{{ site.url }}/img/adb-hangle-keyboard/screen17.png" width="30%">

## 5. 에뮬레이터 실행하면 play store 아이콘이 나를 반겨준다... 감동
실행 후 계정 설정을 해야한다.<br>
![hangle-keyboard5]({{ site.url }}/img/adb-hangle-keyboard/screen5.png)

## 6. 아직 키보드 설치 전... 영문으로 hangle.... 입력해 한글 키보드를 검색한다.
<img src="{{ site.url }}/img/adb-hangle-keyboard/screen6.png" width="30%">

## 7. Google 한국어 입력기 설치.
<img src="{{ site.url }}/img/adb-hangle-keyboard/screen7.png" width="30%">

## 8. Google 한국어 입력기 실행하고 순서대로 따라하면 완료
<img src="{{ site.url }}/img/adb-hangle-keyboard/screen8.png" width="30%">

<br><br><br>

초창기에 에뮬레이터 너무 느려서 안쓰다가 오랫만에 써봤더니 속도도 나름 괜찮고<br>
플레이스토어까지 지원하니 써볼만 할거 같다.<br>
