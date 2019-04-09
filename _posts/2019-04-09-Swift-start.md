---
title: 'Swift로 API 호출 함수 테스트 하기'
date: 2019-04-03 23:37:00
categories: tutorial
tags: swift ios TIL
---

안녕하세요, 괴짜 개발자 namedboy 입니다.😗

오랜만의 포스팅이네요.
회사일에 놀러가는 것 까지 겹치니 블로그를 전혀 신경 못쓰고 다시 버려두고 있네요.

올해는 블로그를 다시 버리지 않기로 작정했기 때문에 여러가지 내용들을 포스팅 하려고 합니다!
그중에 요즘은 ios 개발을 시작하게 되어 그와 관련된 내용을 적어보고자 합니다.

같이 공부해요~!! 😆

먼저 개발환경은 이렇습니다.

- OS: MacOS Mojave v10.14.4
- Tool: xCode, AppCode
- Version: Swift 5

최근에 나온 Swift 5를 사용해서 작업을 해보고 있어요.

먼저 기본적인 세팅을 해야 하는데 이 부분은 다음에 다시 다루기로 하고 오늘은 코드 조각을 가지고 얘기를 해보려고 합니다.

일단 호출할 API URL은 http://date.jsontest.com/?service=ip 입니다.
간단하게 내 IP값을 JSON 형태로 반환시켜주는 URL 입니다.

위 URL을 복사해서 curl로 요청해보면 아래와 같은 리턴 값을 줍니다.

```bash
$ curl -i http://date.jsontest.com/?service=ip
HTTP/1.1 200 OK
Access-Control-Allow-Origin: *
Content-Type: application/json
X-Cloud-Trace-Context: 0215469bca9a9b0db2fe0c0ec0155ad5
Date: Tue, 09 Apr 2019 14:53:28 GMT
Server: Google Frontend
Content-Length: 26

{"ip": "211.177.225.234"}
```
바로 위에 ip값이 json 데이터 형태로 리턴된게 보이시나요?ㅎ

그럼 본격적으로 Swift에서 호출하는 코드조각을 볼까요?

```swift
func getMyIP(compilationHandler: @escaping (UserInfo) -> Void) {
        guard let url:URL = URL(string: "http://date.jsontest.com/?service=ip") else {
            return
        }
        var urlReq:URLRequest = URLRequest.init(url: url)
        
        urlReq.httpMethod = "GET"
        urlReq.allHTTPHeaderFields = ["Content-Type":"application/json"]
        
        let IPTask = URLSession.shared.dataTask(with: urlReq) { (data, res, err) in
            if let data = data {
                let jsonData = try? JSONDecoder().decode(UserInfo.self, from: data)
                guard let rsData = jsonData else {
                    return
                }
                compilationHandler(rsData)
            }
        }
        
        IPTask.resume()
    }
```
위와 같은 형태의 코드로 API를 호출 합니다. 대략적으로 코드가 읽히시나요?

`guard`를 사용해서 scope를 지정해주고 `URLRequest`를 사용해서 method type 세팅과 header 값을 지정해 줍니다.

그 이후에는 url을 호출하기 위해 `URLSession`이란 것을 사용해 Task로 만들어 data 값을 받았을 때 `JSONDecoder()`를 사용해 `UserInfo`라는 모델에 데이터를 바인딩합니다.

에러는 `JSONDecoder()`의 바로 아래 `guard`에서 다시 잡아줍니다.

실제로 실행은 제일 하단의 `IPTask`가 가진 메소드 `resume()`를 실행하면서 내부 프로세스로 실행 됩니다.

아래는 구조체로 사용한 `UserInfo`입니다.

```swift
import Foundation

public struct UserInfo: Codable {
    public let ip: String
}
```

위 코드가 제대로 실행이 되었다면 UserInfo.ip에 사용자의 IP가 들어가게 됩니다.

코드만 가지고 간단하게 설명하려고 하니 꽤 많은 부분이 생략 되었습니다.

어려운 부분은 아니나 Swift를 잘 모르시는 분이라면 하나하나 메소드나 사용된 클래스들의 의미를 곱씹으면서 보시다 보면 분명 API를 호출하는 것을 만드는데 무리 없이 하실 수 있으실 겁니다!

P.S 아래 코드는 `info.plist`에 추가된 코드 입니다. 이 부분이 없으면 https가 아닌 url은 실행되지 않는다고 하네요~ 참고하시고 즐거운 코딩라이프 되세요!
```xml
<key>NSAppTransportSecurity</key>
	<dict>
		<key>NSAllowsArbitraryLoads</key>
		<true/>
	</dict>
```

오늘은 여기까지 입니다!

도움이 되었길 바라며 저는 이만 뿅!
