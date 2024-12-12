
---

<details>
<summary><strong style="font-size:1.17em">
## 커맨드 패턴 (Command Pattern)
</strong></summary>

기존에는 예를들어, 버튼을 눌렀을 때 램프를 키거나 또는 알람을 동작하는 등의 기능이 추가될때마다
버튼의 클래스를 수정하게 되며 OCP를 위반합니다. 특히 Button 클래스가 점점 복잡해짐에 따라
실수도 할 수 있고, 기존 코드가 점점 복잡해집니다.

이를 해결하기 위해, 커맨드 패턴을 사용합니다. 커맨드 패턴은 수행될 기능을 캡슐화해서 버튼같은경우
램프를 키는 행위의 커멘드, 알람을 울리는 행위의 커멘드를 만들어서 버튼에게 전달합니다. 버튼은
인터페이스인 커멘드를 통해 기능을 수행하게 됩니다.

그리고 이러한 버튼을 Invoker, 커멘드를 Command, 
실제로 명령을 받아다 수행하는 램프나 알람을 Receiver라고 합니다.

커맨드패턴의 장점은
1. 요청을 캡슐화할수있습니다.
2. 요청을 큐에 넣거나 로깅, 되돌리기 등을 할 수 있습니다.
3. 클라이언트의 코드와 요청을 처리하는 수신자(리시버)간의 결합도를 낮출수있습니다.
4. 새로운 종류의 요청이나 명령을 쉽게 추가할 수 있는 확장성이 있습니다.

단점은
1. 클래스의 수가 늘어난다는 점입니다. 이는 과도한 추상화로 인해 디버깅이 어렵고,메모리사용량이 증가되고, 
2. 복잡성이 증가합니다.

주로 사용되는 곳은 
"리모컨으로 TV, 불, 에어컨 등을 제어하는 것처럼, 하나의 버튼으로 다양한 기능을 실행할 때 사용하는 패턴"
2. GUI의 버튼, 메뉴 (클릭 시 다양한 동작 실행)
3. 텍스트 에디터의 실행취소/다시실행 기능
4. 게임의 키보드 설정 (같은 키에 다른 동작 매핑)
5. 작업 스케줄러 (특정 시간에 다양한 작업 실행)

```java
// 1. 버튼이 수행할 수 있는 동작을 정의
interface Command {
    void execute();
}

// 2. 각각의 동작을 별도 클래스로 만듦
class TurnOnTVCommand implements Command {
    void execute() {
        tv.turnOn();  // TV 켜기
    }
}

class TurnOnLightCommand implements Command {
    void execute() {
        light.turnOn();  // 불 켜기
    }
}

// 3. 버튼은 단순히 명령을 실행하기만 함
class Button {
    private Command command;
    
    void setCommand(Command command) {
        this.command = command;
    }
    
    void press() {
        command.execute();  // 어떤 명령이든 실행만 하면 됨
    }
}

// 4. 사용할 때
Button button = new Button();
button.setCommand(new TurnOnTVCommand());  // TV 켜는 버튼
button.press();  // TV 켜기

button.setCommand(new TurnOnLightCommand());  // 불 켜는 버튼으로 변경
button.press();  // 불 켜기
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">## 옵서버 패턴 (Observer Pattern)</strong></summary>


옵서버패턴은 한 객체의 상태 변화를 다른 객체들에게 자동으로 
알려주는 패턴입니다. 이를 발행-구독 패턴이라고도 합니다.
이때 subject 인터페이스나 추상클래스로 발행자를 구현하고, observer 인터페이스로 구독자를 구현합니다.

옵서버패턴의 장점은
느슨한 결합으로 Subject와 Observer는 서로 독립적으로 변경될 수 있습니다.
Subject의 상태가 변경되면 모든 Observer에게 자동으로 알림이 갑니다
새로운 Observer를 쉽게 추가하거나 제거할 수 있습니다.
여러 종류의 옵서버를 만들수있어, 다양한 방식으로 옵서버의 상태변화를 처리할 수 있습니다.

단점은
주체와 옵서버 관계를 잘못설정하면 순환참조가 발생할 수 있습니다.
모든 옵서버에게 알림을 가게하면서 성능저하가 발생할 수 있습니다.

```java
// Subject 인터페이스
interface Subject {
    void attach(Observer observer);
    void detach(Observer observer);
    void notifyObservers();
}

