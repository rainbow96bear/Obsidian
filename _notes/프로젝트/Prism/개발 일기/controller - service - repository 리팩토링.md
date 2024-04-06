# 목차
1. controller - service - repository 란?
2. 폴더
3. 참고 자료

-----
# controller - service - repository 란?
소프트웨어 디자인 패턴 중 하나로 계층 구조를 활용하여 각 계층이 특정 역할을 수행하도록 구조화하는 방식
## controller
사용자의 입력을 받아 해당하는 서비스 메소드를 호출

## service
비즈니스 로직을 처리하고 데이터의 가공 및 처리를 담당

## repository
데이터베이스나 외부의 데이터에 접근하여 CRUD 연산을 담당

<img src = "/assets/Pasted image 20240204011033.png">

- 장점
	- 코드의 재사용성이 높아진다.
	- 작업이 분리 되어 있기에 유지보수가 쉽다. (ex. DB문제면 repository를 확인, 로직 문제면 service를 확인)
	- 테스트하기 쉽다. (작업 단위로 메서드를 만들었기에 각 메서드를 테스트 할 수 있다.)
	- 코드가 깔끔하다.
- 단점
	- 아직 익숙하지 않아 작업이 오래 걸린다.

-----

# 폴더
### handler
사용자의 요청을 처리한 후 뷰에 모델 객체를 넘겨주는 역할
``` go
// users handler
func (u *UsersHandler)RegisterHandlers(r *mux.Router) {
	r.HandleFunc("/info", u.User.GetInfo).Methods("GET")
	
    r.HandleFunc("/profiles/{id}/personaldatas", u.Profile.GetUserProfile).Methods("GET")
	r.HandleFunc("/profiles/{id}/personaldatas", u.ProfilesMiddleware.CheckAccess(u.Profile.UpdateUserProfile)).Methods("PUT")
	
    r.HandleFunc("/profiles/techlist",u.Techs.GetTechList).Methods("GET")
	r.HandleFunc("/profiles/{id}/techs", u.Techs.GetUserTechList).Methods("GET")
	r.HandleFunc("/profiles/{id}/techs", u.ProfilesMiddleware.CheckAccess(u.Techs.UpdateUserTechList)).Methods("PUT")
}
```
요청의 경로에 따라 실행할 service의 메서드를 구별하여 실행   
필요 시 미들웨어를 사용하여 접근 권한 등을 확인
### service
controller에 의하여 호출되고 사용자의 요구사항을 처리하는 역할
``` go
// service - profile 정보 제공
func (p *Profile)GetUserProfile(res http.ResponseWriter, req *http.Request) {
	vars := mux.Vars(req)
	id := vars["id"]
	tx, err := mysql.DB.Begin()
	if err != nil {
		log.Println("service/profiles.go : DB Begin 오류", err)
		tx.Rollback()
		http.Error(res, "Internal Server Error", http.StatusInternalServerError)
		return
	}
```
요청에 대하여 server에서 처리할 작업을 실행하며 DB가 필요한 경우 tx를 생성하여 repository 메서드에 tx를 전달
### repository
service에 의하여 호출되고 DB의 CRUD 작업
``` go
// repository - profile 테이블에 user id와 profile id를 Insert
func (p *ProfileRepository)Create(tx *sql.Tx, id string) (string, error) {
	query := "INSERT INTO profile(id, user_info_User_id) VALUE(?, ?)"
	_, err := tx.Exec(query, id, id)
	if err != nil {
		return "", err
	}
	return id, nil
}
```
각 메서드가 실행시킬 query문을 가지고 있고 결과를 반환하도록 설계
### DTO (Data Transfer Object)
데이터를 전송하기 위한 객체
``` go
package dto

type Personaldata struct {
	Id                 string   `json:"id"`
	Nickname           string   `json:"nickname"`
	One_line_introduce string   `json:"oneLineIntroduce,omitempty"`
	Hashtag            []string `json:"hashtag,omitempty"`
}
```
client에 전달할 정보에 대한 자료 구조와 json 변환에 대한 key 정의

-----

# 참고 자료
- [https://gallery-k.tistory.com/310](https://gallery-k.tistory.com/310) : 레이어드 아키텍처 패턴
- [https://www.joinc.co.kr/w/man/12/golang/robust](https://www.joinc.co.kr/w/man/12/golang/robust) : golang 구조화
- [https://velog.io/@qowl880/ControllerServiceRepository-%EC%B0%A8%EC%9D%B4%EC%A0%90](https://velog.io/@qowl880/ControllerServiceRepository-%EC%B0%A8%EC%9D%B4%EC%A0%90) : controller - service - repository 개념
- [https://frozenpond.tistory.com/113](https://frozenpond.tistory.com/113) : 파일 구조 참고