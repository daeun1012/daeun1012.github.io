---
layout: post
title: Gradle Dependency 관리하기 (buildSrc)
categories: [Android]
---

### Gradle Dependency Management Issue

build.gradle 파일이 module 당 1개씩 존재해 나중에 모듈별로 관리하다보면 수많은 gradle 파일을 관리해야하는 이슈가 생긴다.

기존엔 안드로이드 gradle dependency 관리를 위해 루트레벨 build.gradle 파일에서 ext ... 선언하여 관리하였으나 이 방법은 IDE에서 아직 지원되지 않는다. (Autocomplete되지 않음)

최근 미디움 메일링을 통해 접한 추천글에서 코틀린을 이용한 gradle dependency 관리발견!!! (이것은혁명?!)

[Organizing Gradle Projects](https://docs.gradle.org/current/userguide/organizing_gradle_projects.html#sec:build_sources)

Use buildSrc to abstract imperative logic
....
buildSrc uses the same source code conventions applicable to Java and Groovy projects. It also provides direct access to the Gradle API. Additional dependencies can be declared in a dedicated build.gradle under buildSrc.

Gradle이 수행되면 buildSrc 디렉토리가 존재하는지 체크한다. 이 경우 Gradle은 자동적으로 코드를 컴파일하고 테스트한 뒤 당신의 빌드 스크립트의 classpath에 넣는다. 어떤 추가적인 지시도 규정 할 필요가 없다.

---

1. 루트폴더에 buildSrc 폴더를 만든다.
2. buildSrc 폴더 안에  build.gradle.kts 파일을 생성한다.
3. 아래와 같이 작성한다.

    plugins {
        `kotlin-dsl`
    }
    // Required since Gradle 4.10+.
    repositories {
        jcenter()
    }

4. buildSrc의 하위 폴더로 src > main > java 폴더를 생성한다.

5. java 폴더 안에 Dependencies.kt 파일을 생성한다. (파일명은 자유롭게)

6. 아래와 같이 작성한다. (예시)

    object Versions {
        val kotlin = "1.2.71"
    }
    object Dependencies {
        val kotlinStandardLibrary = "org.jetbrains.kotlin:kotlin-stdlib-jdk7:${Versions.kotlin}"
    }

7. 아래와 같이 사용한다!!!!!!! (편하드아)

    implementation Dependencies.kotlinStandardLibrary

---

참고 사이트

[https://proandroiddev.com/gradle-dependency-management-with-kotlin-94eed4df9a28](https://proandroiddev.com/gradle-dependency-management-with-kotlin-94eed4df9a28)