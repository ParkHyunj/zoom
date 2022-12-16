# Noom

Zoom Clone using NodeJS, WebRTC and Websockets.

# nodemon.json

1. exec는 server.js를 실행시킨다.
2. nodemon은 이거 하나만 수행한다.

# dev

1. "dev"는 nodemon을 호출한다.(이것만 한다.)
2. nodemon이 호출되면 nodemon이 nodemon.json을 살펴보고 거기있는 코드를 실행한다.

# 0.2 Server Setup

1. npm run dev 시, SyntaxError: Cannot use import statement outside a module면,
   package.json 최상단에"type": "module",을 추가해서 해결
2. 기본 모듈 시스템이 CommonJS인 Node.js에서 바벨을 통해 ESModule(+ 최신 ES문법)을 사용할 수 있도록 하고 있습니다.
   package.json의 type:module을 추가 하는 건 프로젝트의 모듈 시스템만ESModule로 변경하는 것으로, 바벨은 적용되지 않았을 수 있습니다.
3. npm run dev 시, 'babel-node'은(는) 내부 또는 외부 명령, 실행할 수 있는 프로그램, 또는 배치 파일이 아닙니다.
   나오는 경우, npm i @babel/node -g => -g를 붙여 바벨을 다운받기

# 0.3 Frontend Setup

1. Express로 할 일은 view를 설정해주고, render 해주는 것.
2. pug 파일을 만들었지만, npm run dev하는 데 있어서 not found라고 계속 떠서 직접 instlal함.
