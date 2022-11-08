## ****2주차****

## Contents

- [학습 내용](#학습-내용)
    - [빌더 패턴](#-builder-패턴)
    - [SOLID](#solid)
    - [TDD](#tdd)
- [기능 목록](#기능-목록)

## ****학습 내용****

이번 과제를 통해 클린 코딩과 TDD의 방식을 지향해 보고자 합니다

## **📖 Builder 패턴**

> 객체를 잘 만들 수 있게 해주는 도구

일반적 정의:

복잡한 객체를 생성하는 방법을 정의하는 클래스와

표현하는 방법을 정의하는 클래스를 별도로 분리하여,

서로 다른 표현이라도 이를 생성할 수 있는 동일한 절차를 제공하는 패턴

Setter대신 각각의 필드를 생성하는 메소드를 작성해 안전하게 사용하는 방법

Getter, Setter는 데이터를 보호하기 위함이지만,

무분별한 Setter는 데이터 무결성을 헤칠 수 있다

이를 해결하기 위해, 객체를 생성하는 생성자와, 이를 표현하는 메소드를 분리하여 사용하는 Builder 패턴을 이용해서 좀 더 직관적인 코드 생성이 가능하다

기존 객체 만드는 2가지 방법

```java
// 1. Setter 메서드를 사용하는 방법 

public class User {
	private String email;
	
	public void setEmail(String email) {
		this.email = email;
	}
}

User user = new User();
user.setEmail("test@email.com");

// 2. 생성자를 사용하는 방법

public class User {
	private String email;
	
	public User(String email) {
		this.email = email;
	}
}
```

Setter의 문제점

1. 일관성
    - 일관성
        
        모든 인스턴스 변수마다 Setter가 실행 되어야만 객체가 완성된다
        
        객체가 완전히 생성되기 전까지는 일관성이 무너진 상태에 놓였다고 한다
        
        일관성이 무너지더라도 실행에는 문제가 없기에
        
        컴파일 오류로 잡을 수 없다
        
    - 자바빈 규약에 따르면, Getter, Setter 메서드의 접근자는 public으로 선언되어야 한다
        
        → 언제, 어디든 객체의 값에 접근과 변경이 가능하다는 뜻이다
        
        → 객체 정보의 일관성을 지키기 힘들다
        
    - 일관성을 지키기 위해 인스턴스 변수를 final로 지정해서 객체를 만들었을 경우
        
        → Setter 개념과 충돌하게 되면서 컴파일 오류가 발생한다
        
        → 즉, Setter을 통해 불변객체를 만들 수 없다
        
2. 의도를 파악하기 힘듦
    - 값을 초기 설정하기 위한 것인지, 변경하기 위한 것인지 헷갈린다
        
        → 이를 메서드로 따로 작성하면 변경이 불필요한 필드의 변경을 막을 수 있다
        
        → User클래스를 사용하는 입장에서도 메서드의 의미를 명확하게 파악 가능하다
        

### 결론 : Setter 메서드 지양

생성자의 장점

1. 일관성
    
    ```java
    User user = new User("test@email.com, "1234")
    ```
    
    하나의 메서드를 통해 객체 생성과 초기화로 완성된 객체 반환이 가능
    
    → 일관성을 지킬 수 있다
    

문제점

1. 클래스의 매개변수가 많아질 경우
    
    → 필요하지 않은 값들을 굳이 null 값을 넣어가면서 써줘야 한다
    
    → 변수를 어느 위치에 세팅을 해야하는지 알기 어렵다
    
    → 경우의 수에 따라 생성자를 분리해서 여러개 만들면
    
    ```java
    public User(String wall, String roof) {
    	this.wall = wall;
    	this.roof = roof;
    }
    
    public User(String wall, String door) {
    	this.wall = wall;
    	this.roof = door;
    }
    ```
    
    오버로딩 기본원칙에 어긋나 생성이 불가하다
    

### 결론: 생성자에 매개변수가 많다면 빌더를 고려하라

**빌더클래스**

```java
public class User {
	_ User 필드, 생성자

	// Static inner Builder class 생성
	static public class Builder {
	
		// 세팅해줄 필드를 생성
		private String email;
		private String name;

		// 각각 필드의 값을 설정하는 메서드를 생성
		public Builder email(String email) {
			this.email = email;
			return this;
		}
		public Builder name(String name) {
			this.name = name;
			return this;
		}
		// -> 값 설정 후 자기자신(Bulider 객체)을 반환해야한다

		// User 객체를 반환하는 메서드를 생성
		public User build() {
			return new Uwer(email. name);
		}
}

빌더 클래스 사용

String email = "test@email.com"
String name = "ejachoi"

User user = new User.Builder()
									.email(email);
									.email(name);
									.build();
```

빌더 클래스의 장점

1. 가독성을 높여주고, 어디에 어떤 값을 세팅해야 하는지가 명확하다
2. 필요한 값만 설정하면, 나머지 값은 null로 설정된다
3. 하나의 메서드를 사용하는 것처럼 사용 가능하고, 마지막에 build() 메서드까지 호출 해야지만 User 객체로써 활용할 수 있으므로 일관성이 있다

빌더 클래스의 단점

1. 클래스 작성으로 인해 코드가 길어진다
    
    → 위와같이 User 클래스가 3개밖에 없을 경우 Builder를 사용하는게 맞나? 고민할 필요가 있다
    

정해진 틀에 맞게 구현하기보다 상황에 맞게 빌더를 유연하게 활용하자

1. 빌더를 사용하더라도 필수 값들은 받은 후에 나머지 값에 세팅을 하고 싶다면?
    
    ```java
    String email = "test@email.com";
    String password = "1234";
    String name = "ejachoi";
    
    User user = new User.Builder(email, password)
    										.name(name)
    										.build();
    ```
    
2. User 객체에 name만 추가해서 새롭게 생성할 수 있도록 하고 싶다면?
    
    ```java
    // 회원조회
    User user = userRepository.findById(1L);
    
    User updateUser = new User.builder(user)
    												.name(name)
    												.build();
    ```
    

Lombok - @Builder

> 롬복에서 지원하는 @builder 어노테이션을 사용해 간단히 사용할 수 있다
> 

```java
/*
public class User {
	static public class Builder {
	
		private String email;
		private String name;

		public Builder email(String email) {
			this.email = email;
			return this;
		}
		public Builder name(String name) {
			this.name = name;
			return this;
		}
		public User build() {
			return new Uwer(email. name);
		}
}
*/
@Builder //-> 모든 필드를 빌더 메서드로 사용이 가능 
public class User {
	private String email;
	private String name;

	public User(String email. String name) {
		this.email = email;
		this.name = name;
	}
}

User user = User.builder()
							.email(email)
							.name(name)
							.build();
```

특정 생성자 위에 @Builder 어노테이션을 적용해서 부분적으로도 사용이 가능하다

QnA

매개변수가 많다고 생각하는 기준이 어떻게 되는가?

→ 개인차… 7개 정도로 생각… 활용도의 관점으로 보자

두가지의 빌드패턴이 있는걸로 아는데 차이가 뭔가?

→ 이팩티브자바 빌드패턴 == GOF 디자인 패턴에 대한 빌드패턴

<div align = "right">
	<b><a href = "#Contents">↥ top</a></b>
</div>

## **📖 SOLID**

> **객체지향 프로그래밍 - 설계 5대 원칙** 

### S: 단일 책임 원칙

> 하나의 클래스는 하나의 책임만 가진다
> 

책임 → 기능

### O: 개방 폐쇄 원칙

> 기능을 추가할 때는 기존의 코드를 변경하지 않고도 추가할 수 있어야 한다
> 

animal 상위 객체를 만들고 강아지에게 상속해 각각의 울음 소리를 하위 클래스에서 구현한다면

 강아지.울기() 소.울기()를 통해 각각 구현이 가능

### L: 리스코프 치환 원칙

> 상위 타입의 객체를 사용하다가 하위 타입의 객체로 사용해도 정상작동 되어야 한다
> 

### I: 인터페이스 분리 원칙

> 하나의 일반적인 인터페이스를 어떤 클래스가 인터페이스를 구현하고 있을 때 너무 큰 범위의 인터페이스를 사용하지 않고 작고 구체적인 것들로 나눠서 사용해야한다.
> 

고양이, 개가 있을 때 고양이는 걷는 기능, 개는 걷는 기능, 짖는 기능이 필요할 때 

걷는 기능과 짖는 기능이 담긴 인터페이스를 상속받게 된다면 

고양이는 불필요한 기능까지 구현해야하는 문제가 발생

### D: 의존 역전 원칙

> 의존(다른걸 가져와서 쓸때)할 때는 좀 더 일반적이고 추상적인 것에 의존해야한다
> 

토끼 클래스 안에는 먹이라는 내부 필드가 있다. 

내부 필드는 Carrot 데이터 타입을 받는다. 

근데 Apple 먹이로 바꿔야한다면 기존의 데이터 타입이 다르므로 수정 소요가 발생한다. 

그런데 Carrot과 Apple은 vagetable의 상위 개념에 상속받은 존재라면 먹이 타입을 상위 개념으로 의존시켜라.

<div align = "right">
	<b><a href = "#Contents">↥ top</a></b>
</div>

## **📖 TDD**

TDD란 Test Driven Development의 약자로 ‘테스트 주도 개발’이라고 한다

테스트케이스를 작성 한 후 실제 코드를 개발하여 리펙토링하는 절차를 따른다

작은 단위부터 테스트를 만들어가며 코드를 개발한다

TDD에는 최소한의 `정적 모델링`이 필요하다

_모델링을 할 때 요구사항, 기능 분석등을 통하여 명사, 동사를 뽑아 클래스와 메소드로 추출하는 것이 정적 모델링이라 한다_

이번 과제에서 내가 시도해볼 TDD 프레임

1. JUnit 잘 동작하나

    ```java
    import org.junit.Test;

    public class GameTest {
    
        @Test
        public void nothing(){
        }
    }
    ```

2. 무엇을 테스트할까? 가장 쉬운 것부터

    class 만들기 → 실패하기 → 성공을 위해 구현하기 → 리펙토링

    리펙토링 중점 사항: 중복된 코드, 사용하지 않는 코드 제거

    가장 먼저 게임이 만들어지는지 테스트

    ```java
    import org.junit.Test;

    public class GameTest {
        @Test
        public void isGameCreateAvailable(){
            Game game = new Game();
        }
    }
    ```

    Game class가 없으니까 당연히 실패

3. 실패한 테스트를 성공하기 위한 최소한의 코드 작성

    ```java
    public class Game {
    }
    ```

    또는,
    ```java
    public class GameResultCalculatorTest {

        @Test
        public void isCounted3StrikesWhen123And123(){
            assertEquals(calculator.getStrikesCnt("123", "123"), 3);
        }
    }
    ```

    라는 test의 성공을 위해

    ```java
    public class GameResultCalculator {
    //이전 단계 동일

        public int getStrikesCnt(String s, String s1) {
            return 3;
        }
    }
    ```

    으로 최소한의 코드 작성

    일반화가 어려운 경우 가장 작은 단위부터 테스트를 진행해

    하나씩 늘려가며 일반화해 나가기


### 내가 느낀 TDD의 장, 단점

장점

- 모든 기능이 구현된 후 조합해가며 코드를 완성했을 때 에러나 버그가 없었다

    -> 디버깅 시간의 단축

단점

- 테스트는 말 그대로 테스트일 뿐 실제 코드가 더 중요한 상황인데도 불구하고 테스트 원칙 때문에 쉽게 넘어가지 못하는 경우가 발생했다

  -> 생산성이 저하된다

<div align = "right">
	<b><a href = "#Contents">↥ top</a></b>
</div>


## ****기능 목록****

게임 생성 기능 :white_check_mark:

- [x] 게임을 생성한다

- [x] 게임 종료 후, 재시작할지를 결정 하기위한 값을 받는다

숫자 비교 기능 :white_check_mark:

- [x] 두개의 문자열을 비교한다
- [x] 스트라이크, 볼, 낫싱 결과를 판단한다

상대방 숫자열 생성 기능 :white_check_mark:

- [x] Randoms를 활용한 숫자열 생성

유효성 검사 기능 :white_check_mark:

- [x] 사용자 숫자를 입력받는다

- [x] 입력에 대해 유효성 검사를 한다

  1. 게임 생성 기능의 **[예외처리]**

     - [x] 1, 2의 값이 아닌 경우

  2. 사용자 입력 값에 대한 **[예외처리]**
     - [x] 숫자가 아닌 경우

     - [x] 숫자에 0이 들어간 경우

     - [x] 3자리의 숫자가 아닌 경우

     - [x] 중복된 숫자가 아닌 경우

<div align = "right">
	<b><a href = "#Contents">↥ top</a></b>
</div>