// Observer 인터페이스
interface Observer {
    void update(String message);
}

// 구체적인 Subject 구현
class NewsAgency implements Subject {
    private List<Observer> observers = new ArrayList<>();
    private String news;

    @Override
    public void attach(Observer observer) {
        observers.add(observer);
    }

    @Override
    public void detach(Observer observer) {
        observers.remove(observer);
    }

    @Override
    public void notifyObservers() {
        for (Observer observer : observers) {
            observer.update(news);
        }
    }

    // 뉴스를 설정하고 옵서버들에게 알림
    public void setNews(String news) {
        this.news = news;
        notifyObservers();
    }
}

// 구체적인 Observer 구현
class NewsChannel implements Observer {
    private String name;

    public NewsChannel(String name) {
        this.name = name;
    }

    @Override
    public void update(String news) {
        System.out.println(name + "이(가) 뉴스를 받았습니다: " + news);
    }
}

---

Subject newsAgency = new NewsAgency();
Observer channel1 = new NewsChannel("채널1");
Observer channel2 = new NewsChannel("채널2");

newsAgency.attach(channel1);
newsAgency.attach(channel2);

((NewsAgency) newsAgency).setNews("중요한 뉴스가 발생했습니다!");
```





</details>


---

<details>
<summary><strong style="font-size:1.17em">## 데코레이터 패턴 (decorator pattern) </strong></summary>

여러 기능을 상황에 맞게 조합하여 그때마다 다르게 실행할 수 있도록 하는 패턴입니다.

장점은
객체에 동적으로 기능을 추가할 수 있고,
유연하게 기능을 조합할 수 있으며
단일 책임원칙과 기존코드 수정없이 확장이 가능합니다.

단점은
객체 생성이 복잡해지며, 객체 식별이 어렵습니다.
데코레이터 관리가 어렵습니다.

```java
public abstract Display{
    public abstract void draw();
}

// 기본 도로 표시 클래스
public class RoadDisplay extends Display{
    public void draw(){
        System.out.println("도로 기본 표시");
    }
}

// 다양한 추가 기능에 대한 공통 클래스
public class DisplayDecorator extends Display{
    private Display decoratedDisplay;
    
    public DisplayDecorator(Display decoratedDisplay){
        this.decoratedDisplay = decoratedDisplay;
    }
    
    public void draw(){
        decoratedDisplay.draw();
    }
}

public class LaneDecorator extends DisplayDecorator{
    public LaneDecorator(Display decoratedDisplay){
        super(decoratedDisplay);
    }
    
    public void draw(){
        super.draw();
        drawLane();
    }
    
    private void drawLane() {System.out.println("차선 표시");}
}


public class TrafficDecorator extends DisplayDecorator{
    public TrafficDecorator(Display decoratedDisplay){
        super(decoratedDisplay);
    }
    
    public void draw(){
        super.draw();
        drawTraffic();
    }
    
    private void drawTraffic(){System.out.printlnn("교통량 표시")}
}


public class Client{
    public static void main(String[] args){
        Display road = new RoadDisplay();
        road.draw();
        
        Display roadWithLane = new LaneDecorator(new RoadDisplay());
        roadWithLane.draw();
        
        Display roadWithTraffic = new TrafficDecorator(new RoadDisplay());
        roadWithTraffic.draw();
    }
}
```

2번째 예시

```java
// Component (원본 객체와 장식된 객체 모두를 묶는 역할)
abstract class Pizza{
    protected String description = "Original Pizza";
    
    public String getDescription(){
        return description;
    }
    
    public abstract int getCost();
}

// ConcreteComponent(원본 객체, 데코레이팅 할 객체)
class CheesePizza extends Pizza{
    public CheesePizza(){
        this.description = "CheesePizza";
    }
    
    @Override
    public ing getCost(){
        return 1000;
    }
}

class CombinationPizza extends Pizza{
    public CombinationPizza(){
        this.description = "Combination Pizza";
    }
    
    @Override
    public int getCost(){
        return 120000;
    }
}


// decorator
abstract class ToppingDecorator extends Pizza{
    protected Pizza pizza;
    
    ToppingDecorator(final Pizza pizza){
        this.pizza = pizza;
    }
    
