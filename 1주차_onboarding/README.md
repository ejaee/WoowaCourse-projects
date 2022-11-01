## ****1주차****

## Contents

- [문제1](#-문제1)
- [문제2](#-문제2)
- [문제3](#-문제3)
- [문제4](#-문제4)
- [문제5](#-문제5)
- [문제6](#-문제1)
- [문제7](#-문제1)

### 📝 [문제1](https://github.com/ejaee/java-onboarding/blob/main/docs/PROBLEM1.md)

### ****기능 목록****

- 플레이어가 받은 두 페이지의 유효성을 확인하는 기능

    ☑️ [예외처리] 책의 1부터 400까지의 범위를 벗어나는지 검증하는 기능

    ☑️ [예외처리] 첫 번째 요소는 홀수, 두 번째 요소는 짝수인지 검증하는 기능

    ☑️ [예외처리] 두 요소가 연속된 자연수인지 검증하는 기능

    ☑️ [💥예외처리] 1이나 400을 포함하지 않았는지 검증하는 기능

    ☑️ [💥예외처리] 받은 페이지가 두 요소가 아닌지 검증하는 기능
    - 예외사항 시 return -1

 
- 받은 페이지 값을 활용해 최대값을 구하는 기능
  
    ☑️ 플레이어가 받은 두 페이지를 활용해 조건에 맞는 최대값을 구하는 기능
    
    ☑️ 페이지 각 자리 숫자의 합과 곱 중 더 큰 값을 구하는 기능

    ☑️ 왼쪽 페이지와 오른쪽 페이지 중 더 큰 값을 구하는 기능


- 각 플레이어의 최대값을 비교하는 기능

    ☑️ 각 플레이어의 숫자를 서로 비교하여 승부 결과를 반환하기
    - pobi가 이길 시 return 1
    - crong이 이길 시 return 2
    - 무승부 시 return 0
    - 예외사항 시 return -1

### ****학습 내용****

1. `List<integer> pages`

    java에는 컬렉션 프레임웍의 핵심 인터페이스가 존재한다

    ```
    컬렉션
    -> 여러 객체를 모아 놓은 것

    프레임웍
    -> 표준화, 정형화된 체계적인 프로그래밍 방식

    컬렉션 프레임웍
    -> 컬렉션(다수의 객체)를 다루기 위한 표준화된 프로그래밍 방식
    -> 객체(데이터)를 다룬다 
        : 저장, 검색, 삭제, 정렬...

    컬렉션 클래스
    -> 다수의 데이터를 저장할 수 있는 클래스
        :  Arraylist, HashSet, Vector...
    ```


    - List
    - Set
    - Map

- `List`

    배열의 정적 생성의 한계를 해결하기위해 만들어진 클래스로,

    메모리 허용 범위 내에서 게속 추가 할 수 있도록 만든 자료형 클래스이다

    ```java
    List<String> listA = new ArrayList<String>();
    List<String> listB = new LinkedList<String>();
    List<String> listC = new Vector<String>();
    List<String> listD = new Stack<String>();
    ```

    특징

    - 순서가 있다
    - 중복을 허용한다
    - 쓰임 : 대기자 명단

- `add()`

    List의 값을 추가하기 위한 메서드이다

    ```java
    List<String> listA = new ArrayList<String>();

    listA.add("aaa");
    listA.add("eee");
    listA.add(new String("ccc"));
    listA.add(1, "ddd");

    [aaa, ddd, eee, ccc]
    ```

- `get(index)`

    값을 꺼내주는 메서드이다

    모든 데이터를 전부 가져오고 싶을 때는 Iterator와 For문을 사용한다

    ```java
    // index를 통한 조회
    String element0 = ListA.get(0);
    String element1 = ListA.get(1);
    String element2 = ListA.get(2);

    // Iterator를 통한 전체 조회
    Iterator<String> iterator = listA.iterator();

    while (iterator.hasNext()) {
        String element = itrator.next();
        sout(element);
    }

    // for-loop를 통한 전체 조회
    for (Object obj : ListA) {
        String element = (String)obj;
    }
    ```
    
    리스트 내에는 `객체가 저장`된다




- List`<String>` `제네릭(Generics)`

    <> 안에 어떤 타입을 선언해주어 해당 List가 사용할 객체의 타입을 지정해준다는 뜻이다

    다룰 객체의 타입을 미리 명시하므로써 객체 캐스팅의 필요성을 없앤다

    1. 타입의 안전성 : 의도하지 않은 타입의 객체저장을 막는다
    2. 캐스팅을 줄여 코드의 간결함

<br>

- `제네릭의 다형성`

    제네릭은 클래스, 인터페이스 등 다앙하게 사용된다
    
    ```java
    List<Sports> arrList = new ArrayList<Sports>();

    arrList.add(new Sports());
    arrList.add(new Soccer());
    arrList.add(new BaseBall());

    class Soccer extends Sports {}
    class Baseball extends Sports {}

    하위 클래스 객체가 부모 클래스 타입으로 선언된 List에 저장될 수 있다

    Sports sports = arrList.get(0);
    Soccer soccer = (Soccer)arrList.get(1); // 꺼낼때는 캐스팅이 필요하다
    ```

- `기타 메서드`

    1. 값의 대 소 비교 메서드

        ```java
        Math.max()
        Math.min()
        ```

    2. Integer to String

        ```java
        int num = 10;
        String str1 = integer.toString(num);
        String str2 = "" + num;
        ```

    3. 길이를 구하는 메서드

        ```java
        String str1 = "ABCDE";

        str1.length();
        ```




## 📝 [문제2](https://github.com/ejaee/java-onboarding/blob/main/docs/PROBLEM2.md)

### ****기능 목록****


- 받은 String 암호문이 유효한지 검증하는 기능
  
    ☑️ [예외처리] 암호문의 길이가 1이상 1000이하가 아닌지 검증하는 기능

    ☑️ [예외처리] 암호문의 구성요소가 소문자로 이루어지지 않았는지 검증하는 기능
  
 
- 조건에 맞게 해독하는 기능

    ☑️ 연속하는 중복 문자들이 없을때까지 반복하는 기능

    ☑️ 연속하는 중복 문자들을 범위를 구하는 기능

    ☑️ 받아온 범위만큼 문자를 삭제하는 기능

- 해독된 문자열을 반환하는 기능


### ****학습 내용****


1. `예외 발생시키기`

    ```java
    throw new IllegaArgumentException("Error");
    ```

    인자의 예외사항이 발생한 경우,

    잘못된 인자가 들어왔음을 뜻하는 `IllegaArgumentException`의 메서드에 출력하고자하는 에러메세지를 입력한 후

    `new`를 통해 에러를 생성하고 `throw` 하면

    `런타임에러`를 실행해 프로그램을 종료시킴과 동시에 에러메세지를 출력할 수 있다
    
2. `String` vs `StringBuilder`

    String은 값을 바꿀 수 없다

    값을 바꾸는 것 같은 행동이 사실은 객체를 게속 생성하는 것이다

    값을 바꿀 수 있는 class가 바로 `StringBuilder`이다

- `sb.delete(start, end)`

    값을 수정할 때 사용되는 메서드로,

    start<= < end 범위의 값을 삭제한다

- `sb.toString()`

    StringBuilder을 String으로 캐스팅한다

3. Pattern.matches("^[a-z]*$", str)

    Pattern class의 matches 메서드로,

    문자열의 `구성요소를 확인`할 수 있다

- `"^[a-z]*$"`

    `^` : 문자열의 시작을 의미한다

    `[a-z]` 유효한 문자들의 리스트를 의미한다

    `*` : 반복을 의미한다

    `$` : 문자열이 끝났음을 의미한다


  

## 📝 [문제3](https://github.com/ejaee/java-onboarding/blob/main/docs/PROBLEM3.md)

### ****기능 목록****


- 받은 숫자가 유효한지 검증하는 기능
  
    ☑️ [예외처리] 숫자의 길이가 1이상 10,000이하가 아닌지 검증하는 기능
 
- 받은 숫자에 대한  총 손뼉 횟수를 구하는 기능
  
    ☑️ 1부터 받은 숫자까지 반복하는 기능

    ☑️ 각 숫자마다 손뼉의 횟수를 누적 저장하는 기능


- 하나의 숫자에 대한 손뼉 횟수를 구하는 기능

    ☑️ 숫자 각 자릿수에 3, 6, 9가 있을때마다 손뼉치는 횟수를 세는 기능


###  ****학습 내용****

.

## 📝 [문제4](https://github.com/ejaee/java-onboarding/blob/main/docs/PROBLEM4.md)

### ****기능 목록****

- 받은 문자열 word가 유효한지 검증하는 기능

    ☑️ [예외처리] word의 길이가 1 이상 1,000 이하인지 검증하는 기능

- 문자열을 문제의 조건에 맞게 바꾸는 기능

    ☑️💥 문자열이 끝날때까지 반복하는 기능

    ☑️ 문자열의 각 문자 중 알파벳만 반대로 뒤집는 기능

### ****학습 내용****

1. String

    String은 값을 바꿀 수 없으므로

    기존의 값을 바꾸려면 `char[]`로 바꾼다

    ```java
    String word = "Hello";

    char[] arrChar = word.toCharArray();
    
    를 통해 배열을 생성할 수 있다
    ```

- `isUpperCase(char c)` | `isUpperCase(char c)`

    문자의 대, 소문자를 확인할 수 있는 메서드

- `toString()` vs `String.valueOf()`

    두 메서드 모두 Object -> String 으로 반환한다

    이 둘의 차이는 다음과 같다

    `toString()`
    - 대상 값이 null이면 NPE를 발생시키고 Object에 담긴 값이 String이 아니여도 출력한다.

    `String.valueOf()`
     - 파라미터가 null이면 문자열 "null"을 만들어서 반환한다.

    두가지 메서드의 차이점은 null값에 따른 `Null PointerException(NPE)`의 발생 유무이다

    `String.valueOf()`를 사용하자


## 📝 [문제5](https://github.com/ejaee/java-onboarding/blob/main/docs/PROBLEM5.md)

### ****기능 목록****

- 받은 숫자 money가 유효한지 검증하는 기능

    ☑️ [예외처리] money가 1 이상 1,000,000 이하인지 검증하는 기능

- 답을 구해오는 기능

    ☑️ money가 모든 화폐 단위와 비교할 수 있도록 반복하는 기능

    ☑️ 최소한의 화폐 단위로 money를 구성하는 기능

### ****학습 내용****

- `Arrays.asList()` | `List.of()`로 List 생성하기

    ```java
    List<String> asList = Arrays.asList();
    List<String> listOf = List.of();
    ```

    `Arrays.asList()`

    - Arrays.asList()의 리턴값은 java.util.ArrayList이 아닌 Arrays클래스의 내부클래스 ArrayList이다
    - add와 remove를 구현할 수 없는 이유는 참조로 동작하기 때문이다

    List.of()`

    - JAVA 9 부터 지원하는 메서드이다. 
    - ListN이라는 타입의 객체를 반환한다
    - 값을 기반으로 독립적인 객체를 만들기 때문에 참조가 일어나지 않는다 
    -  Immutable한 Collection

    Arrays.asList()는 List.of()보다 힙에 더 많은 개체를 생성하기 때문에 더 많은 오버헤드 공간을 차지한다

    따라서, `단지 값 요소가 필요한 경우`라면 `List.of()가 적합`하다

    Arrays.asList(), List.of() 모두 크기는 변경할 수 없다. `크기를 바꾸려면 Collections을 생성해서 요소의 값을 옮겨야 한다`

    ||Array.asList|List.of|
    |------|---|---|
    |삽입(add)|불가능|불가능|
    |삭제(remove)|불가능|불가능|
    |변경(set, replace)|가능|불가능|
    |Null허용여부|허용|허용X|





## 📝 [문제6](https://github.com/ejaee/java-onboarding/blob/main/docs/PROBLEM6.md)

### ****기능 목록****

- 받은 List가 유효한지 검증하는 기능

    ☑️ [예외처리] 크루의 수가 1명 이상 10,000명 이하인지 검증하는 기능
    ☑️ [💥예외처리] 닉네임이 한글로만 구성되고 전체 길이가 1자 이상 20자 미만인지 검증하는 기능
    ☑️ [💥예외처리] 이메일이 이메일 형식에 부합하고 전체 길이는 11자 이상 20자 미만인지 검증하는 기능
    ☑️ [예외처리] 이메일 도메인이 email.com인지 검증하는 기능

- 답을 구해오는 기능

- 맵을 만드는 기능

    ☑️ 받은 List를 key와 value를 가진 map으로 만드는 기능

- 모든 닉네임을 서로 한번씩 검증하는 기능
- 한 개의 닉네임이 서로 다른 닉네임들과 모두 비교하는 기능
- 두 개의 닉네임이 서로 중복되었는지 확인하는 기능
- 중복된 닉네임을 저장하는 기능
- 중복된 닉네임들의 이메일을 정렬하는 기능

### ****학습 내용****

1. `Set`

    Set은 List와는 다르게 객체(데이터)를 중복해서 저장할 수 없다

    저장 순서가 보장되지 않는다

    수학의 집합과 같다

    HashSet, TreeSet, LinkedHashSet이 있다

    인덱스로 객체를 관리하지 않기 때문에 데이터를 검색하기 위해서는 iterator() 메서드로 Iterator(반복자)를 생성하고 데이터를 가져와야 한다


    ```java
    Set<String> set = new HashSet<String>();
	
    set.add("one"); // 데이터 저장(추가)
	set.add("two");
	set.add("three");
	set.add("one");

    Iterator<String> it = set.iterator(); // Iterator(반복자) 생성

	while (it.hasNext()) { // hasNext() : 데이터가 있으면 true 없으면 false
		System.out.println(it.next()); // next() : 다음 데이터 리턴
	}

    it = set.iterator(); // 반복자 재생성(위의 반복문에서 next 메서드로 데이터를 다 가져왔기 때문에 재생성을 해야함)
    ```

    특징

    - 순서가 없다
    - 중복을 허용하지 않는다
    - 쓰임 : 소수의 집합

    입력된 순서대로 데이터를 관리하고 싶다면 `LinkedHashSet`를 활용한다
    

2. Map

    키와 값의 쌍으로 이루어진 데이터의 집합이다

    List와 Set의 공통부분을 뽑아서 컬렉션 interface를 정의했다

    특징
    - 저장 순서가 없다
    - 키는 중복 허용 안한다
    - 값은 중복 허용 한다
    - ex) id-passwd, 02-서울


- HashMap

    _map 인터페이스 구현_

    데이터를 키와 값의 쌍으로 저장

    Hashtable은 옛날 버전(동기화가 되어있음)

    순서를 유지해야하는 경우 `LinkedHashMap` 클래스 사용

- HashMap의 키와 값

    `해싱 기법`으로 데이터를 저장

    데이터가 많아도 `검색이 빠르다`

    ```java
    HashMap map = new Hashmap();
    map.put("Id_1", "123");
    map.put("Id_2", "456");
    map.put("Id_2", "789");

    [저장 상태]

    Id_1 | 123 -> entry
    Id_2 | 789
    ```

- 해싱

    어떤 키값을 주면 해당 배열의 인덱스를 알려준다

    즉 키를 받아 저장위치(해쉬코드)를 알려준다

    즉 해쉬함수를 이용해서 데이터를 저장하고 읽어오는 것

    다시말해 `해시함수`로 `해시테이블`에 데이터를 `저장`, `검색`

    `해시테이블`은 `배열`과 `링크드리스트`가 조합된 형태

  - 배열 : 접근성
  - 링크드리스트 : 변경에 유리



- 주요 메서드

    Object put(Object key, Object value)

    - key와 value를 저장

    void putAll(Map m)

    - m을 모두 저장

    Object remove(Object key)

    - key 삭제

    Object replace(Object key, Object value)

    - 기존에 저장된 key에 새로운 값을 저장

    Set entrySet()

    - entry 쌍들로 이루어진 Set을 얻을 수 있음

    Set keySet()

    - key값만 가져옴

    Collection values()

    - value값만 가져옴

    Object get(Object key)

    - key값을 넣으면 해당하는 값을 가져옴

    Object getOrDefault(Object key, Object defaultValue)

    - 없는 key을 넣었을때 두번째 매개변수가 반환됨

    boolean containsKey(Object key)

    - 해당 key가 있는지 확인

    boolean containsValue(Object Value)

    - 해당 value가 있는지 확인


3. str.split("구분자")

    구분자를 기준으로 배열을 2차 배열로 나눈다


## 📝 [문제7](https://github.com/ejaee/java-onboarding/blob/main/docs/PROBLEM7.md)

### ****기능 목록****

- 받은 List가 유효한지 검증하는 기능

    ☑️ [예외처리] user, friends, visitor 아이디의 길이가 1 이상 30 이하인지 검증하는 기능
    ☑️ [예외처리] 사용자 아이디가 소문자로만 이루어졌는지 검증하는 기능
    ☑️ [예외처리] friends의 size가 1이상 10,000이하인지 검증하는 기능
    ☑️ [예외처리] friends[0]의 size가 2인지 검증하는 기능
    ☑️ [예외처리] 동일한 친구 관계가 중복되지 않았는지 검증하는 기능
    ☑️ [예외처리] visitors 길이가 0 이상 10,000 이하인 리스트/배열인지 검증하는 기능

- 답을 구해오는 기능
- 사용자의 친구들을 저장하는 기능
- 사용자와 함께 아는 친구에게 10점을 부여하는 기능
- 사용자의 타임 라인에 방문한 사람들의 횟수만큼 1점을 부여하는 기능
- 결과값을 정렬하는 기능

### ****학습 내용****

1. Comparator | Comparable

    Comparable

    - 기본 정렬기준을 구현하는데 사용
    - compareTo(대상)

    Comparator

    - 사용자가 만든 기준으로 정렬하고자 할 때 사용
    - compare(대상, 기준)

    문제에서 point를 비교한 후 값이 같을 경우 String을 비교해야 한다면 오버라이딩을 통해 구현

    ```java
    Class Person implements Camparable<Person>{
            ...

        @Override
        public int compareTo(Person p) {
            if (getPointAsInteger() < p.getPointAsInteger()) {
                return 1;
            } else if (getPointAsInteger() < p.     getPointAsInteger()) {
                return -1;
            } else {
                int compareString = getNameAsString().compareTo(p.getNameAsString());
                if (compareString == 1) {
                    return 1;
                } else if (compareString == -1) {
                    return -1;
                }
            }
        return 0;
        }
    }

    ```

