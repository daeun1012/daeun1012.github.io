---
layout: post
title:  이더리움 뭐라도 해보자!!
tags: Ethereum
comments: true
---
요즘 이래저래 너무 의욕상실이었다...
다시 시작해야지...!
으쌰으쌰!!
<br><br>
<h1>이더리움 개발을 위한 TestRPC를 설치하자.</h1><br>
TestRPC : Ethereum client for testing and development<br>
in-memory 블럭체인, 간단히 블럭체인 시뮬레이터라고 생각하면 된다.<br>

[ethereumjs/testRPC 설치](https://www.npmjs.com/package/ethereumjs-testrpc)

```
    npm install -g ethereumjs-testrpc
```

설치 후 실행 시켜보면 지갑주소 10개와 해당하는 PrivateKey 10개를 볼 수 있다.

```
    testrpc
```

<h1>다음으로 Truffle 을 설치해보자.</h1>
Truffle은 ehtereum CLI 툴이다.

[Truffle](https://github.com/trufflesuite/truffle)

```
    npm install -g truffle
```

<h1>설치가 완료되었으면 임의 위치에 폴더를 생성한뒤 샘플을 따라해보자.</h1>
문서상으론 truffle init webpack 이라는데 안된다. unbox 해야한다.

[BUILDING & TESTING A FRONTEND APP WITH TRUFFLE 3.0](http://truffleframework.com/tutorials/creating-a-cli-with-truffle-3)

```
    truffle unbox webpack
```

완료후 build 해보자.
```
    truffle build
```

에러난다. 에러나란다.....ㅎㅎㅎ
자 이제 실행해보자!!!
.sol 파일들 컴파일 해주고

```
    truffle compile
```

testRPC 켜놓으세요, 그리고 포트도 확인하시구요.

```
    truffle migrate
```

자알된다아.
블럭을 5개나 만드넹.

다음으로 웹으로 실행해보기 위한 단계이다.
webpack build 해보자.

```
    npm run build
```

ㅎㅏ지마세요 에러나요.
저는 truffle 4.x 대라서 에러나는거 같아요.

참고사이트<br>
[https://medium.com/@mvmurthy/full-stack-hello-world-voting-ethereum-dapp-tutorial-part-1-40d2d0d807c2](https://medium.com/@mvmurthy/full-stack-hello-world-voting-ethereum-dapp-tutorial-part-1-40d2d0d807c2)
[https://winterj.me/prepare_smart_contract_deploying/](https://winterj.me/prepare_smart_contract_deploying/)
