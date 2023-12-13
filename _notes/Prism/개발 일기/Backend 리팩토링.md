# 목차
1. DB와 Session을 setup하는 함수 제거
2. 요청 경로에 따른 분류

-----

# DB와 Session을 setup하는 함수 제거

## 함수 예시

### main.go
```go
var err error
	db, err := sql.Open("mysql", "root:"+os.Getenv("MYSQL_PW")+"@tcp(localhost:3306)/prism")
	if err != nil {
		fmt.Println("Failed to open DB")
	}
	KakaoLogin.SetupDB(db)
	KakaoLogin.SetupStore(store)
	defer db.Close()
```

### kakaologin.go
```go
func SetupDB(db *sql.DB) {
	MainDB = db
}

func SetupStore(store *sessions.CookieStore) {
	Mainstore = store
}
```

기존의 db와 session의 store를 main.go 에서 생성하고 각 package의 메서드를 통하여 값을 전달하는 방식

## 문제점
package가 생성될 때마다 메서드를 호출하여 값을 전달하는 번거로움과 코드가 길어지는 문제

## 수정 후
session.go와 mysql.go를 생성하여 session과 db를 import하여 사용할 수 있도록 변경

### Session.go
```go
var Store *sessions.CookieStore
func SetupStore() {
    Store = sessions.NewCookieStore([]byte(os.Getenv("SECRET_KEY")))
}
```
Store를 외부에서 import 할 수 있게 지정
<br>

### mysql.go
```go
var DB *sql.DB

func SetupDB() {
    DB, err = sql.Open("mysql","root:"+os.Getenv("MYSQL_PW")+"@tcp(localhost:3306)/prism")
    if err != nil {
        fmt.Println("Failed to open DB")
    }
}
```
DB를 외부에서 import 할 수 있게 지정

### main.go
```go
Mysql.SetupDB()
Session.SetupStore()
```
main.go에서 main함수가 실행되면 두 함수를 실행하도록 하여 server가 시작되면 DB와 Store를 생성하도록 설정

-----

# 요청 경로에 따른 분류

## 코드 예시
```go
r.HandleFunc("/userinfo",GetUserInfo_from_Session).Methods("GET")
	
	r.HandleFunc("/kakao/login", KakaoLogin.OAuthLogin).Methods("GET")
	r.HandleFunc("/kakao/withToken", KakaoLogin.OAuthLoginAfterProcess).Methods("GET")
	r.HandleFunc("/kakao/logout", KakaoLogin.Logout).Methods("GET")

```
main.go에서 모든 요청에 대한 경로를 다루는 방식

## 문제점
main.go에 모든 경로가 기록되면 코드가 길어지고 가독성이 떨어짐

## 수정 후
```go
Kakao.RegisterHandlers(r.PathPrefix("/kakao").Subrouter())
UserInfo.RegisterHandlers(r.PathPrefix("/userinfo").Subrouter())
```
Subrouter를 이용하여 main.go의 길이를 줄이고 Subrouter에서 해당 경로를 관리

### kakao.go
```go
package Kakao
import (
	Login "prism_back/kakao/login"
	"github.com/gorilla/mux"
)

func RegisterHandlers(r *mux.Router) {
	r.HandleFunc("/login", Login.OAuthLogin).Methods("GET")
	r.HandleFunc("/withToken", Login.OAuthLoginAfterProcess).Methods("GET")
	r.HandleFunc("/logout", Login.Logout).Methods("GET")
}
```
kakao에 대한 요청은 kakao.go를 거쳐서 수행되도록 정리