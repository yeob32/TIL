# Design Pattern

## 생성 패턴

### 팩토리 메서드

- 객체 생성을 공장(Factory) 클래스로 캡슐화 처리하여 대신 생성하게 하는 생성 디자인 패턴
- SRP, OCP 지킬 수 있음

```java
public abstract class UserFactory {
    public User newInstance() {
        User user = createUser();
        user.signup();
        return user;
    }

    protected abstract User createUser();
}

public class NaverUserFactory extends UserFactory {
    @Override
    protected User createUser() {
        return new NaverUser();
    }
}

public class KakaoUserFactory extends UserFactory {
    @Override
    protected User createUser() {
        return new KakaoUser();
    }
}

UserFactory userFactory = new NaverUserFactory();
User user = userFactory.newInstance();

// 위 클라이언트 코드 수정 없이 다른 곳에서 사용 가능
UserFactory kakaoUserFactory = new KakaoUserFactory();
User kakaoUser = kakaoUserFactory.newInstance();
```

**Simple Factory** 의 경우 디자인패턴에 포함되지 않음

- OCP 원칙에 위배됨

```java
public class PetFactory {

    public Pet createPet(Pet.Type petType) {
        switch (petType) {
            case CAT:
                return new Cat();
            case DOG:
                return new Dog();
            default:
                throw new IllegalArgumentException("Pet 타입이 아닙니다");
        }
    }
}
```

### 추상 팩토리

연관성이 있는 **객체 군**이 여러개 있을 경우 이들을 묶어 추상화하고, 어떤 구체적인 상황이 주어지면 팩토리 객체에서 집합으로 묶은 객체 군을 구현화 하는 생성 패턴

```java
interface AbstractProductA {
}

class ConcreteProductA1 implements AbstractProductA {
}

class ConcreteProductA2 implements AbstractProductA {
}

interface AbstractProductB {
}

class ConcreteProductB1 implements AbstractProductB {
}

class ConcreteProductB2 implements AbstractProductB {
}

interface AbstractFactory {
    AbstractProductA createProductA();
    AbstractProductB createProductB();
}

class ConcreteFactory1 implements AbstractFactory {
    public AbstractProductA createProductA() {
        return new ConcreteProductA1();
    }
    public AbstractProductB createProductB() {
        return new ConcreteProductB1();
    }
}

class ConcreteFactory2 implements AbstractFactory {
    public AbstractProductA createProductA() {
        return new ConcreteProductA2();
    }
    public AbstractProductB createProductB() {
        return new ConcreteProductB2();
    }
}
```

### 빌더

복잡한 객체의 생성 과정과 표현 방법을 분리하여 다양한 구성의 인스턴스를 만드는 생성 패턴

```java
class StudentBuilder {
    private int id;
    private String name;
    private String grade;
    private String phoneNumber;

    public StudentBuilder id(int id) {
        this.id = id;
        return this;
    }

    public StudentBuilder name(String name) {
        this.name = name;
        return this;
    }

    public StudentBuilder grade(String grade) {
        this.grade = grade;
        return this;
    }

    public StudentBuilder phoneNumber(String phoneNumber) {
        this.phoneNumber = phoneNumber;
        return this;
    }

		public Student build() {
        return new Student(id, name, grade, phoneNumber);
    }
}
```

### 싱글톤

### 프로토타입

## 구조 패턴

### 어댑터

호환성이 없는 인터페이스 때문에 함께 동작할 수 없는 클래스들을 함께 작동해주도록 변환 역할

- SRP, OCP

```java
class Service {

    void specificMethod(int specialData) {
        System.out.println("기존 서비스 기능 호출 + " + specialData);
    }
}

interface Target {
    void method(int data);
}

class Adapter implements Target {
    Service adaptee;

    Adapter(Service adaptee) {
        this.adaptee = adaptee;
    }

    public void method(int data) {
        adaptee.specificMethod(data);
    }
}

class Client {
    public static void main(String[] args) {
        Target adapter = new Adapter(new Service());
        adapter.method(1);
    }
}
```

### 프록시

대상 원본 객체를 대리하여 대신 처리하게 함으로써 로직의 흐름을 제어

- 보호프록시,로깅프록시,원격프록시,캐싱프록시

```java
class Proxy implements ISubject {
    private RealSubject subject; // 대상 객체를 composition

    Proxy() {
    }

    public void action() {
    	// 프록시 객체는 실제 요청(action(메소드 호출)이 들어 왔을 때 실제 객체를 생성한다.
        if(subject == null){
            subject = new RealSubject();
        }
        subject.action(); // 위임
        /* do something */
        System.out.println("프록시 객체 액션 !!");
    }
}

class Client {
    public static void main(String[] args) {
        ISubject sub = new Proxy();
        sub.action();
    }
}
```

### 데코레이터

대상 객체에 대한 기능 확장이나 변경이 필요할때 객체의 결합을 통해 서브클래싱 대신 쓸수 있는 유연한 대안 구조 패턴

