## ****3주차****

## Contents

- [****3주차****](#3주차)
- [Contents](#contents)
- [과제 목표](#과제-목표)
- [****학습 내용****](#학습-내용)
- [**📖 MVC**](#-mvc)
  - [모델](#모델)
  - [뷰](#뷰)
  - [컨트롤러](#컨트롤러)
  - [느낀점](#느낀점)
- [**📖 정적 팩토리 메서드**](#-정적-팩토리-메서드)
- [**📖 정규식**](#-정규식)
- [****기능 목록****](#기능-목록)
  - [🎯 프로젝트 개요](#-프로젝트-개요)
  - [🚀 기능목록](#-기능목록)
- [과제를 이해한 후 느낀점](#과제를-이해한-후-느낀점)

 
## 과제 목표

- 함수 분리
    
    함수별로 테스트를 작성
    
- [추가]
    
    **1. 클래스(객체)를 분리하는 연습**
    
    **2. 도메인 로직에 대한 단위 테스트를 작성하는 연습**
    
    (작은 기능부터 테스트를 작성하는 연습을 시작해 보는 것입니다.)    


## ****학습 내용****

이번 과제를 통해 하나의 메소드에 하나의 기능 구현과 클래스 분리를 중점적으로 연습 해보겠습니다.

## **📖 MVC**

이번에 처음 MVC모델을 알게되어 lotto 과제 설계에 적용해보았다

MVC 패턴은어플리케이션을 세가지 역할로 구분한 개발 방법론을 말한다

사용자가 입력을 담당하는 View를 통해 요청을 보내면 해당 요청을 컨트롤러가 받고

컨트롤러는 모델을 통해 데이터를 가져오고

해당 데이터를 바탕으로 출력을 담당하는 뷰를 제어해서 사용자에게 전달한다

MVC 패턴을 사용하면 모델과 뷰가 다른 컴포넌트들에 종속되지 않아

변경에 유리하다는 장점을 가진다

컴포넌트는 모델 뷰 컨트롤러가 있다

### 모델

어플리케이션에 무엇을 할 것인지 정의한다

내부 비즈니스 로직을 처리하기 위한 역할을 한다

데이터 저장소와 연동해 사용자가 입력한 데이터나 사용자에게 출력할 데이터를 다룬다

추가, 변경, 삭제와 같은 데이터 변경을 하나의 작업으로 묶은 트랜잭션을 다루는 일도 한다

모델은 다른 컴포넌트들에 대해 알지 못한다

자기 자신이 무엇을 수행하는지만 알고 있다

### 뷰

최종 사용자에게 무엇을 화면(UI)로 보여준다

즉 모델이 처리한 데이터나 그 작업 결과를 가지고 사용자에게 출력할 화면을 만든다

뷰 역시 다른 컴포넌트들에 알지 못한다

자기 자신이 무엇을 수행하는지만 알고 있다

### 컨트롤러

모델과 뷰 사이에 있는 컴포넌트이다

모델이 데이터를 어떻게 처리할 지 알려주는 역할을 한다

클라이언트의 요청을 받으면 해당 요청에 대한 업무를 수행하는 모델을 호출한다

클라이언트가 보낸 데이터가 있다면, 모델을 호출할 때 전달하기 쉽게 적절히 가공한다

예를들어 내가 이해한 로또를 사기위한 금액을 받아 Money 객체에 저장하는 과정은 다음과 같다

1. 뷰를 통해 String 받기
2. 모델로 전달하기 전 가공하기
   1. NULL인가 유효성 검사(utils)
   2. 숫자인가 유효성 검사(utils)
3. 모델로 전달
   1. 생성자에서 1000원 단위가 맞는지 유효성 검사

모델이 업무 수행을 완료하면 그 결과를 가지고 화면을 생성하도록 뷰에 전달한다

즉 클라이언트의 요청에 대해 모델과 뷰를 결정하여 전달하는 일정의 조정자로서의 일을 한다

컨트롤러는 다른 컴포넌트들에 대해 알고 있다 자기 자신 외에 모델과 뷰가 무엇을 수행하는지 안다

inputView를 통해 사용자로부터 입력을 받고

Model을 통해 내부 비즈니스 로직을 처리하고

outputView를 통해 사용자에게 화면을 출력한다

### 느낀점

프로그램 실행 환경이 바뀌었을때 모델은 그대로 사용하고 컨트롤러와 뷰만 새로 구현하면 된다는 것을 깨달았다

모델은 내부 비즈니스 로직을 가지기 때문에 보통 개발할 때 구현에 가장 오랜 시간이 걸린다

모델을 그대로 활용하니까 코드를 크게 변경하지 않아도 금세 새로운 환경에서 작동하는 어플리케이션을 만들 수 있을거라 생각한다

모델과 뷰가 다른 컴포넌트들에 독립적이게 만드는 것이 생각보다 어렵다는 것을 알게 되었다


<div align = "right">
	<b><a href = "#Contents">↥ top</a></b>
</div>

## **📖 정적 팩토리 메서드**

**이름을 가질 수 있다**

객체는 생성 목적과 과정에 따라 생성자를 구별해서 사용할 필요가 있다.

new 라는 키워드를 통해 객체를 생성하는 생성자는 내부 구조를 잘 알고 있어야 목적에 맞게 객체를 생성할 수 있다.

하지만 정적 팩토리 메서드를 사용하면 메서드 이름에 객체의 생성 목적을 담아 낼 수 있다.

```java
public class LottoFactory() {
  private static final int LOTTO_SIZE = 6;

  private static List<LottoNumber> allLottoNumbers = ...; // 1~45까지의 로또 넘버

  public static Lotto createAutoLotto() {
    Collections.shuffle(allLottoNumbers);
    return new Lotto(allLottoNumbers.stream()
            .limit(LOTTO_SIZE)
            .collect(Collectors.toList()));
  }

  public static Lotto createManualLotto(List<LottoNumber> lottoNumbers) {
    return new Lotto(lottoNumbers);
  }
  ...
}
```

메서드의 이름만 보아도 로또 객체를 자동으로 생성하는지, 아니면 수동으로 생성하는지 단번에 이해할 수 있을 것이다.

이처럼 정적 팩토리 메서드를 사용하면 해당 생성의 목적을 이름에 표현할 수 있어 가독성이 좋아지는 효과가 있다.

**호출할 때마다 새로운 객체를 생성할 필요가 없다.**

enum과 같이 자주 사용되는 요소의 개수가 정해져있다면 해당 개수만큼 미리 생성해놓고 조회(캐싱)할 수 있는 구조로 만들수 있다. 

**정적 팩터리 메서드**와 **캐싱구조**를 함께 사용하면 매번 새로운 객체를 생성할 필요가 없어진다.

```java
public class LottoNumber {
  private static final int MIN_LOTTO_NUMBER = 1;
  private static final int MAX_LOTTO_NUMBER = 45;

  private static Map<Integer, LottoNumber> lottoNumberCache = new HashMap<>();

  static {
    IntStream.range(MIN_LOTTO_NUMBER, MAX_LOTTO_NUMBER)
                .forEach(i -> lottoNumberCache.put(i, new LottoNumber(i)));
  }

  private int number;

  private LottoNumber(int number) {
    this.number = number;
  }

  public LottoNumber of(int number) {  // LottoNumber를 반환하는 정적 팩토리 메서드
    return lottoNumberCache.get(number);
  }

  ...
}
```

미리 생성된 로또 번호 객체의 캐싱을 통해서 새로운 객체 생성의 부담을 덜 수 있다는 장점도 있지만,

생성자의 접근 제한자를 `private`으로 설정함으로써 **객체 생성을 정적 팩토리 메서드로만 가능하도록 제한**할 수 있다는 것이다. 이를 통해 정해진 범위를 벗어나는 로또 번호의 생성을 막을 수 있다는 장점을 확보할 수 있다

****하위 자료형 객체를 반환할 수 있다.****

하위 자료형 객체를 반환하는 정적 팩토리 메서드의 특징은 상속을 사용할 때 확인할 수 있다. 

이는 생성자의 역할을 하는 정적 팩토리 메서드가 반환값을 가지고 있기 때문에 가능한 특징이다.

시험 점수에 따라 결정되는하위 등급 타입을 반환하는 정적 팩토리 메서드를 만들면, 

다음과 같이 분기처리를 통해 하위 타입의 객체를 반환할 수 있다.

```java
public class Level {
  ...
  public static Level of(int score) {
    if (score < 50) {
      return new Basic();
    } else if (score < 80) {
      return new Intermediate();
    } else {
      return new Advanced();
    }
  }
  ...
}
```

## **📖 정규식**

정규식 표현은 특정한 규칙을 가진 문자열의 집합을 표현하는데 사용되는 언어를 말한다

자바 utils.regex에서의 pattern이나 matches를 주로 사용한다

특정 문자열이 주어진 정규식에 매칭되는지 테스트가 가능하다


- replaceAll()

	문자열을 대체하는 메소드로

	replace와 두개가 있음

	replaceAll()은 정규표현식 사용이 가능

	String regex = "[0-9]";

	input = input.replaceAll(regex,"");
	
	숫자를 “”으로 지우고

	!input.matches(“[1-9]+[0-9]*”)를 확인

http://yoonbumtae.com/?p=1865


****객체 생성을 캡슐화할 수 있다.****

여러 번의 객체 생성이 필요한 경우라면 생성자보다는 정적 팩토리 메서드를 사용해보자.

<div align = "right">
	<b><a href = "#Contents">↥ top</a></b>
</div>

## ****기능 목록****

### 🎯 프로젝트 개요

로또 게임 기능을 구현합니다. 

로또 한 장의 가격은 1,000원 입니다.

숫자 1부터 45 범위 내의 숫자 중, 6개의 숫자를 자동으로 뽑습니다.

당첨 번호 추첨 시 중복되지 않는 숫자 6개와 보너스 번호 1개를 뽑습니다.

당첨 내역 및 수익률을 출력하고 로또 게임을 종료합니다.

### 🚀 기능목록

- [x] 로또 구입 금액을 입력받는 기능

    - [x] 구매 가능한 로또 개수 구하는 기능
    - [x] 공백이 있다면 제거
    - [x] (e) 공백인 경우 예외처리
    - [x] (e) 정수 입력이 아니면 예외처리
    - [x] (e) 음수이면 예외처리
    - [x] (e) 1000원 단위 외의 금액은 예외처리

    <br/>

- [x] 구매한 로또 개수 출력하는 기능

    <br/>

- [x] 로또 목록 기능
    - [x] 로또 티켓을 랜덤으로 생성하는 기능

    - [x] 로또 숫자 정렬하는 기능

    - [x] 생성된 티켓 목록을 출력하는 기능

    <br/>

- [x] 당첨 번호 입력받는 기능

    - [x] 공백 제거
    - [x] (e) 숫자가 아니면 예외처리
    - [x] (e) 숫자가 6개가 아니면 예외처리
    - [x] (e) 숫자가 1 ~ 45 범위가 아니면 예외처리
    - [x] (e) 입력 구분자가 , 가 아니면 예외처리
    - [x] (e) 중복된 숫자가 올 경우 예외처리

    <br/>

- [x] 보너스 번호 입력받는 기능

    - [x] 공백 제거
    - [x] (e) 숫자가 아니면 예외처리
    - [x] (e) 숫자는 1 ~ 45 범위가 아니면 예외처리
    - [x] (e) 당첨 번호와 중복되면 예외처리

    <br/>

- [x] 결과를 계산하는 기능

    - [x] 6등 확인 기능
    - [x] 5등 확인 기능
    - [x] 4등 확인 기능
    - [x] 3등 확인 기능
    - [x] 2등 확인 기능
    - [x] 1등 확인 기능 

    <br/>

- [x] 추첨 결과를 출력하는 기능

    - [x] 수익률 출력하는 기능



<div align = "right">
	<b><a href = "#Contents">↥ top</a></b>
</div>

## 과제를 이해한 후 느낀점

controller에게 너무 과중한 책임이 있다

input값을 받아 작동하는 부분과

그렇지 않는 부분을 나눠서 설계를 할수는 없을까

3주차 과제 lotto를 마치고 피드백을 하는 과정에서 많은 아쉬움이 느껴졌다

더 나은 4주차 과제가 되기위해 아쉬운 점을 먼저 고민해보고 과제를 진행하기로 했다.

이전과제 코드리뷰 - 박우빈 님의 코드를 리뷰하며 느낀점을 필두로 작성

```java
public void run() {
        try {
         
				   LottoPurchaseAmount lottoPurchaseAmount = inputLottoPurchaseAmount();

				}
private LottoPurchaseAmount inputLottoPurchaseAmount() {

        String lottoPurchaseAmountInput = inputView.inputLottoPurchaseAmount();

        return BasicLottoInputParser.parseLottoPurchaseAmount(lottoPurchaseAmountInput);
    }
```

컨트롤러의 run()에서 LottoPurchaseAmount의 값을 받아 가공한 후 

모델에 값을 전달하여 LottoPurchaseAmount 객체를 생성하는 과정을 보자

BasicLottoInputParser은 유틸 패키지에 존재하고 널, 숫자를 확인한다

```java
public class BasicLottoInputParser {

    private BasicLottoInputParser() {
    }

    public static LottoPurchaseAmount parseLottoPurchaseAmount(final String input) {
        return parseWithCheckingEmpty(input, LottoPurchaseAmount::from);
    }
		
		private static <T> T parseWithCheckingEmpty(final String input, final IntFunction<T> creationFunction) {
        EmptyChecker.check(input);

        return parse(input, creationFunction);
    }

    private static <T> T parse(final String input, final IntFunction<T> creationFunction) {
        return Stream.of(input)
                .map(String::trim)
                .map(Integer::parseInt)
                .map(creationFunction::apply)
                .findFirst()
                .orElseThrow(IllegalArgumentException::new);
    }
}
```

parseLottoPurchaseAmount(lottoPurchaseAmountInput); 에서 먼저 Empty를 확인한다

```java
private static <T> T parseWithCheckingEmpty(final String input, final IntFunction<T> creationFunction) {
```

<T> ? 

제네릭에 대해 먼저 공부해보자

[코딩교육 티씨피스쿨](http://tcpschool.com/java/java_generic_concept)

## 제네릭(generic)

- 설명 보기
    
    데이터의 타입을 일반화한다는 것을 의미한다
    
    클래스나 메소드에서 사용할 내부 데이터 타입을 컴파일 시에 미리 지정하는 방법이다
    
    장점
    
    1. 클래스, 메소드 내부에서 사용되는 객체 타입 안정성을 높일 수 있다
    2. 반환값에 대한 타입 변환 및 타입 검사에 들어가는 노력을 줄일 수 있다
    
    제네릭이 없을때는 인수나 반환값으로 Object 타입을 사용했다
    
    이럴 경우 반환된 Object 객체를 다시 원하는 타입으로 변환하야한다
    
    제네릭을 통해 이와같은 번거로운 작업을 생략할 수 있다
    
    ## 제네릭의 생성
    
    ```java
    class MyArray<T> {
        T element;
        
    		void setElement(T element) { 
    			
    			this.element = element; 
    		}
        
    		T getElement() {
    	
    			return element; 
    		}
    }
    ```
    
    위의 T를 타입 변수라고 하며 임의의 참조현 타입을 의미한다
    
    어떤 문자를 사용해도 상관 없음은 물론, 쉼표로 구분하여 여러개의 타입 변수를 명시할 수 있다
    
    실제로 선언할 때에는 사용할 실제 타입을 명시해야한다
    
    ```java
    MyArray<Integer> myArr = new MyArray<Integer>();
    
    // 추정 가능할 때에는 생략이 가능
    MyArray<Integer> myArr = new MyArray<>(); // Java SE 7부터 가능함.
    ```
    
    자바 코드에서 선언되고 사용된 제네릭 타입은 컴파일 되면 자동으로 검사되어 타입 변환된다
    
    모든 제네릭 타입은 제거되는데, 제네릭을 사용하지 않는 코드와의 호환성 유지를 위해서이다
    
    ## 제네릭 타입 변수의 제한
    
    extends 키워드를 사용하면 타입 변수에 특정 타입만을 사용하도록 제한할 수 있다
    
    ```java
    class AnimalList<T extends LandAnimal> { ... }
    ```
    
    ## 제네릭 메소드
    
    메소드의 선언부에 타입 변수를 사용한 메소드를 의미한다
    
    ```java
    public static <T> void sort( ... ) { ... }
    ```
    
    ## 와일드카드의 사용
    
    와일드 카드란 이름에 제한을 두지 않음을 표현하는 데 사용하는 기호를 의미한다
    
    자바의 제네릭에서는 물음표(?) 기호를 사용ㅇ하여 이러한 와일드 카드를 사용할 수 있다
    
    ```java
    <?>           // 타입 변수에 모든 타입을 사용할 수 있음.
    <? extends T> // T 타입과 T 타입을 상속받는 자손 클래스 타입만을 사용할 수 있음.
    <? super T>   // T 타입과 T 타입이 상속받은 조상 클래스 타입만을 사용할 수 있음.
    ```
    

위에서 언급한 <T>는 제네릭 메서드를 의미하는 것  이었다

컴파일러에게 “T라는 클래스가 매개변수가 오면 Optional의 유형도 T야” 라고 알려주는 것

```java
private static <T> T parse(final String input, final IntFunction<T> creationFunction) {
        return Stream.of(input)
                .map(String::trim)
                .map(Integer::parseInt)
                .map(creationFunction::apply)
                .findFirst()
                .orElseThrow(IllegalArgumentException::new);
    }
```

(IntFunction<T> creationFunction) 은 무엇일까

[Java Lambda (2) 타입 추론과 함수형 인터페이스](https://futurecreator.github.io/2018/07/20/java-lambda-type-inference-functional-interface/)

## 기본형 함수형 인터페이스

- 설명 보기
    
    자바는 람다를 지원하기 우해서 타입 추론을 강화해야 했다
    
    이로인해 함수형 인터페이스가 등장한다
    
    함수형 인터페이스는 하나의 추상메소드로 이루어진 인터페이스를 말하는데
    
    함수의 시그니쳐가 정의되어 있기 때문에 컴파일러가 이 정보를 참고해 람다에서 생략된 정보들을 추론할 수 있다
    
    함수형 인터페이스는 단 하나의 메소드를 가질 수 있다
    
    ****@FunctionalInterface**** 로 표시가 가능하다
    
    ```java
    // 컴파일 OK
    public interface FunctionalInterfaceExample {
        
    }
    
    // 추상 메소드가 없으므로 컴파일 에러
    @FunctionalInterface
    public interface FunctionalInterfaceExample {
        
    }
    
    // 추상 메소드가 두 개 이상이면 컴파일 에러
    @FunctionalInterface
    public interface FunctionalInterfaceExample {
      void apply();
      void illigal(); // error
    }
    ```
    

함수형 인터페이스를 사용하는 이유는 다음과 같다

```java
		public static LottoPurchaseAmount parseLottoPurchaseAmount(final String input) {
        return parseWithCheckingEmpty(input, LottoPurchaseAmount::from);
    }

    public static SizeOfManualLotto parseSizeOfManualLotto(final String input) {
        return parseWithCheckingEmpty(input, SizeOfManualLotto::from);
    }

    public static LottoNumber parseLottoBonusBall(final String input) {
        return parseWithCheckingEmpty(input, LottoNumberPool::get);
    }

    private static <T> T parseWithCheckingEmpty(final String input, final IntFunction<T> creationFunction) {
        EmptyChecker.check(input);

        return parse(input, creationFunction);
    }
		private static <T> T parse(final String input, final IntFunction<T> creationFunction) {
        return Stream.of(input)
                .map(String::trim)
                .map(Integer::parseInt)
                .map(creationFunction::apply)
                .findFirst()
                .orElseThrow(IllegalArgumentException::new);
    }
}
```

문제에서 여러개의 인자를 받는데 그 중, 구매량, 수동로또의 사이즈, 로또번호는 숫자만을 받는다는 공통점이 있다.

이러한 점을 고려해 동일하게 parse 메서드를 사용할 수 있도록 구현했다

서로 같은 유효성 검사를 하지만 결과적으로 우리는 객체를 생성해야 하는데 그 객체가 서로 다르므로 생성자를 intfunction에 담는다

parse의 .map(creationFunction::apply)에서 객체를 생성하게되고 .findFirst()로 객체를 전달한다

이때 람다식을 사용하고 있다

## 람다

[Java Lambda (1) 기본](https://futurecreator.github.io/2018/07/19/java-lambda-basics/)

[자바의 정석 - 람다식(Lambda Expression)](https://ryan-han.com/post/java/java-lambda/)

- 설명 보기
    
    람다는 메서드를 하나의 식으로 표현한 것을 말한다
    
    메서드를 람다식으로 표현하면 메서드의 이름과 반환값이 없어지므로 람다식을 익명 함수라고도 한다
    
    람다식은 메서드의 매개변수로 전달될 수 있고,
    
    메서드의 결과로 반환될 수 있다
    
    즉, 메서드를 변수처럼 다루는 것이 가능하다
    
    익명 클래스와 헷갈릴 수 있는데, 익명 클래스는 인스턴스를 생성해야 하지만, 함수는 평가될 때마다 새로 생성되지 않는다
    
    함수를 위한 메모리 할당은 자바 힙의 permanent 영역에 한번 저장된다
    
    객체는 데이터와 밀접하게 연관해서 동작하지만, 함수는 데이터와 분리되어있다
    
    상태를 보존하지 않기 때문에 연산을 여러 번 적용해도 결과가 달라진다
    
    ## 람다식 작성하기
    
    메서드에서 이름과 반환타입을 제거한다
    
    매개변수 선언부와 몸통 사이에 → 를 추가한다
    
    ```java
    //기존
    반환타입 메서드이름 (매개변수 선언)  {
      ...
    }
    
    //람다식
    (매개변수 선언) ->  {
      ...
    }
    ```
    
    반환값이 있는 메서드는 return 대신 식으로 대신할 수 있다
    
    (연산 결과가 자동으로 반환값이 되고 ;를 생각)
    
    매개변수의 타입은 추론가능하면 생략이 가능하다
    
    두 매개변수 중 하나만 생략하는 것은 불가능하다
    
    매개변수가 하나뿐이면 괄호() 생략이 가능하다
    
    ```java
    //기존
    int max(int a, int b) {
      return a > b ? a : b;
    }
    
    //람다식
    (int a, int b) -> {
      return a > b ? a : b;
    }
    
    //return문 대신 expression 사용
    (int a, int b) -> a > b ? a: b
    
    //매개변수 타입 생략
    (a, b) -> a > b ? a : b
    
    //매개변수 1개일 경우 괄호 생략
    a -> a*a     //OK
    int a -> a*a //에러
    
    //본문 문장 1개일 경우 중괄호 생략
    (String name, int i) -> System.out.println(name+"="+i)
    ```
    
    ## 함수형 인터페이스
    
    람다식을 다루기 위한 인터페이스를 말한다
    
    람다식은 메서드와 동등한 것이 아니라 익명클래스의 객체와 동등하다
    
    ```java
    // 람다식
      (int a, int b) -> a > b ? a : b
    
    // 익명클래스의 객체
      new Object()  {
        int max(int a, int b) {
          return a > b ? a : b ;
        }
      }
    ```
    
    람다식으로 정의된 익명 객체의 메서드를 호출하려면 참조 변수가 필요하다
    
    이때, 참조 변수의 타입은 클래스 또는 인터페이스가 가능한데 람다식과 동등한 메서드가 정의되어 있는 것이어야 한다
    
    예를 들어
    
    ```java
    // 예를 들어 max() 메서드가 정의된 Myfunction 인터페이스 정의
      interface MyFunction  {
        public abstract int max(int a, int b);
    
    // MyFunction 인터페이스를 구현한 익명클래스 객체 생성
      MyFunction f = new MyFunction() {
        public int max (int a, int b);
          return a > b ? a : b;
        }
      }
      int big = f.max(5, 3);  //익명 객체의 메서드 호출
    
    // 위의 익명 객체를 람다식으로 대체
      MyFunction f = (int a, int b) -> a > b ? a : b;
      int big = f.max(5, 3);
    ```
    
    MyFunction 인터페이스를 구현한 익명 객체를 람다식으로 대체 가능한 이유는 
    
    람다식도 실제로는 익명 객체이고 
    
    MyFunction 인터페이스를 구현한 익명 객체의 메서드 max()와 람다식의 매개변수의 타입과 개수, 반환값이 일치하기 때문이다.
    
    단 함수형 인터페이스에는 오직 하나의 초상 메서드만 정의되어있다.
    
    @FunctionalInterface 를 붙이면 컴파일러가 함수형 인터페이스를 올바르게 정의하였는지 확인해준다
    
    ```java
    // 기존 인터페이스의 메서드 구현
      List<String> list = Arrays.asList("abc", "aaa", "bbb", "ccc");
      Collections.sort(list, new Comparator<String>() {
        public int compare(String s1, String s2)  {
          return s2.compareTo(s1);
        }
      });
    
    // 람다식으로 구현
      List<String> list = Arrays.asList("abc", "aaa", "bbb", "ccc");
      Collections.sort(list, (s1, s2) -> s2.compareTo(s1));
    ```
    
    ## ****java.util.function 패키지****
    
    - 수학에서 결과로 true 또는 false를 반환하는 함수를 Predicate 라고 한다.
    - 매개변수가 2개인 함수형 인터페이스는 이름 앞에 ‘Bi’가 붙는다.
    - Supplier는 매개변수는 없고 반환값만 존재하는데 메서드는 두 개의 값을 반환할 수 없으므로 BiSupplier가 없다.
    - 매개변수의 타입과 반환타입이 일치할 때는 Function 대신 UnaryOperator를 사용한다. (매개 변수 2개면 BinaryOperator)
    
    문법 요약
    
    ```java
    // 인자 -> 바디
    (int x, int y) -> { return x + y; }
    
    // 인자 타입 생략 - 컴파일러가 추론
    (x, y) -> { return x + y; }
    
    // return 및 중괄호 생략
    (x, y) -> x + y
    
    // 인자가 하나인 경우 인자 괄호 생략
    x-> x * 2
        
    // 인자가 없으면 빈 괄호로 표시
    () -> System.out.println("Hey there!")
    
    // 메소드 참조 Method reference
    // (value -> System.out.println(value)) 의 축약형
    System.out::println
    ```
    
    ## 메서드 참조
    
    람다식이 하나의 메서드만 호출하는 경우 메서드 참조를 통해 람다식을 간략히 할 수 있다
    
    클래스명 :: 메서드명 또는 참조변수 :: 메서드명
    
    ```java
    // 기존
    Function<String, Integer> f = (String s) -> Integer.parseInt(s);
    
    // 메서드 참조
    Funcation<String, Integer> f = Integer::parseInt;
    ```
    
    생성자를 호출하는 람다식도 메서드 참조로 변환이 가능하다
    
    ```java
    Supplier<MyClass> s = () -> new MyClass();  // 람다식
    Supplier<MyClass> s = MyClass::new; // 메서드 참조
    ```
    
    배열을 생성할 경우
    
    ```java
    Function<Integer, int[]> f = x -> new int[x]; // 람다식
    Function<Integer, int[]> f2 = int[]::new; // 메서드 참조
    ```
