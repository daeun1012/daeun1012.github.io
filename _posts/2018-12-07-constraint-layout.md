---
layout: post
title: Constraint layout 의 다른점
tags: Android
comments: true
---

## 안드로이드는 뷰를 어떻게 그리는가?
- 측정<br>시스템은 각각의 뷰 그룹과 뷰 구성요소들의 크기와 위치를 결정하기 위해 뷰 트리의 하향식 탐색(top-down traversal)을 수행합니다.<br>뷰 그룹이 측정될 때에는, 뷰 그룹에 속한 뷰들(children)도 함께 측정됩니다.
<br><br>
- 레이아웃<br>측정 단계에서 결정된 뷰그룹 하위에 속한 오브젝트들의 사이즈를 이용하여 뷰그룹의 위치가 결정됨과 함께, 또 다른 뷰 트리의 하향식 탐색이 일어납니다.
<br><br>
- 그리기<br>시스템은 아직 또 다른(레이아웃 단계에서 일어난) 하향식 탐색을 수행하고 있습니다. <br>
뷰 트리에 속한 오브젝트들을 위해,GPU가 수행할 그리기 명령들(a list of drawing commands to the GPU)을 담은 리스트를 보낼 Canvas 오브젝트가 생성됩니다.<br>
그리기 명령들은 앞의 두 단계(측정과 레이아웃)에서 시스템이 결정한, 뷰 그룹과 뷰 오브젝트들의 사이즈와 위치가 포함되어 있습니다.

### 즉, 그리기 과정 내의 모든 단계에서 뷰 트리에 대한 하향식 탐색을 필요로 한다. 그러므로, 각 뷰 계층내에 포함시킨 뷰가 많아질 수록, 디바이스가 뷰를 그리기 위해 더 많은 시간과 연산 능력을 필요로한다.

ConstraintLayout 을 사용하면 수평적인 구조로 Layout 을 구성할수 있다.

하지만, 기존의 RelativeLayout 이 있었는데, 왜 ConstraintLayout 이 더 강력하다고 물어본다면...<br>
ConstraintLayout 은 최근에 개발된 기술이다. 단점이 있으니 개선하려 개발하지 않았겠는가...는 농담반, 진담반이고 다른점을 찾아보도록하자.

- RelativeLayout에서 불가능했던 자식 뷰간의 상호관계 정의가 가능
- LinearLayout을 써야만 했던 뷰 비율 조정도 간단하게 가능 (depth가 깊어지는 것 방지)
- 뷰 계층을 간단하게 구성하여 유지보수, 성능 향상
- 구글이 기존의 많은 layout 기능들을 deprecated함. -> constraintLayout을 할 수 밖에 없음 ㅜㅜ


## ConstraintLayout 의 Group

문제점.
ConstraintLayout 의 가장 큰 강점은 뷰를 flat 하게 구성할수 있다는 것이다.
그런데 여러 뷰들을 그룹지어야 하는 경우가 생기면 어떻게 해야할까?
<b>(예를 들면 여러 뷰들의 visibility를 한번에 수정하려고 하는 경우)</b>

기존처럼 뷰들을 Layout 으로 감싸면 되겠지만, 그러면 ConstraintLayout을 사용하는 의미가 퇴색된다.

이런경우 Group 을 이용하면 된다.

app:constraint_referenced_ids 을 사용해 뷰를 그룹화 하자.

```xml
    <android.support.constraint.Group
        android:id="@+id/winnerplayer_group"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        app:constraint_referenced_ids="winnerPlayerLabel,winnerPlayer" />

    <TextView
        android:id="@+id/winnerPlayerLabel"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:text="@string/result_winner"
        android:textSize="44sp" />

    <TextView
        android:id="@+id/winnerPlayer"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:text="O"
        android:textSize="44sp" />
```