```java
// 원본 객체와 장식된 객체 모두를 묶는 인터페이스
interface IComponent {
    void operation();
}

// 장식될 원본 객체
class ConcreteComponent implements IComponent {
    public void operation() {
    }
}

// 장식자 추상 클래스
abstract class Decorator implements IComponent {
    IComponent wrappee; // 원본 객체를 composition

    Decorator(IComponent component) {
        this.wrappee = component;
    }

    public void operation() {
        wrappee.operation(); // 위임
    }
}

// 장식자 클래스
class ComponentDecorator1 extends Decorator {

    ComponentDecorator1(IComponent component) {
        super(component);
    }

    public void operation() {
        super.operation(); // 원본 객체를 상위 클래스의 위임을 통해 실행하고
        extraOperation(); // 장식 클래스만의 메소드를 실행한다.
    }

    void extraOperation() {
    }
}

class ComponentDecorator2 extends Decorator {

    ComponentDecorator2(IComponent component) {
        super(component);
    }

    public void operation() {
        super.operation(); // 원본 객체를 상위 클래스의 위임을 통해 실행하고
        extraOperation(); // 장식 클래스만의 메소드를 실행한다.
    }

    void extraOperation() {
    }
}

public class Client {
    public static void main(String[] args) {
        // 1. 원본 객체 생성
        IComponent obj = new ConcreteComponent();

        // 2. 장식 1 하기
        IComponent deco1 = new ComponentDecorator1(obj);
        deco1.operation(); // 장식된 객체의 장식된 기능 실행

        // 3. 장식 2 하기
        IComponent deco2 = new ComponentDecorator2(obj);
        deco2.operation(); // 장식된 객체의 장식된 기능 실행

        // 4. 장식 1 + 2 하기
        IComponent deco3 = new ComponentDecorator1(new ComponentDecorator2(obj));
    }
}
```

### 컴포지트

## 행동 패턴

### 전략

실행(런타임) 중에 알고리즘 전략을 선택하여 객체 동작을 실시간으로 바뀌도록 할 수 있게 하는 행위 디자인 패턴

```java
interface IStrategy {
    void doSomething();
}

class ConcreteStrateyA implements IStrategy {
    public void doSomething() {}
}

class ConcreteStrateyB implements IStrategy {
    public void doSomething() {}
}

class Context {
    IStrategy Strategy;
	
    void setStrategy(IStrategy Strategy) {
        this.Strategy = Strategy;
    }
	
    void doSomething() {
        this.Strategy.doSomething();
    }
}

class Client {
    public static void main(String[] args) {
        // 1. 컨텍스트 생성
        Context c = new Context();

        // 2. 전략 설정
        c.setStrategy(new ConcreteStrateyA());

        // 3. 전략 실행
        c.doSomething();

        // 4. 다른 전략 설정
        c.setStrategy(new ConcreteStrateyB());

        // 5. 다른 전략 시행
        c.doSomething();
    }
}
```

### 옵저버

옵저버(관찰자)들이 관찰하고 있는 대상자의 상태가 변화가 있을 때마다 대상자는 직접 목록의 각 관찰자들에게 통지하고, 관찰자들은 알림을 받아 조치를 취하는 행동 패턴

```java
interface ISubject {
    void registerObserver(IObserver o);
    void removeObserver(IObserver o);
    void notifyObserver();
}

class ConcreteSubject implements ISubject {
    List<IObserver> observers = new ArrayList<>();

    @Override
    public void registerObserver(IObserver o) {
        observers.add(o);
        System.out.println(o + " 구독 완료");
    }

    @Override
    public void removeObserver(IObserver o) {
        observers.remove(o);
        System.out.println(o + " 구독 취소");
    }

    @Override
    public void notifyObserver() {
        for(IObserver o : observers) { // 관찰자 리스트를 순회하며
            o.update(); // 위임
        }
    }
}

interface IObserver {
    void update();
}

class ObserverA implements IObserver {
    public void update() {
        System.out.println("ObserverA 한테 이벤트 알림이 왔습니다.");
    }

    public String toString() { return "ObserverA"; }
}

class ObserverB implements IObserver {
    public void update() {
        System.out.println("ObserverB 한테 이벤트 알림이 왔습니다.");
    }

    public String toString() { return "ObserverB"; }
}

public class Client {
    public static void main(String[] args) {

        ISubject publisher = new ConcreteSubject();

        IObserver o1 = new ObserverA();
        IObserver o2 = new ObserverB();
        publisher.registerObserver(o1);
        publisher.registerObserver(o2);

        publisher.notifyObserver();

        publisher.removeObserver(o2);

        publisher.notifyObserver();
    }
}
```

### 템플릿 메서드

### 상태

객체가 특정 상태에 따라 행위를 달리하는 상황에서, 상태를 조건문으로 검사해서 행위를 달리하는 것이 아닌, **상태를 객체화** 하여 상태가 행동을 할 수 있도록 위임하는 패턴

```java
interface AbstractState {
    void requestHandle(Context cxt);
}

class ConcreteStateA implements AbstractState {
    @Override
    public void requestHandle(Context cxt) {}
}

class ConcreteStateB implements AbstractState {
    @Override
    public void requestHandle(Context cxt) {
        // 상태에서 동작을 실행한 후 바로 다른 상태로 바꾸기도 함
        // 예를 들어 전원 on 상태에서 끄기 동작을 실행한후 객체 상태를 전원 off로 변경 하듯이
        cxt.setState(ConcreteStateC.getInstance());
    }
}

class ConcreteStateC implements AbstractState {
    @Override
    public void requestHandle(Context cxt) {}
}

class Context {
    AbstractState state;

    void setState(AbstractState state) {
        this.state = state;
    }

    // 상태에 의존한 처리 메소드로서 state 객체에 처리를 위임함
    void request() {
        state.requestHandle(this);
    }
}

class Client {
    public static void main(String[] args) {
        Context context = new Context();

        // 1. StateA 상태 설정
        context.setState(new ConcreteStateA());

        // 2. 현재 StateA 상태에 맞는 메소드 실행
        context.request();

        // 3. StateB 상태 설정
        context.setState(new ConcreteStateB());

        // 4. StateB 상태에서 또다른 StateC 상태로 변경
        context.request();

        // 5. StateC 상태에 맞는 메소드 실행
        context.request();
    }
}
```

### 커맨드


## References
- https://refactoring.guru/ko/design-patterns