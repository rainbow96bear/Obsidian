# 기술 스택
### server

Golang

-----

# 프로젝트 결심 이유
websocket을 활용한 채팅은 Node.js로 구현해보았기에 새로운 방법을 고민하게 되었고 gRPC에 대한 이해를 위하여 결정하게 되었습니다.

# gRPC
gRPC는 서비스 정의, 매개변수 및 반환 유형을 사용하여 원격으로 호출할 수 있는 메서드를 지정한다는 아이디어를 기반으로 합니다.
<img src="/assets/Pasted image 20240214180821.png">
gRPC 클라이언트와 서버는 Google 내의 서버부터 개인 데스크톱까지 다양한 환경에서 실행되어 서로 통신할 수 있으며, gRPC에서 지원하는 언어 중 어떤 것이든 사용하여 작성할 수 있습니다.

[[gRPC 자료 조사]]

-----
# 문제점
채팅 기능을 웹에서 구현하고 싶었으나 gRPC를 서버간의 통신이 아닌 웹 브라우저와 통신 구현에 어려움이 발생   
## gRPC-Gateway
<img src="/assets/Pasted image 20240219181244.png">
프론트엔드 플랫폼에서 HTTP 호출을 통해 간접적으로 gRPC 메시지를 소비하는 방법  

결국 Reverse Proxy에게 RESTful API로 전달하게 되므로 성능 개선에 의미가 적다고 생각하였습니다.   
gRPC에 대한 경험이라도 쌓기 위하여 CLI를 활용한 채팅을 구현하였습니다.

# 결과
<img src="/assets/rainbowbear_20240208_210024.gif">