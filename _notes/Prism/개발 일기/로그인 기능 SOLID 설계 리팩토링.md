
# 목차
1. Login Interface
2. Token Interface
3. 파일 트리

-----

# Login Interface

## 초기 계획
```go
// User 인터페이스
type I_User interface {
	// 로그인 메서드
	Login(res http.ResponseWriter, req *http.Request)
}

// Interface를 활용한 Login
func Login(u I_User, res http.ResponseWriter, req *http.Request) {
	u.Login(res, req)
}
```

위와 같이 설계 후 Kakao 로그인과 Admin 로그인을 I_Login의 Login을 사용하려고 하였으나 로그인 요청은 path를 통하여 분류를 하기 때문에 큰 의미가 없다고 판단.

## 결과

**/Routers/OAuth/Kakao/Kakao.go**
```go
kakaoUser := &KakaoUser.KakaoUser{}

r.HandleFunc("/login", kakaoUser.Login).Methods("GET")
```

**/Structs/Users/KakaoUser/KakaoUser.go**
```go
func (u *KakaoUser) Login(res http.ResponseWriter, req *http.Request) {
	OAuthLogin(res, req)
}
```
이러한 방식으로 KakaoUser.go를 수정하여도 kakao.go는 수정하지 않도록 구현

-----

## SRP 적용?

### 수정 전

```go
func OAuthLoginAfterProcess(res http.ResponseWriter, req *http.Request) (error) {
	// 함수 내용
	http.Redirect(res, req, "http://localhost:3000/home", http.StatusFound)
}
```
Router에서 oAuthLoginAfterProcess 실행하면 관련된 작업을 하고 로그인을 위한 Redirect 실행

### 수정 후
```go
func (k *KakaoUser)AfterProcess(res http.ResponseWriter, req *http.Request) {
	token, err := I_Token.GetToken(kakaoToken, res, req)
	if err != nil {
		log.Println(err)

        http.Error(res, err.Error(), http.StatusInternalServerError)
	}
	kakaoUser, err := getUserInfo(token.(*KakaoToken.Token).Access_token)
	if err != nil {
		log.Println(err)
		http.Error(res, err.Error(), http.StatusInternalServerError)
	}
	// 추가적인 내용
	http.Redirect(res, req, "http://localhost:3000/home", http.StatusFound)
}
```

Router가 KakaoUser의 메서드(AfterProcess)를 실행하도록 변경   
AfterProcess는 필요한 작업을 함수로 호출   
호출된 함수가 완료되면 Redirect   
장점 : 기존의 AfterProcess라는 메서드는 결과가 Redirect이기에 테스트가 불편, 수정 후 각각의 기능을 함수로 불러오기에 테스트가 가벼움

-----

# Token Interface

## Interface
```go
type I_Token interface {
	GetToken(res http.ResponseWriter, req *http.Request) (I_Token, error)
}

func GetToken(t I_Token, res http.ResponseWriter, req *http.Request) (I_Token, error) {
	token, err := t.GetToken(res, req)
	if err != nil {
		return nil, err
	}
	return token, nil
}
```

추후에 다른 OAuth를 적용하게 될 경우 기능 추가에 개방적이도록 Interface 사용

-----

# 파일 트리

구조체를 Structs에 인터페이스는 Interfaces에 모으고 Router에 대한 내용은 Routers로 분류

## 변경 전
```bash
prism_back
├─admin
│  ├─middleware
│  ├─tech
│  └─user
├─DataBase
│  └─MySQL
├─kakao
│  └─login
├─session
└─user
    ├─lightInfo
    └─profile
```

## 변경 후
```bash
prism_back
├─DataBase
│  └─MySQL
├─session
├─Interfaces
│  └─I_Token
├─Routers
│  └─Admin
│      └─User
│  └─OAuths
│      └─Kakao
└─Structs
	├─Tokens
	│  └─KakaoToken
	└─Users
	    ├─Admin
	    └─KakaoUser
```
