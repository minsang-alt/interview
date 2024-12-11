
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