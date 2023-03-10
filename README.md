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

# 0.4 Recap

1. Nodemon은 우리의 프로젝트를 살펴보고 변경 사항이 있을 시 서버를 재시작해주는 프로그램.
2. 여기서는 서버를 재시작하는 대신에 babel-node를 실행하게 되는데, Babel은 우리가 작성한 코드를 일반 NodeJS 코드로 컴파일 해주는데, 그 작업을 src/server.js 파일에 해준다.
3. server.js 파일에서는 express를 import하고, express 어플리케이션을 구성하고, 여기에 view engine을 pug로 설정하고, views 디렉토리가 설정되고, public 파일들에 대해서도 똑같은 작업을 해주고 있다.
4. public 파일들은 frontend에서 구동되는 코드다. server.js는 backend에서, app.js는 frontend에서 구동된다.
5. app.get("/\*", (req, res) => res.redirect("/"));
   => 어떤 url로 들어갈려고 해도, home으로만 돌아오게 된다.

# 1.1 HTTP vs WebSockets

1. HTTP, WebSockets => protocol의 종류
2. backend(server)는 client(user)의 request가 오면 response만 할 뿐, client를 잊어버린다.(stateless)
3. http protocol => request에 대한 response만 있을 뿐, 저장하거나 다른 기능은 없다.
4. browser가 websocket request를 보내면, 서버는 받거나 거절하기를 한다. 이런 왔다갔다가 한번 성립되면 이 연결을 성립(establish)라고 한다.
5. websocket으로 인한 연결 상태에서, 서버는 request를 기다리지 않고, 답장을 할 수 있다.(bi-directional(양방향의) 연결이기 때문)
6. websocket의 연결 상태에서는 서버만 response를 할 수도 있다.

# 1.2 WebSockets in NodeJS

1. nodejs로 websocket 서버를 만들어 보자.
2. ws는 websocket의 핵심이다.

# 1.3 WebSocket Events

1. backend와 frontend 사이의 connection(연결)을 만들어 보자.
2. websocket은 listen할 특정한 event명이 정해져 있다.(그것들을 잘 사용하자.)
3. ws(websocket), wss(sebsocket secure)로 지정을 해서, http가 아닌 url로 우리의 정보를 제공한다.
4. webSocket은 브라우저와 서버 사이의 연결

# 1.4 WebSocket Messages

1. server.js에서, socket.on("message", message => {
   console.log(message.toString('utf8'));
   });
2. addEventListener는 자바스크립트 함수이고 on은 NodeJS 함수
