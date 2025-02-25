# 상수와 enum

## 상수
상수는 **변하지 않는 값**이다.
```java
public static void main(String[] args) {
        /*
         * 1. 사과
         * 2. 복숭아
         * 3. 바나나
         */
        int type = 1;
        switch(type){
            case 1:
                System.out.println(57);
                break;
            case 2:
                System.out.println(34);
                break;
            case 3:
                System.out.println(93);
                break;
        }
    }
```
이 코드에서 1의 과일은 언제나 사과이다.

고정된 **상수 값**에 따라 **주석을 통해 과일의 이름을 임의로 지정**해놓았기 때문이다.

그렇기에 나중에 **주석에 이상이 생기면 코드를 알아보기 힘들다.**

```java
public class ConstantDemo {
    private final static int APPLE = 1;
    private final static int PEACH = 2;
    private final static int BANANA = 3;
    public static void main(String[] args) {
        int type = APPLE;
        switch(type){
            case APPLE:
                System.out.println(57+" kcal");
                break;
            case PEACH:
                System.out.println(34+" kcal");
                break;
            case BANANA:
                System.out.println(93+" kcal");
                break;
        }
    }
}
```

이렇게 코드를 수정하게 되면, 주석이 사라지더라도 **변수 이름**을 통해 1이 사과라는 것을 알 수 있다.

이전의 코드가 숫자(상수 값)를 통해 의미를 지정했다면, 이 코드는 **상수를 통해 의미를 지정**했다고 볼 수 있다.

## enum 도입된 배경

위의 코드에서 기업 명에 대한 변수도 필요해져서 추가를 하면 아래와 같이 된다.
```java
public class ConstantDemo {
    // fruit
    private final static int APPLE = 1;
    private final static int PEACH = 2;
    private final static int BANANA = 3;
     
    // company
    private final static int GOOGLE = 1;
    //private final static int APPLE = 2;
    private final static int ORACLE = 3;
     
    public static void main(String[] args) {
        int type = APPLE;
        switch(type){
            case APPLE:
                System.out.println(57+" kcal");
                break;
            case PEACH:
                System.out.println(34+" kcal");
                break;
            case BANANA:
                System.out.println(93+" kcal");
                break;
        }
    }
}
```
위에서 **'private final static int APPLE = 2;'** 에 주석을 단 이유는 **이미 같은 변수가 선언**이 되어있기 때문이다.

그리고 코드를 작성해 보면 알 수 있듯 **컴파일을 하지 않아도 final의 특성상 오류가 있다는 것을 알 수 있다.**

하지만 이러한 충돌 문제는 앞에 **접두사**를 붙여서 해결할 수 있다.
```java
public class ConstantDemo {
    // fruit(과일일)
    private final static int FRUIT_APPLE = 1;
    private final static int FRUIT_PEACH = 2;
    private final static int FRUIT_BANANA = 3;
     
    // company(기업)
    private final static int COMPANY_GOOGLE = 1;
    private final static int COMPANY_APPLE = 2;
    private final static int COMPANY_ORACLE = 3;
     
    public static void main(String[] args) {
        int type = FRUIT_APPLE;
        switch(type){
            case FRUIT_APPLE:
                System.out.println(57+" kcal");
                break;
            case FRUIT_PEACH:
                System.out.println(34+" kcal");
                break;
            case FRUIT_BANANA:
                System.out.println(93+" kcal");
                break;
        }
    }
}
```
#### 이렇게 같은 이름을 사용하는 변수,함수 이름을 소속을 구분하는는 기법을 네임스페이스라고 한다.

다시 코드를 봐보면 줄줄이 이어지는 상수들이 **복잡**해 보인다.

이를 **인터페이스(interface)** 를 사용하여 더 **간단**하게 만들 수 있다.
```java
interface FRUIT{
    int APPLE=1, PEACH=2, BANANA=3;
}
interface COMPANY{
    int GOOGLE=1, APPLE=2, ORACLE=3;
}
 
public class ConstantDemo {
     
    public static void main(String[] args) {
        int type = FRUIT.APPLE;
        switch(type){
            case FRUIT.APPLE:
                System.out.println(57+" kcal");
                break;
            case FRUIT.PEACH:
                System.out.println(34+" kcal");
                break;
            case FRUIT.BANANA:
                System.out.println(93+" kcal");
                break;
        }
    }
}
```
**접미사로 구분했던 부분을 인터페이스를 바꾸며**, 언어의 특성을 더 잘 살릴 수 있다.

