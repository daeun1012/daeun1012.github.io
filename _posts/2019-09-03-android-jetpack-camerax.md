---
layout: post
title: Android CameraX
tags: Android
comments: true
---

# Android Jetpack CameraX

## 특징

- Camera2를 사용
- 생명주기를 인식함
- 특정 디바이스에 종속되는 Bokeh, HDR 등과 같은 이펙트 지원
- 구글 공식 카메라X 예제에서는 ViewFinder(뷰파인더)라는 명칭을 씀

## 최소 요구 사항

- Android API Level 21 (롤리팝 5.0)
- 안드로이드 아키텍처 컴포넌트 1.1.1 버전
- lifecycle-aware 액티비티로는 FragmentActivity 또는 AppCompatActivity 사용

## UseCase

- [미리보기](https://tech.burt.pe.kr/android/camerax/preview): 디스플레이에서 이미지 얻기
- [이미지 분석](https://tech.burt.pe.kr/android/camerax/analyze-image): MLKit과 같은 알고리즘에 데이터를 전달하기 위한 버퍼에 대한 완전한 접근.
- [이미지 캡처](https://tech.burt.pe.kr/android/camerax/take-photo): 고품질 이미지 저장

## CameraX 장점

- Reduced device specific testing
- 75% 의 코드 길이 감소
- 코드 가독성 향상
- apk 크기 감소

---

## 그래들 의존성 추가
```
    def camerax_version = "1.0.0-alpha01"
    implementation "androidx.camera:camera-core:${camerax_version}"
    implementation "androidx.camera:camera-camera2:${camerax_version}"
```

## 화면 미리보기
```kotlin
    val previewConfig = PreviewConfig.Builder().build()
    val preview = Preview(previewConfig)
    preview.setOnPreviewOutputUpdateListener {
    PreviewOutput : Preview.PreviewOutput? ->
    // your code here. e.g. use previewOutput?.surfaceTexture
    // and post to a GL renderer.
    }
    // attach preview to lifecycle
    CameraX.bindToLifecycle(this as LifecycleOwner, preview)
```
## 이미지 분석
```kotlin
    // configure image analysis
    // set resolution
    val imageAnalysisConfig = ImageAnalysisConfig.Builder()
    .setTargetResolution(Size(1280, 720))
    .build()
    val imageAnalysis = ImageAnalysis(imageAnalysisConfig)
    // attach output
    imageAnalysis.setAnalyzer({ image : ImageProxy, rotationDegrees : Int ->
    val cropRect = image.cropRect
    // insert your code here
    })
    CameraX.bindToLifecycle(this as LifecycleOwner, imageAnalysis, preview)
```
## 이미지 촬영
```kotlin
    // configure image capture
    val imageCaptureConfig = ImageCaptureConfig.Builder()
    .setTargetRotation(windowManager.defaultDisplay.rotation)
    .build()
    val imageCapture = ImageCapture(imageCaptureConfig)
    CameraX.bindToLifecycle(this as LifecycleOwner, imageCapture, imageAnalysis, preview)
```
## 이미지 저장
```kotlin
    val file = File(...)
    imageCapture.takePicture(file,
    object : ImageCapture.OnImageSavedListener {
    override fun onError(error: ImageCapture.UserCaseError,
    message: String, exc: Throwable?){
    // insert your code here
    }
    override fun onImageSaved(file: File) {
    // insert your code here
    }
    })
```


## 참조

[Getting Started with CameraX](https://codelabs.developers.google.com/codelabs/camerax-getting-started/#0)
[찰스의 안드로이드-Android CameraX 라이브러리 미리보기](https://www.charlezz.com/?p=1237)
