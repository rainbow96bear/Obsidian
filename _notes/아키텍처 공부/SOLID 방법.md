# 목차
1. Single Responsibility Principle (SRP)
2. Open Closed Principle (OCP)
3. Liskov Substitution Principle (LSP)
4. Interface Segregation Principle (ISP)
5. Dependency Inversion Principle (DIP)

-----

# Single Responsibility Principle (SRP)

## SRP 특징
**한 클래스는 하나의 책임만 가져야 한다.**   
**나의 해석** : 하나의 기능만 가져야 한다는 것이 아닌 한 가지 분야를 담당하여야 한다.   

**예시**
```go
type Person struct {}

func (p *Person) Walk() {}
func (p *Person) Stop() {}
func (p *Person) Smile() {}
func (p *Person) Cry() {}
```
1. 사람을 표현하는 클래스(Golang의 예시 struct)가 있을 때 Walk와 Stop은 동작, Smile과 Cry는 감정을 담당합니다.   
2. Person의 경우 코드 수정이 동작 혹은 감정이 수정되어야 하는 경우 Person을 수정합니다.
3. SRP를 적용한다면 Person은 동작과 감정이라는 클래스(Golang은 struct)를 가지고 있고 동작이 수정되어야 하면 동작 클래스를, 감정이 수정되어야 하면 감정 클래스를 수정합니다.

```go
type Act struct{}

func (a *Act) Walk() {}
func (a *Act) Stop() {}

type Emotion struct{}

func (e *Emotion) Smile() {}
func (e *Emotion) Cry() {}

// 구조체 내장
type Person struct {
	Act
	Emotion
}
```
### 참고 자료
- [https://dding9code.tistory.com/32](https://dding9code.tistory.com/32)

-----

# Open Closed Principle (OCP)

## OCP 특징
**확장에 대해서는 개방되어야 하지만 변경에 대하여 폐쇄 되어야 한다.**   
**나의 해석** : 추가적인 기능을 구현할 때 기존 코드를 수정하지 않는 방식    

**예시**
```go
type Animal interface{
	Speak()
}

type Dog struct{}
func (d *Dog) Speak() {
	fmt.Println("왈왈")
}

type Cat struct{}
func (c *Cat) Speak(){
	fmt.Println("야옹")
}

func AnimalSpeak(a Animal){
	a.Speak()
}

func main(){
	dog := &Dog{}
	cat := &Cat{}

	AnimalSpeak(dog)
	AnimalSpeak(cat)
}
```

1. Animal에 Speak이란 함수를 구현하여 각각의 동물에 맞는 울음을 지정하는 방식이 아닌 각 동물에 해당하는 울음을 지정하고 interface를 통하여 실행
2. 새로운 동물이 추가될 때 기존의 코드가 수정되는 것이 아닌 새로운 동물에 대한 내용을 작성

### 참고 자료
- [https://dublin-java.tistory.com/48](https://dublin-java.tistory.com/48)
- [https://www.youtube.com/watch?v=EmnIdUvTRfk](https://www.youtube.com/watch?v=EmnIdUvTRfk)
- [https://piatoss3612.tistory.com/m/46](https://piatoss3612.tistory.com/m/46)

-----

# Liskov Substitution Principle (LSP)

## LSP 특징
**B가 A의 자식 타입이면 부모 타입인 A 객체는 자식 타입인 B로 치환해도 작동에 문제가 없어야 한다.**    
**나의 해석** : 작은 통의 내용을 큰 통에 담을 수 있다.   
추상적일수록 작은 것 -> 구체적인 것은 추상적인 내용을 모두 포함하고 있으니 문제가 없다.

**예시**
```go
type Dog struct{}

func (d *Dog) Speak() {
	fmt.Println("왈왈")
}

type Puddle Dog

func (p *Puddle) Speak(){
	fmt.Println("으르렁")
}

func (p *Puddle) Sleep(){
	fmt.Println("푸들이 잔다.")
}

func main() {
	dog := &Dog{}
	// dog := &Puddle{}
	dog.Speak()
	// if
	// puddle := &Puddle{}
	// puddle.Sleep()
	// if
	// if 사이의 코드에서 &Puddle{}를 &Dog{}로 변경 시 오류
}
```

### 참고 자료
- [https://pizzasheepsdev.tistory.com/9](https://pizzasheepsdev.tistory.com/9)

-----

# Interface SegreGation Principle (ISP)

## ISP 특징
**클라이언트가 자신이 이용하지 않는 메서드에 의존하지 않아야 한다.**   
**나의 해석** : SRP의 인터페이스 버전  

**예시**      
- 인터페이스를 기반으로 구현하는 경우 인터페이스가 여러 기능을 포함 ex) 걷기, 헤엄, 날기
- 인터페이스를 통하여 강아지 구현, 물고기 구현, 비둘기 구현
	- 강아지는 날기 불가능
	- 물고기는 걷기, 날기 불가능
	- 비둘기는 헤엄 불가능
- 구현 시 불필요한 내용을 포함하게 됨
- SRP처럼  각각의 책임을 단일 책임으로 활용

-----

# Dependency Inversion Principle (DIP)

## DIP 특징
**추상화에 의존해야지, 구체화에 의존하면 안된다.**   
**나의 해석** : 인터페이스를 활용한 작업 진행

**예시**

- main.go
```go
package main

import (
	"golang_practice/DIP_practice/Developer"
	IPerson "golang_practice/DIP_practice/I_Person"
	"golang_practice/DIP_practice/Singer"
)

func main() {
	developer := &Developer.Developer{}
	singer := &Singer.Singer{}

	// Worker 인터페이스를 활용하여 Work를 실행
	IPerson.Work(developer)
	IPerson.Work(singer)
}
```

- singer.go
```go
package Singer

import "fmt"

type Singer struct{}

func (s *Singer) Work() {
	s.Singing()
}

func (s *Singer) Singing() {
	fmt.Println("노래를 부릅니다.")
}
```
- developer.go
```go
package Developer

import "fmt"

type Developer struct{}

func (d *Developer) Work() {
	d.Programming()
}

func (d *Developer) Programming() {
	fmt.Println("개발을 합니다.")
}
```

- IPerson.go
```go
package IPerson

type Person interface {
	Work()
}

func Working(p Person) {
	p.Work()
}
```

**의존성**   
![[Pasted image 20231225004731.png]]


참고 자료   
- [https://simplear.tistory.com/24](https://simplear.tistory.com/24)
- [https://www.youtube.com/watch?v=nOHdunGzeRc&t=699s](https://www.youtube.com/watch?v=nOHdunGzeRc&t=699s)