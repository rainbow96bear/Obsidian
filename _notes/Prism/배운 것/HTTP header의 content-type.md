# 목차
1. Content-Type 헤더
2. MIME란?
3. multipart란?
4. form-data와 mixed 차이

-----

# Content-Type 헤더
HTTP 헤더 중 하나인 Content-Type은 MIME 형식을 지정하는 데 사용됩니다. 클라이언트와 서버 간에 전송되는 데이터의 형식을 명시하는 역할을 합니다.

-----

# MIME이란?
Multipurpose Internet Mail Extensions의 약어로 인터넷의 전자 메일에서 사용되는 문자 데이터를 표현하기 위한 형식 표준을 의미합니다.

## MIME 형식
- text/plain
	- 텍스트 데이터를 나타냄
- text/html
	- HTML 문서를 나타냄
- application/json
	- JSON 형식의 데이터를 나타냄
- image/jpeg, image/png 등
	- jpeg, png등의 이미지를 나타냄
- audio/mpeg, audio/wav 등
	- mpeg, wav등의 오디오를 나타냄
- video/mp4, video/quicktime 등
	- mp4, quicktime 등의 비디오를 나타냄
- multipart/form-data, multipart/mixed 등
	- 여러 부분으로 이루어진 문서나 데이터를 나타냄

-----

# multipart란?
multipart/form-data : 파일 업로드와 함께 텍스트 데이터를 전송
multipart/mixed : 여러 종류의 독립적인 데이터를 함께 전송할 때 사용됩니다. 각 부분은 독립적인 MIME 형식을 가지며, 각각의 부분은 서로 관련 없는 데이터를 나타낼 수 있습니다.

-----

# form-data와 mixed 차이
## multipart/form-data
form-data는 주로 HTML 폼에서 파일 업로드와 함께 텍스트 데이터를 서버로 전송할 때 사용됩니다.
## multipart/mixed
이메일의 본문과 함께 여러 첨부 파일이 있는 경우 사용됩니다.

-----

# 참고 자료
- https://lena-chamna.netlify.app/post/http_multipart_form-data/
- https://eastash.me/http-multipartform-data-feat-react-express-multer