    public abstract String getDescription();
}


// concrete decorator
class FreshTomato extends ToppingDecorator{
    public FreshTomato(final Pizza pizza){
        super(pizza);
    }
    
    @Override
    public String getDescription(){
        return pizza.description + "with FreshTomato";
    }
    
    @Override
    public int getCost(){
        return 300+pizza.getCost();
    }
}
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">## 템플릿 메서드 패턴 (template method pattern) </strong></summary>

전체적으로 동일하면서 부분적으로 상이한 문장을 가진 메소드에 대해서
하위 클래스에서 구현할 수 있도록 하는 패턴입니다.

주요 특징은
1. 변하지 않는 부분은 상위 클래스에 두고, 변하는 부분은 하위 클래스에서 구현합니다.
2. 알고리즘의 뼈대는 고정되어 있지만, 세부 구현은 하위 클래스마다 다르게 할 수 있습니다.
3. 코드 재사용성을 높이고 중복을 줄일 수 있습니다.

단점은
하위클래스가 너무 많은 책임을 맡게되고, 상위클래스의 복잡성이 증가합니다.


```java
// 추상 클래스
public abstract class 음료 {
    // 템플릿 메서드
    public final void 음료만들기() {
        물끓이기();
        우려내기();  // 하위 클래스에서 구현
        컵에따르기();
        if (고객이첨가물을원하는가()) {
            첨가물추가하기();  // 하위 클래스에서 구현
        }
    }

    protected abstract void 우려내기();
    protected abstract void 첨가물추가하기();

    private void 물끓이기() {
        System.out.println("물을 끓입니다.");
    }

    private void 컵에따르기() {
        System.out.println("컵에 따릅니다.");
    }

    private boolean 고객이첨가물을원하는가() {
        return true;
    }
}

// 구체 클래스
public class 커피 extends 음료 {
    void 우려내기() {
        System.out.println("커피를 우려냅니다.");
    }

    void 첨가물추가하기() {
        System.out.println("설탕과 우유를 추가합니다.");
    }
}

class 차 extends 음료 {
    void 우려내기() {
        System.out.println("차를 우려냅니다.");
    }

    void 첨가물추가하기() {
        System.out.println("레몬을 추가합니다.");
    }
}
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">## 팩토리 메서드 패턴 (factory method pattern) </strong></summary>

팩토리 메소드 패턴(Factory Method Pattern)은 객체 생성을 직접 하지 않고 
팩토리 클래스를 통해 객체를 생성하는 디자인 패턴입니다

장점은
객체 생성 로직을 한 곳에서 관리할 수 있어 코드 유지보수가 쉬워집니다.
실제 구현 클래스를 감추고 인터페이스를 통해 접근하므로, 시스템이 확장에는 열려있고 변경에는 닫혀있게 됩니다.
코드 재사용: 객체 생성 로직을 재사용할 수 있습니다.

스프링에선
BeanFactory가 Creator 인터페이스이고,
이를 구현한 AnnotationConfigApplicationContext,
Product 는 Object 타입이고 
이를 넘겨 받는 인스턴스가 ConcreateProduct

자바에선
Calendar의 getInstance()

```java
abstract class AnimalFactory {
    abstract Animal createAnimal();  // 팩토리 메소드
    
    // 템플릿 메소드처럼 사용할 수도 있습니다
    public void makeAnimalSound() {
        Animal animal = createAnimal();
        animal.sound();
    }
}

// 구체적인 팩토리 클래스들
class DogFactory extends AnimalFactory {
    @Override
    Animal createAnimal() {
        return new Dog();
    }
}

class CatFactory extends AnimalFactory {
    @Override
    Animal createAnimal() {
        return new Cat();
    }
}


interface Animal {
    void sound();
}

// 구체적인 제품 클래스들
class Dog implements Animal {
    @Override
    public void sound() {
        System.out.println("멍멍!");
    }
}

class Cat implements Animal {
    @Override
    public void sound() {
        System.out.println("야옹!");
    }
}

```

</details>

---

<details>
<summary><strong style="font-size:1.17em">## 추상 팩토리 패턴 (abstract factory pattern) </strong></summary>

연관된 여러 객체들을 일관된 방식으로 생성할 때 사용하는 패턴입니다.
관련된 객체들이 함께 사용되어야 할 때와
시스템이 여러 제품군 중 하나를 선택해서 사용해야 할 때 유용합니다.

```java
// 제품군 인터페이스들
interface Button {
    void render();
}

