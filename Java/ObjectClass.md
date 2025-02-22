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
**객체가 소멸 전 호출**되는 메소드이다. 하지만 **사용하지 않는 것**을 권장하고 있다.

인스턴스를 만들면 컴퓨터의 **메모리(RAM)가 사용**된다.

그리고 프로그래밍 언어들은 램을 효율적으로 사용하기 위해 **더 이상 사용하지 않는 데이터**를 램에서 **제거**할 수 있는 방법을 제공한다.

java에서는 이러한 방법을 자동으로 해주는 **가비지컬렉션(Garbage collection)**이 있다.

### clone
어떤 객체가 있을 때 그 **객체를 복제**하는 메소드이다.

```java
class Student implements Cloneable{
    String name;
    Student(String name){
        this.name = name;
    }
    protected Object clone() throws CloneNotSupportedException{
        return super.clone();
    }
}
 
class ObjectDemo {
 
    public static void main(String[] args) {
        Student s1 = new Student("egoing");
        try {
            Student s2 = (Student)s1.clone();
            System.out.println(s1.name);
            System.out.println(s2.name);
        } catch (CloneNotSupportedException e) {
            e.printStackTrace();
        }
    }
 
}
```
이 코드에서 인터페이스인 Cloneable은 비어있는 인터페이스이다.

만약 **인터페이스를 구현하지 않고** 클래스에 대한 복제를 시도한다면 **오류**가 발생할 것이다.

그리고 **clone을 통해 복사한 객체**가 필드를 가지고 있을 경우, **필드의 객체는 공유**된다.

만약 clone의 복사보다 더 **정교**하게 구현하고 싶다면, 오버라이딩한 **메소드 clone을 직접 구현**하면 된다.

이 부분은 모든 클래스가 Object 클래스의 메소드인 to String과 clone 등을 사용할 수 있지만,

편의에 맞게 메소드를 새롭게 **재정의해서 사용**할 수 있다는 것이다.