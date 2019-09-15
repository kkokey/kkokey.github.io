---
title: 'VSCode python terminal 에러 출력 해결법'
date: 2019-09-16 02:00:00
categories: environment
tags: config vscode error fix solution
---

안녕하세요, 괴짜 개발자 namedboy입니다. 😎

오늘은 Visual Studio Code에서 발생하는 에러 중 하나를 해결하는 방법을 포스팅 하려고 합니다.
심플한 내용이긴 하지만 저 같이 에러 메시지가 표시되는 것마저 짜증나는 분들을 위해 stackoverflow에 올라와 있는 내용을 가져와서 포스팅합니다.

아래에 보면 에러 메시지가 있습니다.
저는 아래 메시지를 파이썬 코드를 실행한 후 터미널에서 만나게 되는데요.
아래 터미널 창을 닫았다가 열기만 하면 무조건 발생하는 에러여서 항상 눈에 거슬렸었습니다.

```bash
nvm is not compatible with the npm config "prefix" option: currently set to "/usr/local"
Run `npm config delete prefix` or `nvm use --delete-prefix v10.15.3 --silent` to unset it.
```

거슬리는것은 그냥 두면 안되겠지요.😁
메시지에 나온대로 동일하게 입력했을 때 문제가 해결된다면 참 좋겠지만, 
그렇지 않았기에 열심히 구글링을 해보았습니다.

[stackoverflow 링크](https://stackoverflow.com/questions/34718528/nvm-is-not-compatible-with-the-npm-config-prefix-option)

위 링크에 답이 있어 추가해봅니다.

아래에 내용이 해당 문제를 해결 할 수 있는 명령어 입니다.
물론 [NODE_VERSION]은 에러 메시지에 나오는 버전을 입력해주어야겠죠?

새로운 터미널을 열어서 아래 2개 명령어를 입력해주고 Visual Studio Code를 재시작해 주면 됩니다!

쉽죠!?

```bash
$ npm config delete prefix 
$ npm config set prefix $NVM_DIR/versions/node/[NODE_VERSION]
```

저는 위 명령어로 해결을 했는데, 혹시 해결이 되지 않는 분은 댓글로 소통해 보아요. :)