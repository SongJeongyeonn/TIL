## interface
어떤 객체가 특정 인터페이스를 사용할때 그 인터페이스의 메서드들을 반드시 구현해야하도록 강제하는 규제
 ```java
 interface I{
    public void z();
}
class A implements I{
    public void z(){}
}
 ```
#### 인터페이스 안의 메서드는 abstract메서드와 같이 본체가 없다.

 또한 클래스 A는 인터페이스 I를 구현하기에 그 안에 있는 **메서드인 z도 본체를 포함해 구현**해야한다.

 대상이 되는 시스템을 제어하기 위해 사용하는 장치들을 인터페이스라고도 한다.

 그래서 **인터페이스의 맴버들은 무조건 public을 사용**해야한다.
```
interface I5{
    // private void x(); 접근 지정자가 public이 아니라서 에러발생
}
```
 ### 하나의 클래스가 여러개의 인터페이스를 구현 할 수 있다.
 ```java
 interface I1{
    public void x();
}
interface I2{
    public void z();
}
class A implements I1, I2{
    public void x(){} // I1 인터페이스의 메서드
    public void z(){} // I2 인터페이스의 메서드
}
 ```
 클래스 A와 같이 하나의 클래스는 복수개의 인터페이스를 구현할 수 있으며, **상속과 구별**되는 점이다.

 #### 인터페이스도 상속이 가능하다.
```java
interface I3{
    public void x();
}

interface I4 extends I3{ 
    public void z();
}

class B implements I4{
    public void x(){}
    public void z(){}
}
```
인터페이스 I4는 인터페이스 I3을 상속받는다.

그리고 클래스 B는 인터페이스 I4를 구현한다.

이때 클래스 B는 I4,I3의 메서드를 모두 구현해야한다.

이것을 보면 인터페이스도 **클래스와 마찬가지로 상속을 받을 때 부모 인터페이스가 가진 기능을 지식도 가져간다는 것을 알 수 있다.**

### abstract vs interface
abstract 클래스는 abstract 메서드를 하위클래스가 상속받는 것을 강제한다는 것 외에는 일반 클래스와 같다.

그래서 구체적인 **로직을 가진 일반 메서드와 필드가 존재할 수 있는 형태**이다.

#### 하지만 interface는 구체적인 로직을가진 메서드가 있어서는 안된다.