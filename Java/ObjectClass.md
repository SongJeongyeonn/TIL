# Object Class
#### 모든 클래스의 조상이다.

## 상속
상속은 자바에서 필수적인 요소로, 상속을 명시하지 않아도 **기본적인(Object) 상속**을 하게 된다.
```java
class O {} // class O extends Object {}
```
위의 코드는 주석 같은 코드로, **명시하지 않아도 Object 클래스를 상속**하고있다.

Object 클래스는 자바의 **모든 클래스들이 상속받기에 모든 클래스들의 조상**이라 할 수 있다.

## Object Class가 가진 다양한 메소드들
다음 [문서](https://docs.oracle.com/javase/7/docs/api/java/lang/Object.html)를 보면 Object에 담긴 다양한 메소드들과 Object 클래스에 대해 자세히 확인할 수 있다.

이 중에서 자주 사용되는 4개의 메소드들에 대해 자세히 살펴보겠다.

### toString
**객체를 문자로 표현**하는 메소드이다.
```java
Calculator c1 = new Calculator(); // 또한 Calculator 클래스는 Object 클래스를 참조하고 있기에 toString을 사용할 수 있다.
c1.setOprands(10, 20);
System.out.println(c1); // System.out.println(c1.toString());
```
위의 코드의 println문에서 **c1**은 **c1.toString**과 **같은 결과**를 보여준다.

그 이유는 toString을 **명시적으로 적지 않아도 System.out.println에서 자동으로 호출**하고 있기 때문이다.

### equals
**객체와 객체가 같은지 비교**하는 메소드이다.
```java
Student s1 = new Student("egoing");
Student s2 = new Student("egoing");
System.out.println(s1 == s2); // 겉(내용)만 비교
System.out.println(s1.equals(s2)); // 본질(객체)을 비교
```
s1과 s2는 서로 **다른 객체**이며 **논리적으로는** "egoing"이라는 **같은 값**을 가지고 있기 때문에

**'=='** 로 비교하였을 때는 **true**가 나오고, **'equals'** 로 비교하였을 때는 **false**가 나온다.

**equals**는 **접근제어자는 public**이며, **반환타입은 불리안**이라는 특징을 가지고 있다.

### finalize
**객체가 소멸 전 호출**되는 메소드이다.


### clone
어떤 객체가 있을 때 그 **객체를 복제**하는 메소드이다.

