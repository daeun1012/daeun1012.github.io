---
layout: post
title:  Android Databinding Library
tags: [Android]
comments: true
---

## Databinding Library

Android 개발을 하며 가장 귀찮고 필요없는 boilerplate code의 쉽상이며
비용처리도 큰 findViewById() 메소드를 도와주는 library가 나왔다. 오ㅐ 이제야 온것이냐. (알고보니 나온지 꽤됐다... 열공하자...)

최근 AAC(Android Architecture Component) 관련 포스팅을 해서 더 알아보고자 샘플 라이브러리를 찾던중 매우 좋은 샘플을 찾았다.
(Github Sample)[https://github.com/googlesamples/android-architecture-components]
RxJava 와 Kotlin, Dagger2, Espresso ... AAC... 다 내가 찾던거다.

간단히 Databinding을 소개하기위해 BasicSample을 참고하여 정리해보자.

[구글문서_DatabindingLibarary](https://developer.android.com/topic/libraries/data-binding/index.html#studio_support) 에 따르면

> 데이터 바인딩 라이브러리는 유연성과 폭넓은 호환성을 모두 제공하는 지원 라이브러리로, <font color="red">Android 2.1(API 레벨 7 이상)</font>까지 Android 플랫폼의 모든 이전 버전에서 사용할 수 있습니다.
>데이터 바인딩을 사용하려면 Android Plugin for Gradle 1.5.0-alpha1 이상이 필요합니다.

### 빌드 환경
build.gradle 파일에 몇줄만 추가 하면 된다.

```
android {
    ....
    dataBinding {
        enabled = true
    }
}
```

### 데이터 바인딩
기본적으로, Binding 클래스는 레이아웃 파일의 이름을 기준으로 생성되어 파일 이름을 파스칼 표기법(Pascal Case: 합성어의 첫 글자를 대문자로 표기)으로 변환하고 그 뒤에 "Binding"을 접미사로 붙인다.
레이아웃 파일은 list_fragment.xml이고, 따라서 생성된 클래스는 ListFragmentBinding이다. 이 클래스는 레이아웃 속성(예: isLoading 변수)에서 레이아웃의 View까지 모든 바인딩을 유지하고 바인딩 식에 대해 값을 할당하는 방법을 알고 있다.
<script src="https://gist.github.com/daeun1012/2c36a515949ff33271b3d8dcad719405.js"/>

### 데이터 바인딩 레이아웃 파일
데이터 바인딩 레이아웃 파일은 약간 달라서 layout의 루트 태그로 시작하고 그 뒤에 data 요소와 view 루트 요소가 나온다.
data 내에 있는 `isLoading` 변수는 해당 레이아웃 내에서 사용할수 있는 속성에 대한 설명이며 레이아웃 내에 있는 식은 "@{}" 구문을 사용하여 특성 속성에 기록된다.
<script src="https://gist.github.com/daeun1012/aab7a991b804956ff20e84e6a3a7f230.js"/>

### 이벤트 처리
데이터 바인딩을 사용하여 뷰에서 발송되는 이벤트를 처리하는 식을 작성할 수 있다.
<script src="https://gist.github.com/daeun1012/a4257c4029d125a924dc8e0d7221ccc8.js"/>
<br><br><br><br><br>

---

나는 주로 Butterknife를 사용하고 있다.<br>
Butterknife는 유지보수 코드를 (ex: findViewById(), onClick()...) 큰 수고비용없이 변환 가능하고, 가독성 역시 기존 코드들을 해치지 않을것이라고 본다.<br>
물론 개인적인 생각일뿐 의견을 다분할수 있다.<br>
그러나 Databinding을 정리하고 알아보고 나니, databinding 의 적용은 많은 부분에서의 변함이 있을것이라고본다.<br>
우선 layout xml 자체 부터 변환을 해야하니, 파일수만해도 여러개가 되는것을 볼수있다.<br>
<br>
AAC 와 함께 적용했을때 빛을 보는 라이브러리같다.
새로운 프로젝트에는 가볍게 적용하여 시작해보면서 살펴봐야하겠다.<br><br><br>
