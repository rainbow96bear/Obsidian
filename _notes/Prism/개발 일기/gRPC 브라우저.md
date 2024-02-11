grpc 서비스란?



react에서 grpc 사용

https://github.com/grpc/grpc-web/releases
위 사이트에서 protoc-gen-grpc-web-1.5.0-windows-x86_64.exe 다운

npm install google-protobuf grpc-web 

protoc --proto_path=. chat.proto --js_out=import_style=typescript:.\ts_out --grpc-web_out=import_style=typescript,mode=grpcwebtext:.\grpc-web_out --plugin=protoc-gen-grpc-web=C:\protoc\bin\protoc-gen-grpc-web-1.5.0-windows-x86_64.exe

protoc --proto_path=. chat.proto --js_out=import_style=commonjs:.\ts_out --grpc-web_out=import_style=commonjs,mode=grpcwebtext:.\grpc-web_out --plugin=protoc-gen-grpc-web=C:\protoc\bin\protoc-gen-grpc-web-1.5.0-windows-x86_64.exe

protoc --proto_path=. chat.proto --js_out=import_style=commonjs:.\js_out --grpc-web_out=import_style=typescript,mode=grpcwebtext:.\grpc-web_out --plugin=protoc-gen-grpc-web=C:\protoc\bin\protoc-gen-grpc-web-1.5.0-windows-x86_64.exe

protoc -I. --js_out=import_style=commonjs,binary:gen/typescript --grpc-web_out=import_style=typescript,mode=grpcwebtext:gen/typescript *.proto --plugin=protoc-gen-grpc-web=C:\protoc\bin\protoc-gen-grpc-web-1.5.0-windows-x86_64.exe