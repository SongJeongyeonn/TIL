## 제어 역전(IoC)
객체를 생성하고 사용하는 일련의 작업을 **개발자가 직접 제어**하는 구조이다.

사용하는 객체를 선언 후 해당 객체의 의존성을 생성해 객체에서 제공하는 기능을 사용합니다.
```
@RestController
public class NoDIController {

    private MyService service = new MyServiceImpl(); // 객체 생성

    @GetMapping("/no-di/hello")
    public String getHello() {
        return service.getHello();
    }

}
```
하지만 IoC를 적용한 환경은 기존 자바 개발방식과 다르게 동작합니다.

사용할 객체를 직접 생성하지 않고, 객체의 생명주기 관리를 외부(스프링 컨테이너, IoC컨테이너)에 위임하기에
**객체의 관리를 컨테이너에 맏기는 제어역전**이 일어납니다. 그래서 **제어 역전을 통한 의존성 주입(DI), 관점 지향 프로그래밍(AOP) 등이 가능**해집니다.
## 의존성 주입(DI)
의전성 주입은 제어 역전 방법 중 하나로, 사용할 **객체를 직접 생성하지 않고 외부 컨테이너가 생성한 객체를 주입받아 사용**하는 방식을 의미합니다.

#### 의존성을 주입하는 3가지 방법
- 생성자를 통한 의존성 주입
- 필드 객체 선언을 통한 의존성 주입
- setter 메서드를 통한 의존성 주입

스프링에서 @Autowired 어노테이션을 통해 의존성을 주입할 수 있습니다.
하지만 스프링 4.3 이후에는 @Autowired을 생략할 수 있지만, 가독성을 위해 명시하는 것을 권장합니다.
```
@RestController
public class DIController {

    MyService myService;

    @Autowired
    public DIController(MyService myService) {
        this.myService = myService; // 생성자를 통한 의존성 주입
    }

    @GetMapping("/di/hello")
    public String getHello() {
        return myService.getHello();
    }

}

```
```
@RestController
public class FieldInjectionController {

    @Autowired
    private MyService myService; // 필드를 통한 의존성 주입

}

```
```
@RestController
public class SetterInjectionController {

    MyService myService;

    @Autowired
    public void setMyService(MyService myService) { // setter 메서드를 통한 의존성 주입
        this.myService = myService;
    }

}
```
주로 쓰이는 의존성 주입 방법은 생성자를 통해 의존성을 주입받는 방식입니다.

다른 방식과는 달리 레퍼런스 객체 없이는 객체를 초기화할 수 없게 설계할 수 있기 때문입니다.

## 관점 지향 프로그래밍(AOP)
스프링의 아주 중요한 특징으로, 객체지향 프로그래밍(OOP)이 있습니다. AOP는 OOP를 잘 사용하도록 돕는 개념입니다.
#### 객체지향 프로그래밍의 특징
① 추상화  ② 캡슐화  ③ 상속  ④ 다형성
AOP는 **관점을 기준으로 묶어 개발하는 방식**입니다. 여기서 관점은 어떤 기능을 구현할 때 **핵심기능과 부가기능**으로 구분해 **각각을 하나의 관점으로 보는 것**을 의미합니다.

**핵심기능**은 비즈니스 로직을 구현하는 과정에서 로직이 처리하려는 목적 기능을 말합니다.

예를 들어 클라이언트로부터 상품 정보를 받아 데이터베이스에 저장하고 그 상품 정보를 조회하는 비즈니스 로직을 구현한다고 했을 때,

1. 상품 정보를 데이터베이스에 저장  2. 저장된 상품 정보 데이터를 보여주기 이렇게가 **핵심 기능**입니다.

실제 애플리케이션을 개발할 때는 핵심기능에 **부가 기능**을 추가해야할 상황이 생긴다. 핵심 기능인 **비즈니스 로직 사이에 로깅을 처리하거나 트랜잭션을 처리하는 코드**가 그 예시 입니다.