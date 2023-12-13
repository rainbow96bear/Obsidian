프로필 페이지 1차 기록에 댓글로 작업에 대한 피드백을 받게 되어 부족한 부분에 대한 보완 작업을 진행하였습니다.   
<br>
테이블의 before와 after에 대한 ERD는 제일 아래에 기록하였습니다.

-----

# 1. 테이블 명, 컬럼 명 통일

## 문제점 : 
테이블 명과 컬럼 명에 규칙이 제각각인 문제   
- 규칙이 없이 작성되는 경우 혼동을 줄 수 있음

## 생각
통일성 있는 테이블 명과 컬럼 명은 혼자 코딩을 하는 경우와 협업을 하는 경우 매우 중요하다고 생각하였습니다.   
이해하기 쉽고 명확한 이름과 정해진 규칙을 사용하여야 작업을 할 때 각각의 이름을 사용하는데 오류를 방지하고 오타를 줄일 수  있다고 생각하여 더 많은 작업이 진행되기 전에 수정하여야 한다고 생각하였습니다.   

## 조치
- 테이블 이름의 모든 문자는 소문자를 사용하고 단어와 단어 사이에 "\_"를 사용
- 컬럼의 첫 글자는 대문자를 사용하여 관계를 맺었을 때 생기는 컬럼의 이름의 경우 테이블 명과 컬럼 명을 구분
- FK의 경우 제일 앞에 테이블 명 + \_컬럼 명
- user의 id 같이 id가 의미가 있는 경우는 User_id 형식으로 지정

-----

# 2. profile테이블의 userinfo_id를 참고하는 것은 추천하지 않음

## 문제점
userinfo 테이블과 profile 테이블은 1:1 관계이고 userinfo의 id를 profile이 PK로 사용하는 관계   
profile과 관련된 테이블은 profile의 userinfo_id를 참고하는 상황   

## 생각
단순히 profile은 userinfo에 관련되어 있고 hashtag, tech, project 등은 userinfo의 id와 profile에 관련이 있으니 userinfo의 id를 건내고 건내는 방식을 하였습니다.   
너무 1차원적인 생각이었다고 느껴집니다.   
hashtag와 tech를 포함하는 것은 profile이기 때문에 userinfo의 id보다 profile에 id 컬럼을 생성하여 id 값을 참조하는 것이 더 좋은 관계라고 생각  

## 조치
- userinfo 테이블과 profile 테이블은 1:1 관계를 유지하되 profile에 profile 번호를 확인할 수 있는 id 컬럼을 추가하고 profile과 관련된 테이블은 id를 참조

-----

# 3. hashtaglist에 id 컬럼이 필요하지 않을까?

## 문제점
hashtag에 id 컬럼이 없이 profile과 N:M의 관계를 가지고 있다보니 hashtaglist_has_profile의 hashtaglist_hashtag와 중복되는 문제

## 생각
처음에 hashtag가 중복되어 저장되지 않기 때문에 PK역할을 하여 id가 필요 없다고 생각
피드백을 듣고 보니 중복되는 문제가 있다는 것을 확인하였고 조치가 필요하다고 생각

## 조치
- hashtag_list 테이블에 id 컬럼을 추가
- 추후에 가장 많이 사용된 hashtag 등을 확인 하기 위하여 count 컬럼 추가

-----

# 4. tech와 techcategory에 대한 이해가 어려움

## 문제 
tech에 대한 분류가 front, back, fullstack등으로 나눌 필요가 있을까 하는 문제

## 생각
처음 생각은 javascript, typescript 등 front와 back 양쪽에서 사용되는 기술 스택에 대하여 front로 활용하는지 back으로 활용하는지 구별을 하기 위하여 테이블을 구성하였습니다.   
이건 프로필에 대한 이해도가 낮아서 생긴 문제라고 생각   
언어에 대한 category가 불필요하다고 생각되었고 본인을 나타내는 hashtag에 front, back을 표현하는 방법으로 대체할 수 있다고 생각

## 조치
- techcategory 테이블을 지우고 tech테이블에 count컬럼을 추가
- count는 추후에 가장 많은 tech 등 활용을 위한 준비

-----

# 5. R_UserInfo에서 아스테리크(\*)로 가져오는 것


```go
query := "SELECT * FROM userinfo WHERE id = ?"
```

## 문제점
피드백 주신분이 실 프로젝트에서 한번도 사용한 적 없는 방법

## 생각
R_UserInfo의 경우 ID가 DB에 저장되어 있는지 확인하기 위한 용도이기 때문에 다른 불필요한 정보까지 담아오는 아스테리크를 사용할 이유가 없다고 생각
위의 경우가 아니어도 가져오는 값이 무엇인지 확실하게 표현하기 위하여 컬럼 명을 사용하는 연습이 필요하다고 생각

## 조치
"SELECT ID FROM userinfo WHERE ID = ?;"
위와 같이 ID값을 가져온다는 것을 명시하여 코드만 보는 경우에도 아이디를 불러오는구나 확인할 수 있도록 수정

```go
query := "SELECT User_id FROM userinfo WHERE User_id = ?"
```

-----

# 6. C_UserInfo와 R_UserInfo의 return 포멧 통일


**R_UserInfo**   
```go
func R_UserInfo(user User, db *sql.DB) ([]User, error)
```
**C_UserInfo**   
```go
func C_UserInfo(user User, db *sql.DB) error
```

## 문제점
insert 후 생성한 데이터 id를 반환값으로 반환하는 경우도 존재하는데 C_UserInfo와 R_UserInfo의 리턴은 다른 상황

## 생각
C_UserInfo와 R_UserInfo의 리턴이 다른 것이 큰 문제라고 생각은 하지 않았습니다.   
하지만 리턴 포멧을 통일한다면 1번 피드백의 생각과 동일하게 R은 어떤 값을 반환하는지, C는 어떤 값을 반환하는지 각각 기억하지 않기에 오류를 줄일 수 있을 것이라고 생각

## 조치
C_UserInfo과 R_UserInfo의 리턴 포멧을 User와 error로 통일

**R_UserInfo**   
```go
func R_UserInfo(user User, db *sql.DB) (User, error)
```
**C_UserInfo**   
```go
func C_UserInfo(user User, db *sql.DB) (User, error)
```

-----

# 7. rollback, commit없이 exec를 실행하는 문제

## 문제점
사실 많은 경험이 없어 얼마나 위험한지 rollback, commit을 활용하는 것이 얼마나 안전한 방법인지 정보가 없습니다.   
이러한 점을 모른다는 것이 가장 큰 문제라고 생각합니다.

## 생각
DB에 대한 오류가 생겼을 때 rollback을 하기 위하여 rollback을 활용하는 것이 안전할 것이라고 생각   
하지만 애매하게 판단하는 것 보다 모르는 내용은 공부하여 확실하게 알아두고 활용하는 것이 올바르다고 생각

## 조치
rollback과 commit에 대한 공부를 추가적으로 공부하여 확실하게 이해 후 적용 방법 고민하기로 결정


-----

# 결과

## ERD

### before
<img src="/assets/ERD 1.png">

### after
<img src="/assets/Pasted image 20231213172151.png">
