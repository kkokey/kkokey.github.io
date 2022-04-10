---
title: 'Android sign key 만드는 법'
date: 2021-12-17 01:00:00
categories: android
tags: 개발자 developer android signkey keytool
comments: true
---

```
$ keytool -genkey -v -keystore keystore -alias nct -keyalg RSA -keysize 2048 -validity 10000 -keypass password -storepass password -dname "CN=nct, OU=team, O=product, L=SEOUL, S=SEOUL, C=ko"
```

keypass와 storepass의 경우 동일한 값을 사용해야 한다.

## [출력내용]
<pre>
키 저장소 비밀번호 입력:  
새 비밀번호 다시 입력:  
이름과 성을 입력하십시오.  
  [Unknown]:  nct  
조직 단위 이름을 입력하십시오.  
  [Unknown]:  team  
조직 이름을 입력하십시오.
  [Unknown]:  product
구/군/시 이름을 입력하십시오?
  [Unknown]:  seoul
시/도 이름을 입력하십시오.
  [Unknown]:  seoul
이 조직의 두 자리 국가 코드를 입력하십시오.
  [Unknown]:  ko
CN=nct, OU=team, O=product, L=seoul, ST=seoul, C=ko이(가) 맞습니까?
  [아니오]:  y

다음에 대해 유효 기간이 10,000일인 2,048비트 RSA 키 쌍 및 자체 서명된 인증서(SHA256withRSA)를 생성하는 중
    : CN=nct, OU=team, O=product, L=seoul, ST=seoul, C=ko
[nctBitStepKey을(를) 저장하는 중]

</pre>
