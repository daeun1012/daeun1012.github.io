---
layout: post
title:  iTunes store 수출 규정 준수
tags: [iOS]
excerpt: "iOS 배포시 수출 규정 준수 에러(?) 처리 방법"
comments: true
---

info.plist 항목 추가

다음 빌드에 수출 규정 준수에 대한 정보를 입력하지 않아도 되도록 info.plist에 다음 키를 입력하십시오.

```xml
    <key>ITSAppUsesNonExemptEncryption</key><false>
```

App Uses Non-Exempt Encryption : Boolean : NO