interface Checkbox {
    void toggle();
}

// 구체적인 제품들 - Light 테마
class LightButton implements Button {
    public void render() {
        System.out.println("밝은 테마 버튼을 그립니다");
    }
}

class LightCheckbox implements Checkbox {
    public void toggle() {
        System.out.println("밝은 테마 체크박스를 토글합니다");
    }
}

// 구체적인 제품들 - Dark 테마
class DarkButton implements Button {
    public void render() {
        System.out.println("어두운 테마 버튼을 그립니다");
    }
}

class DarkCheckbox implements Checkbox {
    public void toggle() {
        System.out.println("어두운 테마 체크박스를 토글합니다");
    }
}

// 추상 팩토리
interface UIFactory {
    Button createButton();
    Checkbox createCheckbox();
}

// 구체적인 팩토리들
class LightThemeFactory implements UIFactory {
    public Button createButton() {
        return new LightButton();
    }
    
    public Checkbox createCheckbox() {
        return new LightCheckbox();
    }
}

class DarkThemeFactory implements UIFactory {
    public Button createButton() {
        return new DarkButton();
    }
    
    public Checkbox createCheckbox() {
        return new DarkCheckbox();
    }
}


public class Application {
    private Button button;
    private Checkbox checkbox;

    public Application(UIFactory factory) {
        button = factory.createButton();
        checkbox = factory.createCheckbox();
    }

    public void createUI() {
        button.render();
        checkbox.toggle();
    }
}

// 메인에서 사용
public static void main(String[] args) {
    // 라이트 테마 사용
    Application app1 = new Application(new LightThemeFactory());
    app1.createUI();

    // 다크 테마 사용
    Application app2 = new Application(new DarkThemeFactory());
    app2.createUI();
}
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">## 컴퍼지트 패턴 (composite pattern) </strong></summary>

컴포지트 패턴은 부분-전체의 관계를
트리 구조로 구성하여 단일 객체와 복합 객체를 동일하게 다룰 수 있게 하는 패턴입니다

장점은
일관된 처리: 단일 객체(File)와 복합 객체(Directory)를 동일한 방식으로 처리
재귀적 구조: 트리 구조를 쉽게 구현할 수 있음
확장성: 새로운 종류의 컴포넌트를 쉽게 추가 가능

```java
// Component: 파일과 디렉토리의 공통 인터페이스
interface FileSystem {
    void display(String indent);
    int getSize();
}

// Leaf: 파일 (단일 객체)
class File implements FileSystem {
    private String name;
    private int size;

    public File(String name, int size) {
        this.name = name;
        this.size = size;
    }

    public void display(String indent) {
        System.out.println(indent + "📄 " + name + " (" + size + "kb)");
    }

    public int getSize() {
        return size;
    }
}

// Composite: 디렉토리 (복합 객체)
class Directory implements FileSystem {
    private String name;
    private List<FileSystem> contents = new ArrayList<>();

    public Directory(String name) {
        this.name = name;
    }

    public void add(FileSystem file) {
        contents.add(file);
    }

    public void display(String indent) {
        System.out.println(indent + "📁 " + name);
        for(FileSystem file : contents) {
            file.display(indent + "  ");
        }
    }

    public int getSize() {
        int totalSize = 0;
        for(FileSystem file : contents) {
            totalSize += file.getSize();
        }
        return totalSize;
    }
}


public class Main {
    public static void main(String[] args) {
        Directory root = new Directory("루트");

        // 문서 폴더
        Directory docs = new Directory("문서");
        docs.add(new File("이력서.doc", 50));
        docs.add(new File("발표자료.ppt", 2048));

        // 사진 폴더
        Directory photos = new Directory("사진");
        photos.add(new File("여행.jpg", 4096));
        Directory subPhotos = new Directory("가족사진");
        subPhotos.add(new File("생일.jpg", 2048));
        photos.add(subPhotos);

        root.add(docs);
        root.add(photos);

        // 전체 구조 출력
        root.display("");
        // 전체 크기 계산
        System.out.println("총 크기: " + root.getSize() + "kb");
    }
}
```

</details>