이렇게 인터페이스에서 선언된 변수를 사용할 수 있는 이유는 **인터페이스에서 선언된 변수는 무조건 public static final의 속성**을 같기 때문이다.

하지만 여기 문제가 있다. **만약 int type의 값을 FRUIT.APPLE가 아니라 COMPANY.GOOGLE를 넣더라도 결과가 동일하게 57kcal**가 나온다는 것이다.

왜냐하면 FRUIT.APPLE과 COMPANY.GOOGLE은 둘다 값이 int타입에 1이라는 값을 가지고 있기 때문이다.

기업 구글과 과일 애플이 같다는 것은 말도 안되고, 애초에 기업에 칼로리가 붙으면 안되기 때문에 **기업과 과일을 비교할 수 없도록** 코드를 작성해야한다.

```java
class Fruit{
    // Fruit 타입의 상수 객체 생성 (각각 독립적인 객체)
    public static final Fruit APPLE  = new Fruit();
    public static final Fruit PEACH  = new Fruit();
    public static final Fruit BANANA = new Fruit();
}
class Company{
    // Company 타입의 상수 객체 생성 (각각 독립적인 객체)
    public static final Company GOOGLE = new Company();
    public static final Company APPLE = new Company();
    public static final Company ORACLE = new COMPANY(Company);
}
 
public class ConstantDemo {
     
    public static void main(String[] args) {
        // 서로 다른 클래스(Fruit와 Company)의 객체 비교 [컴파일 오류 발생]
        if(Fruit.APPLE == Company.APPLE){
            System.out.println("과일 애플과 회사 애플이 같다.");
        }
    }
}
```

이렇게 코드를 바꾸게 되면, **서로 다른 클래스의 객체를 비교하는 것이기에** 'Fruit.APPLE == Company.APPLE' 코드가 실행되지 못하고 **에러가 발생한다**.

하지만 위의 코드는  **switch 문에서 사용할 수 없고 또 하나는 선언이 너무 복잡하다.**

그래서 이러한 점은 보완하기 위해 **enum**이 나오게되었다.

# enum
#### enum은 열거형(enumerated type)으로 서로 연관된 상수들의 집합이다.

위의 예제에서는 Fruit와 Company가 하는 역할이 열거인 셈이다.

enum을 사용하여 위의 코드를 바꾸면 아래와 같이 바뀐다.
```java
enum Fruit{
    APPLE, PEACH, BANANA;
}
enum Company{
    GOOGLE, APPLE, ORACLE;
}
 
public class ConstantDemo {
     
    public static void main(String[] args) {
        /*
        if(Fruit.APPLE == Company.APPLE){
            System.out.println("과일 애플과 회사 애플이 같다.");
        }
        */
        Fruit type = Fruit.APPLE;
        switch(type){
            case APPLE:
                System.out.println(57+" kcal");
                break;
            case PEACH:
                System.out.println(34+" kcal");
                break;
            case BANANA:
                System.out.println(93+" kcal");
                break;
        }
    }
}
```
위의 코드에서 enum으로 바꾼 부분 일부를 살펴보자

```java
enum Fruit{
    APPLE, PEACH, BANANA;
}
``` 

enum은 class, interface와 동급의 형식을 가지는 단위다.

아래의 코드는 위의 코드를 class를 사용해 바꾼 것이다.

```java
class Fruit{
    public static final Fruit APPLE  = new Fruit();
    public static final Fruit PEACH  = new Fruit();
    public static final Fruit BANANA = new Fruit();
    private Fruit(){}
}
```
enum은 **생성자의 접근 제어자가 private**이다.

이는 Fruit는 미리 정의된 객체만 사용이 가능하고, **외부에서 객체로 만들 수 없다는 것을 의미**한다.

#### enum을 사용하는 이유는 다음과 같다.
- 코드가 단순해진다.(switch문에서도 활용 가능)
- 인스턴스 생성과 상속을 방지한다.
- 키워드 enum을 사용하여 구현의 의도가 열거임을 분명하게 나타낼 수 있다.

