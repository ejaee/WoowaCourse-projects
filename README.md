# ???? ****우아한 테크 코스 5기 프리코스 진행****

_우아한테크코스에서 학습한 내용을 정리합니다_



### ****기간****

- '22.10.26. ~ '22.11.22.

### ****진행미션****

|Project|Repository|Pull Request|
|------|---|---|
|onboarding|.|.|
|.|.|.|
|.|.|.|
|.|.|.|


## ****1주차****

? [Problem1](https://github.com/ejaee/java-onboarding/blob/main/docs/PROBLEM1.md)

### ****기능 요구사항****

****기능 목록****

- 책의 왼쪽 페이지와 오른쪽 페이지 값 받기

    ?? [예외처리] 책의 1부터 400까지의 범위를 벗어나는 값을 받은 경우

    ?? [예외처리] 첫 번째 요소는 홀수, 두 번째 요소는 짝수가 아닌 경우

    ?? [예외처리] 두 요소가 연속된 자연수가 아닌 경우

    ?? [?예외처리] 1이나 400을 포함하고 있는 경우

    ?? [?예외처리] 받은 페이지가 두 요소가 아닌 경우
    - 예외사항 시 return -1

 
- 받은 페이지 값을 활용해 최대값 구하기
  
    ?? 플레이어가 받은 두 페이지를 활용해 조건에 맞는 최대값 구하기
    
    ?? 페이지 각 자리 숫자의 합과 곱 중 최대값 구하기

    ?? 왼쪽 페이지와 오른쪽 페이지 중 최대값 구하기


- 각 플레이어의 최대값을 비교하는 기능

    ?? 각 플레이어의 숫자를 서로 비교하여 승부 결과를 반환하기
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

- List

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

- add()

    List의 값을 추가하기 위한 메서드이다

    ```java
    List<String> listA = new ArrayList<String>();

    listA.add("aaa");
    listA.add("eee");
    listA.add(new String("ccc"));
    listA.add(1, "ddd");

    [aaa, ddd, eee, ccc]
    ```

- get(index)

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




- List`<String>` 제네릭(Generics)

    <> 안에 어떤 타입을 선언해주어 해당 List가 사용할 객체의 타입을 지정해준다는 뜻이다

    다룰 객체의 타입을 미리 명시하므로써 객체 캐스팅의 필요성을 없앤다

    1. 타입의 안전성 : 의도하지 않은 타입의 객체저장을 막는다
    2. 캐스팅을 줄여 코드의 간결함

<br>

- 제네릭의 다형성

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

- 기타 메서드

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

---


? [Problem2](https://github.com/ejaee/java-onboarding/blob/main/docs/PROBLEM1.md)

### ****기능 요구사항****

- String 암호문 받기
  - [예외처리] 암호문의 길이가 1이상 1000이하가 아닌 경우
  - [예외처리] 암호문의 구성요소가 소문자로 이루어지지 않은 경우
  
 
- 조건에 맞게 해독하기
- 
  - pobi가 이길 시 return 1
  - crong이 이길 시 return 2
  - 무승부 시 return 0
  - 예외사항 시 return -1



****기능 목록****

****학습 내용****


? [Problem3](https://github.com/ejaee/java-onboarding/blob/main/docs/PROBLEM1.md)

### ****기능 요구사항****

****기능 목록****

****학습 내용****

? [Problem4](https://github.com/ejaee/java-onboarding/blob/main/docs/PROBLEM1.md)

### ****기능 요구사항****

****기능 목록****

****학습 내용****

? [Problem5](https://github.com/ejaee/java-onboarding/blob/main/docs/PROBLEM1.md)

### ****기능 요구사항****

****기능 목록****

****학습 내용****

? [Problem6](https://github.com/ejaee/java-onboarding/blob/main/docs/PROBLEM1.md)

### ****기능 요구사항****

****기능 목록****

****학습 내용****

? [Problem7](https://github.com/ejaee/java-onboarding/blob/main/docs/PROBLEM1.md)

### ****기능 요구사항****

****기능 목록****

****학습 내용****