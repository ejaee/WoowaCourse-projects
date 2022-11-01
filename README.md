# ???? ****����� ��ũ �ڽ� 5�� �����ڽ� ����****

_�������ũ�ڽ����� �н��� ������ �����մϴ�_



### ****�Ⱓ****

- '22.10.26. ~ '22.11.22.

### ****����̼�****

|Project|Repository|Pull Request|
|------|---|---|
|onboarding|.|.|
|.|.|.|
|.|.|.|
|.|.|.|


## ****1����****

? [Problem1](https://github.com/ejaee/java-onboarding/blob/main/docs/PROBLEM1.md)

### ****��� �䱸����****

****��� ���****

- å�� ���� �������� ������ ������ �� �ޱ�

    ?? [����ó��] å�� 1���� 400������ ������ ����� ���� ���� ���

    ?? [����ó��] ù ��° ��Ҵ� Ȧ��, �� ��° ��Ҵ� ¦���� �ƴ� ���

    ?? [����ó��] �� ��Ұ� ���ӵ� �ڿ����� �ƴ� ���

    ?? [?����ó��] 1�̳� 400�� �����ϰ� �ִ� ���

    ?? [?����ó��] ���� �������� �� ��Ұ� �ƴ� ���
    - ���ܻ��� �� return -1

 
- ���� ������ ���� Ȱ���� �ִ밪 ���ϱ�
  
    ?? �÷��̾ ���� �� �������� Ȱ���� ���ǿ� �´� �ִ밪 ���ϱ�
    
    ?? ������ �� �ڸ� ������ �հ� �� �� �ִ밪 ���ϱ�

    ?? ���� �������� ������ ������ �� �ִ밪 ���ϱ�


- �� �÷��̾��� �ִ밪�� ���ϴ� ���

    ?? �� �÷��̾��� ���ڸ� ���� ���Ͽ� �º� ����� ��ȯ�ϱ�
    - pobi�� �̱� �� return 1
    - crong�� �̱� �� return 2
    - ���º� �� return 0
    - ���ܻ��� �� return -1

### ****�н� ����****

1. `List<integer> pages`

    java���� �÷��� �����ӿ��� �ٽ� �������̽��� �����Ѵ�

    ```
    �÷���
    -> ���� ��ü�� ��� ���� ��

    �����ӿ�
    -> ǥ��ȭ, ����ȭ�� ü������ ���α׷��� ���

    �÷��� �����ӿ�
    -> �÷���(�ټ��� ��ü)�� �ٷ�� ���� ǥ��ȭ�� ���α׷��� ���
    -> ��ü(������)�� �ٷ�� 
        : ����, �˻�, ����, ����...

    �÷��� Ŭ����
    -> �ټ��� �����͸� ������ �� �ִ� Ŭ����
        :  Arraylist, HashSet, Vector...
    ```


    - List
    - Set
    - Map

- List

    �迭�� ���� ������ �Ѱ踦 �ذ��ϱ����� ������� Ŭ������,

    �޸� ��� ���� ������ �Լ� �߰� �� �� �ֵ��� ���� �ڷ��� Ŭ�����̴�

    ```java
    List<String> listA = new ArrayList<String>();
    List<String> listB = new LinkedList<String>();
    List<String> listC = new Vector<String>();
    List<String> listD = new Stack<String>();
    ```

    Ư¡

    - ������ �ִ�
    - �ߺ��� ����Ѵ�
    - ���� : ����� ���

- add()

    List�� ���� �߰��ϱ� ���� �޼����̴�

    ```java
    List<String> listA = new ArrayList<String>();

    listA.add("aaa");
    listA.add("eee");
    listA.add(new String("ccc"));
    listA.add(1, "ddd");

    [aaa, ddd, eee, ccc]
    ```

- get(index)

    ���� �����ִ� �޼����̴�

    ��� �����͸� ���� �������� ���� ���� Iterator�� For���� ����Ѵ�

    ```java
    // index�� ���� ��ȸ
    String element0 = ListA.get(0);
    String element1 = ListA.get(1);
    String element2 = ListA.get(2);

    // Iterator�� ���� ��ü ��ȸ
    Iterator<String> iterator = listA.iterator();

    while (iterator.hasNext()) {
        String element = itrator.next();
        sout(element);
    }

    // for-loop�� ���� ��ü ��ȸ
    for (Object obj : ListA) {
        String element = (String)obj;
    }
    ```
    
    ����Ʈ ������ `��ü�� ����`�ȴ�




- List`<String>` ���׸�(Generics)

    <> �ȿ� � Ÿ���� �������־� �ش� List�� ����� ��ü�� Ÿ���� �������شٴ� ���̴�

    �ٷ� ��ü�� Ÿ���� �̸� ����ϹǷν� ��ü ĳ������ �ʿ伺�� ���ش�

    1. Ÿ���� ������ : �ǵ����� ���� Ÿ���� ��ü������ ���´�
    2. ĳ������ �ٿ� �ڵ��� ������

<br>

- ���׸��� ������

    ���׸��� Ŭ����, �������̽� �� �پ��ϰ� ���ȴ�
    
    ```java
    List<Sports> arrList = new ArrayList<Sports>();

    arrList.add(new Sports());
    arrList.add(new Soccer());
    arrList.add(new BaseBall());

    class Soccer extends Sports {}
    class Baseball extends Sports {}

    ���� Ŭ���� ��ü�� �θ� Ŭ���� Ÿ������ ����� List�� ����� �� �ִ�

    Sports sports = arrList.get(0);
    Soccer soccer = (Soccer)arrList.get(1); // �������� ĳ������ �ʿ��ϴ�
    ```

- ��Ÿ �޼���

    1. ���� �� �� �� �޼���

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

    3. ���̸� ���ϴ� �޼���

        ```java
        String str1 = "ABCDE";

        str1.length();
        ```

---


? [Problem2](https://github.com/ejaee/java-onboarding/blob/main/docs/PROBLEM1.md)

### ****��� �䱸����****

- String ��ȣ�� �ޱ�
  - [����ó��] ��ȣ���� ���̰� 1�̻� 1000���ϰ� �ƴ� ���
  - [����ó��] ��ȣ���� ������Ұ� �ҹ��ڷ� �̷������ ���� ���
  
 
- ���ǿ� �°� �ص��ϱ�
- 
  - pobi�� �̱� �� return 1
  - crong�� �̱� �� return 2
  - ���º� �� return 0
  - ���ܻ��� �� return -1



****��� ���****

****�н� ����****


? [Problem3](https://github.com/ejaee/java-onboarding/blob/main/docs/PROBLEM1.md)

### ****��� �䱸����****

****��� ���****

****�н� ����****

? [Problem4](https://github.com/ejaee/java-onboarding/blob/main/docs/PROBLEM1.md)

### ****��� �䱸����****

****��� ���****

****�н� ����****

? [Problem5](https://github.com/ejaee/java-onboarding/blob/main/docs/PROBLEM1.md)

### ****��� �䱸����****

****��� ���****

****�н� ����****

? [Problem6](https://github.com/ejaee/java-onboarding/blob/main/docs/PROBLEM1.md)

### ****��� �䱸����****

****��� ���****

****�н� ����****

? [Problem7](https://github.com/ejaee/java-onboarding/blob/main/docs/PROBLEM1.md)

### ****��� �䱸����****

****��� ���****

****�н� ����****