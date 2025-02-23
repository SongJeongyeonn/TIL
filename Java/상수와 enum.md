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

## enum

