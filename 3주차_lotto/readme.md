## ****3주차****

## Contents

- [이번 주 핵심 사항](#이번-주-핵심-사항)
- [학습 내용](#학습-내용)
    - [정적 팩토리 메서드](#-정적-팩토리-메서드)
- [기능 목록](#기능-목록)


## 이번 주 핵심 사항

- 리드미
    
    해당 프로젝트가 어떤 프로젝트인지
    
    어떤 기능을 담고 있는지 기술하기
    
- 기능 목록
    
    기능 목록을 클래스와 함수 설명을 너무 상세하게 작성하지 않기
    
    (변경될 수 있기 때문)
    
    구현해야할 기능 목록을 정리하는데 집중
    
    정상적인 경우/ 예외 상황도 기능 목록에 정리
    
    게속 추가하면서 적기
    
- 하드 코딩 하지 않는다
    
    상수를 만들고 이름을 부여해 변수의 역할 의도를 드러내기
    
- 구현 순서도 코딩 컨벤션이다
    
    상수 또는 클래스 변수 → 인스턴스 변수 → 생성자 → 메소드
    
- 변수 이름에 자료형은 사용하지 않는다
    
    carNameList
    
    arrayString
    
- 한 함수가 한 가지 기능만 담당하게 한다
    
    중복된다면 함수 분리
    
    함수의 길이는 15라인으로 연습
    
- 테스트를 작성하는 이유에 대해 본인의 경험을 토대로 정리하기
    
    학습 테스트를 통해 JUnit 학습 
    
    [](https://techcourse-storage.s3.ap-northeast-2.amazonaws.com/9b82d8a360c548fcadd14c551dbcbe06)
    
- 처음부터 큰 단위의 테스트를 만들지 않는다
    
    문제를 작게 나누고 그 중 핵심 기능에 가까운 부분부터 작게 테스트를 만들어 나간다
    
## 과제 목표

- 함수 분리
    
    함수별로 테스트를 작성
    
- [추가]
    
    **1. 클래스(객체)를 분리하는 연습**
    
    **2. 도메인 로직에 대한 단위 테스트를 작성하는 연습**
    
    (작은 기능부터 테스트를 작성하는 연습을 시작해 보는 것입니다.)    


## ****학습 내용****

이번 과제를 통해 하나의 메소드에 하나의 기능 구현과 클래스 분리를 중점적으로 연습 해보겠습니다.

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

