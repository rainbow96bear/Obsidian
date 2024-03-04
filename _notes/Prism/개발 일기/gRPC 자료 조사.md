
# 목차
1. gRPC 소개
2. gRPC 통신 방법
3. gRPC-Web의 메커니즘
4. gRPC-Gateway

-----

# gRPC 소개
gRPC는 서비스 정의, 매개변수 및 반환 유형을 사용하여 원격으로 호출할 수 있는 메서드를 지정한다는 아이디어를 기반으로 합니다.
![[Pasted image 20240214180821.png]]
gRPC 클라이언트와 서버는 Google 내의 서버부터 개인 데스크톱까지 다양한 환경에서 실행되어 서로 통신할 수 있으며, gRPC에서 지원하는 언어 중 어떤 것이든 사용하여 작성할 수 있습니다.

## gRPC와 net/rpc의 차이

go언어에서 net/rpc 패키지를 활용하여 rpc 통신을 하는 방법도 있습니다. 

### net/rpc 패키지
- 서버와 클라이언트가 모두 go언어로 작성되어야 한다는 제약이 발생
- 교환되는 데이터가 기본적으로 go에서 사용하는 gob 포맷으로 인코딩 되기 때문
### gRPC
- gRPC를 사용하면 protoc을 활용하여 각 언어에 맞는 서버와 클라이언트를 작성하여 데이터 교환 포맷인 프로토콜 버퍼를 사용하기에 언어 제약 없이 사용할 수 있음
## 프로토콜 버퍼
프로토콜 버퍼는 정의 언어(.proto 파일에서 생성)와 데이터와 상호 작용하기 위해 프로토 컴파일러가 생성하는 코드   
구조화된 데이터를 직렬화하기 위한 언어 중립적이고 플랫폼 중립적인 확장 가능한 메커니즘   
JSON과 비슷하지만 더 작고 빠르며 한 번 데이터를 어떻게 구조화할지 정의한 다음, protoc으로 생성된 소스 코드를 사용하여 다양한 데이터 스트림 및 다양한 언어를 사용하여 쉽게 쓰고 읽을 수 있음   
## protoc
프로토콜 버퍼 컴파일러로 protocol Buffers를 go언어로 생성하기 위해서는 컴파일러 플러그인인 protoc-gen-go를 사용

## proto 작성

```proto
service HelloService {
  rpc SayHello (stream HelloRequest) returns (HelloResponse);
}

message HelloRequest {
  string greeting = 1;
}

message HelloResponse {
  string reply = 1;
}
```
### syntax
프로토콜 버퍼 파일이 어떤 버전의 프로토콜 버퍼를 사용하는지 정의합니다.
### service
gRPC 서비스를 정의하고 원격에서 호출 가능한 메서드를 포함하며, 클라이언트와 서버 간의 통신을 정의합니다.
### message
클라이언트와 서버 간에 주고받는 데이터 형식을 정의합니다.
### stream
여러 메시지를 연속적으로 주고 받을 수 있도록 합니다.

-----
# gRPC 통신 방법

- 단항 RPC
- 서버 스트리밍 RPC
- 클라이언트 스트리밍 RPC
- 양방향 스트리밍 RPC

-----

# gRPC-Web의 메커니즘
1. 브라우저는 gRPC-Web 클라이언트 호출
2. Envoy 프록시는 Protobuf 정의 요청이 포함된 호출을 수신
3. Envoy는 이를 HTTP/2 gRPC 호출로 변환하여 gRPC 서버로 전달
4. gRPC 서버는 요청을 처리하고 응답을 Envoy에 반환
5. Envoy는 gRPC 응답을 다시 gRPC-Web 형식으로 변환하여 클라이언트에 전달

-----
# gRPC-Gateway
![[Pasted image 20240219181244.png]]
프론트엔드 플랫폼에서 HTTP 호출을 통해 간접적으로 gRPC 메시지를 소비하는 방법  

-----

# 참고 자료
- [https://grpc.io/docs/what-is-grpc/introduction/](https://grpc.io/docs/what-is-grpc/introduction/): gRPC docs - gRPC 소개
- https://protobuf.dev/overview/ : 프로토콜 버퍼 document - 프로토콜 버퍼 소개
- 실무에 바로 쓰는 go언어 핸즈온 가이드(책)
- https://grpc.io/blog/postman-grpcweb/ : gRPC가 websocket을 대체할 수 있는가?
- https://blog.banksalad.com/tech/making-typescript-grpc-stub-generator/ : gRPC-web을 사용하는 방법