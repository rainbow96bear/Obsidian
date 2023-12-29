# 목차
1. fmt 보다 strconv 선호
2. import 그룹 정리/배치
3. 구조체 초기화
4. 패키지 이름
5. 디렉터리
6. 참고 자료

-----

# fmt 보다 strconv 선호
프리미티브(primitives)를 문자열로 변환할 때 strconv가 fmt보다 빠르다.
```go
num := 3

// bad
strNum1 := fmt.Sprint(num)

// good
strNum2 := strconv.Itoa(num)
```

-----

# import 그룹 정리/배치
표준 라이브러리와 그 외에 모든 것은 empty line로 구분한다.
```go
import (
	"fmt"
	"os"

	"go.uber.org/atomic"
)
```

-----

# 구조체 초기화
구조체를 초기화 할 때는 거의 대부분 필드 명을 지정해야 한다.
```go
// bad
k := User{"John", "Doe", true}

// good
k := User{
    FirstName: "John",
    LastName: "Doe",
    Admin: true,
}
```

-----

# 패키지 이름
- 모두 소문자를 사용하고 대문자와 언더스코어는 사용하지 말 것
- 복수형 사용 금지
- 파일 이름의 경우 언더스코어를 사용(스네이크 표기법)

-----

# 디렉터리
## /cmd
메인 애플리케이션을 담는 디렉터리

## /internal
외부에서 사용하지 않을 라이브러리를 담는 디렉터리로 프로젝트 트리의 모든 레벨에서 하나 이상의 internal 디렉터리를 가질 수 있습니다.   
[internal 패키지 참고 자료](https://jacking75.github.io/go-0515/)

## /pkg
외부에서 사용되어도 괜찮은 라이브러리를 담는 디렉터리로 pkg에 있는 내용은 어디서든 import하여 사용 가능

## /assets
레포지토리와 함께 사용될 이미지, 로고 등을 담는 디렉터리

-----

# 참고 자료
- https://go.dev/blog/package-names
- https://github.com/TangoEnSkai/uber-go-style-guide-kr
- https://github.com/golang-standards/project-layout/blob/master/README_ko.md
- https://jacking75.github.io/go-0515/