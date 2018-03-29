---
layout: post
title:  Android Architecture Component
categories: [Android]
---

## [Android Architecture Component](https://developer.android.com/topic/libraries/architecture/index.html)

안드로이드 개발하며 대표적으로 MVC - MVP - MVVM 패턴을 많이 사용한다.
나 역시 [Todo project](https://github.com/googlesamples/android-architecture/tree/todo-mvp) 를 참조하여 MVP 패턴을 주로 사용해왔다.<br>
<br>
최근 다녀온 GDG DevFest Seoul 2017 에서 Android Architecture Component Codelab 세션을 통해<br>
구글에서 제공하는 AAC(Android Architecture Component) library 를 접하게 되었다.<br>
처음에 코드랩 신청할때는 그냥 기존 MVP나 MVVM 설명인줄... 사실 AAC 도 MVVM 의 일종 인거 같지만...<br>
구글에서 친절히 [codelab](https://codelabs.developers.google.com/codelabs/android-lifecycles/index.html?index=..%2F..%2Findex#0) 을 제공하여 설명하고 있다면 한번이라도 살펴보는게 맞다고 생각한다.<br>
그리고 구글 코드랩 페이지는 정말 좋다, 배울게 많다 :)<br>
또한 [Developer 문서](https://developer.android.com/topic/libraries/architecture/index.html)에도 따로 정리까지 해주었다. (감동쓰...)<br>
Android Architecture Component library 는 1.0 stable 버전이라 개인 프로젝트에 적용해보고자 AAC 를 좀더 분석해 보기로 하였다.

### 1. ViewModel
 - activity 나 fragment에 데이터를 제공하는 역할을 한다.
 - 데이터 로드, 제공, 사용자 수정 내용을 전달하기 위해 다른 구성요소를 호출하는등 데이터 처리의 비지니스 부분과의 통신을 처리한다.
 - View 에 대해 알지 못하며, 회전으로 인한 activity 재생성 등의 구성 변경에 영향을 받지 않는다. --> <font style="bold" color="red">즉, UI에 독립적이다!!!! (별표 백만개 *******) UI 테스트 할때 좋겠다.</font>

주의해야 할 점은 ViewModel 에 Context나 View 클래스를 참조하면 안된다.<br>
메모리 누수의 원인이 될 수 있기 때문이다.

아래 그림이 ViewModel 의 LifeScope 를 좀 더 명확히 설명해 주고 있다.
 ![aac1]({{ site.url }}/public/img/android-architecture-component/screen1.png)

### 2. LiveData
 - Observable 데이터 홀더 이다.
 - app 안의 component 들이 명시적으로 dependency 를 갖지 않도록 하면서, 변경 사항을 LiveData 객체에서 관찰 할 수 있도록 한다.
 - Lifecycle 을 인지하고 있기 때문에 더이상 data가 필요하지 않게되면 자동으로 reference 를 clean up 한다. (오 좋다)

<script src="https://gist.github.com/daeun1012/ce293b49a9f90ec11bd0dd6b8226e713.js"></script>

### 3. LifecycleOwner/LifecycleRegistryOwner
  - lifecycle 을 주관(?)하는 클래스이다. stable 버전에서 AppCompatActivity 와 Support Fragment 클래스에서 implement 하고 있다.<br>
  - 해당 인터페이스를 implement 하고 다른 component를 주입하여 사용할 수 있다.

 기존엔 아래와 같이 nCreate(), onStart(), onStop() 메소드를 통해 lifecycle을 직접 handling 해 왔었다.
 <script src="https://gist.github.com/daeun1012/3e35341b45011f7794188cb057a2b340.js"></script>
  <br>
  그러나 이제는 LifecycleObserver 를 implement 하여 Annotation 을 이용한 Lifecycle Handling 을 할 수 있다.<br>
  <script src="https://gist.github.com/daeun1012/560012101f9954747047b0e8bc24cb7c.js"></script>


<br><br>
dagger2와 espresso 도 적용해 보고싶은데... AAC 를 적용한 reference 가 별로 없다.
직접 해보고 판단하는 수밖에... 아니면 기다리거나... 무튼 삽질이라도 해보고 후회하는게 나을것 같다. 경험은 중요하니깐.





-----
google Refern 이외 정리 및 이해하는데 참고한 페이지
- [https://medium.com/exploring-android/exploring-the-new-android-architecture-components-c33b15d89c23](https://medium.com/exploring-android/exploring-the-new-android-architecture-components-c33b15d89c23)
- [https://proandroiddev.com/architecture-components-modelview-livedata-33d20bdcc4e9](https://proandroiddev.com/architecture-components-modelview-livedata-33d20bdcc4e9)
- [http://tourspace.tistory.com/23](http://tourspace.tistory.com/23)
- [http://hyuncb.tistory.com/2?category=627854](http://hyuncb.tistory.com/2?category=627854)
- [http://chuumong.github.io/android/2017/06/29/Guide-to-App-Architecture](http://chuumong.github.io/android/2017/06/29/Guide-to-App-Architecture)
