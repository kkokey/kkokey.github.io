---
title: '`개발자 테스트`란 무엇인가?'
date: 2020-03-15 21:20:00
categories: Basic
tags: test, development, tdd
comments: true
---

나는 개발자로서 테스트의 중요성은 아무리 강조해도 지나치지 않다고 생각한다.

개발 업계에서 테스트는 크게 두 가지 의미로 쓰인다고 생각한다.

1. 개발자가 하는 개발자 테스트
2. QA(Quality Assurance) 부서나 팀에서 하는 품질 보증을 위한 테스트

내가 얘기하고자 하는 것은 바로 1번이다.

개발자가 만들어낸 결과물에 대해 책임지는 개발자 테스트다.

많은 개발자가 얘기하는 TDD(Testing Driven Development)가 있다.

개발 전 설계 단계에서 고려하여 생각한 설계 내용을 테스트를 먼저 만들면서 검증하고, 실제 기능이 동작하는 코드를 개발하는 개발 방법론 중 하나다.

설계 후 테스트를 먼저 만드는 것이 테스트가 개발 전체를 리드한다는 개념으로 테스트 주도 개발이란 이름이 붙었다.

여기서 내가 얘기하고 싶은 내용은 TDD는 아니라고 분명히 얘기하고 싶다.

TDD는 내가 얘기하고자 하는 내용에서부터 2~3단계는 더 높은 수준이다.

나는 개발하면서 아래 나열한 단계를 밟아가며 개발을 한다.

1. 개발하고자 하는 기능의 요구사항을 정의하고 분석한다.
2. 알고리즘 설계가 필요한가? 필요 없다면 설계가 필요한지 필요 없는지 확인한다.
3. 주요한 핵심 기능을 1차로 설계하고 대략적인 개발 난이도를 평준화한다.
4. 설계가 끝나면 설계한 대로 개발을 시작한다.
    - 여기서 가능하다면 테스트 코드를 작성한다.
5. 개발한 결과물이 정의하고 분석한 내용과 맞는지 확인한다.
6. 마지막으로 기능 전체를 테스트한다.
7. 코드를 리팩토링하면서 개발을 마무리한다.

이 글에서 얘기하는 테스트는 바로 6번이다.

개발 도중 테스트는 당연하다. 물론 개발 도중 테스트가 제대로 완료된 상태라면 6번에서 큰 문제가 없이 동작해야 한다.

하지만 개발하는 도중 기능의 테스트가 제대로 이루어지지 않았다면 6번에서 당연히 막힌다.

그러면 해당 기능을 다시 확인하고 수정해야 한다.

보통은 5번까지 작업하고 6번은 제대로 수행하지 않고 결과물을 운영 서버에 반영하거나 QA를 하게 된다.

이렇게 하면 어떤 문제가 발생할까?

일반적인 상황을 가정해보자.

- 개발자 A가 화면에 필요한 기능 5가지를 개발한다고 생각해보자.
- 기능을 3개를 만든다. 생각보다 빠르게 진행이 되었고 현재까지는 문제가 없는 것 같다.
- 나머지 기능 2가지는 예상하는 난도도 높고 실제로 개발하는 기간도 늘어져서 마지막에 마지막까지 개발하게 되었다.
- 어떻게든 일정을 맞춰서 개발을 완료했다.
- 하지만 전체 테스트를 못 했다. 앞에서 만든 3개의 기능은 앞서 테스트할 때 잘 동작 했으니 넘어가고 나중에 개발한 기능 2개만 테스트했다.
- 내가 의도 했던 대로 잘 동작하는 것을 확인했다.

여기서 문제점이 무엇이라고 생각하는가?

나도 수도 없이 했던 실수였고, 많은 개발자가 이런 부분을 놓친다고 생각한다.

다음으로 넘어가기 전에 잠시 생각해보자.  
개발자 A는 무엇을 실수한 걸까.  

---

눈치가 빠른 분은 발견했으리라 싶다.

개발 결과물의 기능은 총 5가지인데 3가지는 5개 기능이 모두 개발된 후에 다시 테스트하지 않았다는 것이다.

이유는 많았을 것이다.

- 개발할 시간이 부족해서..
- 앞에서 테스트했으니 별문제 없겠지..
- 마지막에 개발한 2개 기능 잘 동작하니까 괜찮겠지..
- 테스트하다 늦어지면 일정이 꼬이는데...
- 테스트는 한번 만 하면 되는 거 아닌가??

 어떤 이유를 대도 전부 핑계다.

기능을 5개를 개발하겠다고 했으면 최소한 그 5개는 개발 완료 후 해당 기능이 제대로 동작하는지 전부 테스트하고 확인을 해야 했다.

그 테스트가 완료되지 않으면 개발은 끝난 것이 아니다.

*"테스트는 테스트 부서에서 하는 거 아닌가요?"* 라고 하는 분이 계신다면 "최소한 제 기준에서는 아닙니다"라고 말씀드리고 싶다.

나는 `개발자 테스트`를 이렇게 정의한다.

- 개발자가 만든 결과물에 대해서 요구사항에 부합하게 동작할 수 있도록 테스트하는 것.

물론 지금까지 내가 개발한 내용을 보면 저 기준에 부합하지 않는 경우도 많다.

지금까지 개발해오면서 개발자 테스트는 저 기준에 준하지 않으면 하지 않는 것이나 다름없다는 것을 알았다.

부디 개발자 테스트와 QA를 혼동하는 개발자가 줄어들길 바라며 글을 줄입니다.
