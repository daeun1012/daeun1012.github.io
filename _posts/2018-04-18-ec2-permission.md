---
layout: post
title: public key로 ssh 로그인이 안될때
tags: AWS
comments: true
---

.ssh/authorized_keys 파일에 public key를 추가하고
.pem 파일을 이용해 aws ec2 ssh 접근을 시도하려고 했다.

그러나 password 를 다시 물어봤다.

해당 문제는 .ssh 폴더 권한을 설정해주니 말끔히 해결되었다.

> .ssh는 0700, authorized_keys는 0600으로 설정되어 있어야 한다.