## enum과 생성자
enum은 클래스와 같이 생성자를 가질 수 있다.
```java
enum Fruit{
    APPLE, PEACH, BANANA;
    Fruit(){ // enum과 이름이 같은 메서드(생성자)이다.
        System.out.println("Call Constructor "+this);
    }
}
 
enum Company{
    GOOGLE, APPLE, ORACLE;
}
 
public class ConstantDemo {
     
    public static void main(String[] args) {
     
        /*
        if(Fruit.APPLE == Company.APPLE){
            System.out.println("과일 애플과 회사 애플이 같다.");
        }
        */
        Fruit type = Fruit.APPLE;
        switch(type){
            case APPLE:
                System.out.println(57+" kcal");
                break;
            case PEACH:
                System.out.println(34+" kcal");
                break;
            case BANANA:
                System.out.println(93+" kcal");
                break;
        }
    }
}
```
위의 코드의 결과는 아래와 같다.
```
Call Constructor APPLE
Call Constructor PEACH
Call Constructor BANANA
57 kcal
```
Call Constructor가 출력된 것은 생성자 Fruit가 호출되었음을 의미한다.

그리고 필드의 개수가 3개이기에 3번 호출되었다.

하지만 아래와 같이 코드를 바꾸면 에러가 발생한다.
```java
enum Fruit{
    APPLE, PEACH, BANANA;
    public Fruit(){
        System.out.println("Call Constructor "+this);
    }
}
``` 
그 이유는 enum의 생성자가 접근 제어자 private만을 허용하기 때문이다.

생성자의 매개변수를 통해 필드의 값을 부여하는 방법은 아래의 코드처럼 상수 선언과 동시에 생성자를 호출하는 방법이 있다.
```java
enum Fruit{
    APPLE("red"), PEACH("pink"), BANANA("yellow");
    public String color;
    Fruit(String color){
        System.out.println("Call Constructor "+this);
        this.color = color;
    }
}
 
enum Company{
    GOOGLE, APPLE, ORACLE;
}
 
public class ConstantDemo {
     
    public static void main(String[] args) {
        /*
        if(Fruit.APPLE == Company.APPLE){
            System.out.println("과일 애플과 회사 애플이 같다.");
        }
        */
        Fruit type = Fruit.APPLE;
        switch(type){
            case APPLE:
                System.out.println(57+" kcal, "+Fruit.APPLE.color);
                break;
            case PEACH:
                System.out.println(34+" kcal"+Fruit.PEACH.color);
                break;
            case BANANA:
                System.out.println(93+" kcal"+Fruit.BANANA.color);
                break;
        }
    }
}
```
또한 아래와 같이 열거형은 메서드를 가질 수 있다.
```java
enum Fruit{
    APPLE("red"), PEACH("pink"), BANANA("yellow");
    private String color;
    Fruit(String color){
        System.out.println("Call Constructor "+this);
        this.color = color;
    }
    String getColor(){
        return this.color;
    }
}
 
enum Company{
    GOOGLE, APPLE, ORACLE;
}
 
public class ConstantDemo {
     
    public static void main(String[] args) {
        Fruit type = Fruit.APPLE;
        switch(type){
            case APPLE:
                System.out.println(57+" kcal, "+Fruit.APPLE.getColor());
                break;
            case PEACH:
                System.out.println(34+" kcal"+Fruit.PEACH.getColor());
                break;
            case BANANA:
                System.out.println(93+" kcal"+Fruit.BANANA.getColor());
                break;
        }
    }
}
```
그리고 아래와 같이 맴버 전체를 열거하는 기능 또한 제공하고 있다.
```java
enum Fruit{
    APPLE("red"), PEACH("pink"), BANANA("yellow");
    private String color;
    Fruit(String color){
        System.out.println("Call Constructor "+this);
        this.color = color;
    }
    String getColor(){
        return this.color;
    }
}
 
enum Company{
    GOOGLE, APPLE, ORACLE;
}
 
public class ConstantDemo {
     
    public static void main(String[] args) {
        for(Fruit f : Fruit.values()){
            System.out.println(f+", "+f.getColor());
        }
    }
}
```

열거형에 대해 다시 한번 정리해보자!

1. 열거형은 연관된 값들을 저장한다.

2. 값들이 변경되지 않도록 보장한다.

3. 열거형 자체가 클래스이기 때문에 열거형 내부에 생성자, 필드, 메소드를 가질 수 있어서 단순히 상수가 아니라 더 많은 역할을 할 수 있다.