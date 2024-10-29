# abstract
반드시 **상속을 하여 사용**하도록 강제한다.

구체적인 로직을 포함하지 않으며, 그 형태만 지니고 있어 사용자에게 그 역할을 넘긴다.

맴버 중 하나라도 abstract를 가지고 있다면, 그 맴버를 담고있는 클래스 또한 abstract 클래스가 된다.
```java
abstract class A{ // 추상 클래스 A
    public abstract int b(); // 추상메서드는 본체가 없다.(사용을 위해서는 )
    /* 본체가 있는 메서드는 abstract 키워드를 가질 수 없다.
    public abstract int c() {System.out.println("Hello")}  메서드의 구체적인 로직이 담겨있으므로 abstract로 사용 불가
    추상 클래스 내에는 추상 메서드가 아닌 메서드가 존재할 수 있다.
     */
    public void d(){
        System.out.println("world");
    }
}
class B extends A{
    public int b(){ // A 클래스에서 b 메서드가 추상 메서드로, 오버라이딩을 해야 사용할 수 있다.
        return 1;
    }

}
public class AbstractDemo {
    public static void main(String[] args) {
        //A obj = new A();  abstract 클래스로 인스턴스화 할 수 없다.
        B obj = new B();
    }
}

```
## 사용하는 이유
맥락에 따라 달라질 수 있는 기능이 있을때 추상 클래스를 사용하여, 사용자게 용도에 맞게 규약하는 것

```java
abstract class Calculator{
    int left, right;
    public void setOprands(int left, int right){
        this.left = left;
        this.right = right;
    }
    public abstract void sum();
    public abstract void avg();
    public void run(){ // 호출 순서 로직
        sum();
        avg();
    }
}
class CalculatorDecoPlus extends Calculator {
    public void sum(){  // 사용자가 각 하위 클래스의 용도에 맞게 구현한다.
        System.out.println("+ sum :"+(this.left+this.right));
    }
    public void avg(){
        System.out.println("+ avg :"+(this.left+this.right)/2);
    }
}
class CalculatorDecoMinus extends Calculator {
    public void sum(){
        System.out.println("- sum :"+(this.left+this.right));
    }
    public void avg(){
        System.out.println("- avg :"+(this.left+this.right)/2);
    }
}
public class CalculatorDemo {
    public static void main(String[] args) {
        CalculatorDecoPlus c1 = new CalculatorDecoPlus();
        c1.setOprands(10, 20);
        c1.run();

        CalculatorDecoMinus c2 = new CalculatorDecoMinus();
        c2.setOprands(10, 20);
        c2.run();
    }

}
```
위의 코드에서 공통된 부분인 run는 클래스가 구현한다. 

그리고 **맥락에 따라 달라지는 sum, avg는 abstract로 형식만 제공**하여 사용자가 구현한다.

## 디자인 패턴(Design Patterns)
로직의 전개 구성에서 공통적으로 반복되는 패턴을 모아서 정리한 것이다.
1. 행위에 대해 패턴이름이 정해져 있어, **의사소통을 원활이 도울 수 있다.**
2. 패턴을 익혀가는 과정에서 **효율적인 로직의 설계 방법을 공부할 수 있다.**


# final
상속/변경을 금지한다.

``` java
class Calculator {
    static final double PI = 3.14; // PI는 공통적으로 쓰이므로 바뀌면 안된다.
    int left, right;

    public void setOprands(int left, int right) {
        this.left = left;
        this.right = right;
        //Calculator.PI = 6;
    }

    public void sum() {
        System.out.println(this.left + this.right);
    }

    public void avg() {
        System.out.println((this.left + this.right) / 2);
    }
}

public class CalculatorDemo1 {

    public static void main(String[] args) {

        Calculator c1 = new Calculator();
        System.out.println(c1.PI);
        //Calculator.PI = 10; final로 고정되어있어 변경이 불가하다.


    }
}
```
## final 메서드와 final 클래스
final 키워드가 붙은 메서드와 클래스는 모두 상속이 불가능 하다.

아래의 코드는 final 메서드 b를 상속하려 하여 오류가 발생한다.
```java
class A{
    final void b(){}
}
class B extends A{
    void b(){}
}
```
아래의 코드는 final 클래스 C를 상속하려 하여 오류가 발생한다.
```java
final class C{
    final void b(){}
}
class D extends C{}
```