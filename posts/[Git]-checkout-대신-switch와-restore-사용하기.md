---
date: '2020-12-29'
title: '[Git] checkout 대신 switch와 restore 사용하기'
author: 'SeungDuk Seo'
tags: ['git', 'checkout', 'switch', 'restore']
---

![git_logo](./images/Git-logo.png)


1~2년 전쯤 부터 source tree 같은 git gui client를 사용하지 않고 git cli를 사용하기 시작하면서 자주 쓰는 기본적인 명령어 들은 손에 익기도 했고 별 생각없이 사용하고 있었는데 최근 branch를 변경 하면서 작업할 일이 많아지면서 문득 `checkout`을 branch 변경과 변경사항 복구 할 때 두 가지 상황에서 모두 사용 하는 것이 잘못된 사용이 아닌가 하는 생각이 들어 찾아봤더니 작년에 릴리즈된 `2.23`버전에서 이미 `switch`와 `restore`로 분리되고 `checkout`은 `git help`에서도 빠져있는걸 확인했다.

물론 `checkout`이 동작하지 않는 것은 아니지만 이미 git의 feature에서 빠져버린 `checkout`대신 `switch`와 `restore`를 사용하고자 간단히 기능을 정리해봤다.

## git switch
`checkout`에서 branch를 변경/생성하는 기능을 지원한다.

- branch를 변경하고자 할 때는 기존과 같이 사용하되 명령어만 `checkout`에서 `switch`로 변경해주면 된다.
``` bash
$ git switch develop
```

- branch를 새로 생성하고자 할 때는 기존에 사용하던 `-b` 옵션을 `-c`로 변경해주면 된다.
``` bash
$ git switch -c feature/xxx
```

## git restore
`checkout`에서 변경사항을 복구 해주는 기능을 지원 한다.

- 변경사항을 되돌리고 싶을 때는 `checkout`사용법과 완전히 동일하다.
``` bash
$ git restore .
$ git restore index.js
```

- stage된 파일을 복구하고 싶을 때는 `-S, --staged`를 option으로 넘겨주면 된다.
``` bash
$ git restore --staged index.js
```
`checkout`엔 없던 기능이 새로 생겼다! 기존엔 `git reset HEAD index.js`와 같이 `reset`명령어를 사용했어야 했는데 앞으로는 `--staged` 명령어로 해결할 수 있게 됐다.

`checkout` 명령어가 분리된 사실을 안지 한달 가까이 되어 가는 것 같은데 의도적으로 분리해서 사용하려고 해도 한번 씩 습관적으로 `checkout`을 사용하게 된다...

그래도 계속 의식하면서 사용하다보면 언젠간 손에 익지 않을까 하면서 사용중이다.
