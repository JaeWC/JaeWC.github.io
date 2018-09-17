---
layout: post
title: "[Setting] Installing node.js"
subtitle:   "Setting Environment"
categories: etc
tags: Setting
comments: true
---

# Node.js

[Node.js](https://nodejs.org/en/)는 구글에서 개발한 고성능 JavaScript 엔진으로 구성된 Server Side 개발용 소프트웨어 플랫폼이다.

기본적으로 자바스크립트는 웹 브라우저에서 실행되는데, Node.js 런타임 환경에서는 모든 종류의 서버 사이드 도구들을 제공하여 자바스크립트로 서버 개발을 할 수 있다. 따라서 자바스크립트를 이용하여 클라이언트 측(Front-end)과 서버 측(Back-end)을 모두 개발할 수 있다.

> 최근의 개발 Tool들은 노드 기반의 것이 많고, 상위 버전의 노드를 요구하는 경우가 있기 때문에 여러 버전의 노드를 설치할 필요가 있다. 이때, [NVM](https://github.com/creationix/nvm)은 컴퓨터에 다양한 버전의 노드를 설치할 수 있게 해주는 툴이다.



### 설치

NVM 문서에 있는 다음의 설치 스크립트로 설치한다.

```text
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash
```

설치가 완료되었다면, ~/.nvm 폴더에 nvm rpository를 복제하고 terminal profile에 아래와 같은 source line들이 추가된다. 만약 `nvm: command not found`와 같은 오류 메시지가 뜰 경우, 아래의 실행 스크립트 내용을 직접 terminal profile file에 추가해주면 된다.(`~/.bash_profile, ~/.zshrc, ~/.profile, or ~/.bashrc`)

```text
export NVM_DIR="${XDG_CONFIG_HOME/:-$HOME/.}nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
```

nvm이 제대로 설치 되어있는지는 다음의 명령어로 확인한다.

```text
command -v nvm
```

가장 최근 버전의 node.js 설치를 위해서는 다음의 명령어로 확인한다.

```text
nvm install 8.12.0
```

설치된 node.js를 바로 사용하기 위해서는  다음의 명령어를 사용한다.

```text
nvm use 8.12.0
```

추가적으로 설치된 node.js를 확인할 때는 다음을 확인하면 된다.

```text
nvm list
```



