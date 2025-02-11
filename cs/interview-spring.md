<details>
<summary><strong style="font-size:1.17em">
Spring 이란 뭔가요?
</strong></summary>

```text
POJO 프로그래밍을 쉽게 가능하도록 기술적인 기반을 제공하는 프레임워크입니다.
그 기술적인 기반은 IoC/DI, AOP, PSA라는 세 가지 기능 기술을 제공합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
POJO 란 무엇이고, 장점은?
</strong></summary>

```text
객체지향적인 원리에 충실하면서, 환경과 기술에 종속되지않고 
필요에 따라 재활용될 수 있는 방식으로 설계된 오브젝트 입니다.
 
장점은 깔끔한 코드, 테스트에 유리, 객체 지향적인 설계가 가능합니다. 
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
IoC/ DI가 뭐죠?
</strong></summary>

```text
IoC란, 애플리케이션을 구성하는 핵심 오브젝트를 코드가 아닌 외부에서 관리한다는 것입니다. 
즉, 오브젝트의 생명주기를 외부에서 관리합니다.

DI는 외부에서 객체를 생성하여 다른 객체에 주입하는 방식입니다.

그리고 이를 SOLID 관점에서 보면 IoC를 사용하면 객체 생성과 사용의 책임을 분리할 수 있기에 단일책임원칙을 지키며,
DI를 통해 구체적인 구현이 아닌 인터페이스에 의존하는 덕분에 OCP와 DIP를 지키게 됩니다. 

이러한 SOLID 원칙들을 통해 IoC/DI는 코드의 유연성, 재사용성, 테스트 용이성을 크게 향상시키며, 
결과적으로 더 견고하고 유지보수가 쉬운 소프트웨어 구조를 만들 수 있게 합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
Spring IoC 역할은 뭐가 있죠?
</strong></summary>

```text
- 싱글톤 또는 프로토타입 등 다양한 스코프의 객체를 생성하고 관리
- 객체 간의 의존관계를 관리하고 필요한 의존성을 주입합니다.
- AOP 지원
- 국제화 지원
- 리소스 관리
- 이벤트 처리 
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
다양한 스코프에 대해 알려주세요
</strong></summary>

```text
- 싱글톤 스코프는 컨테이너에서 빈 생성시 기본적으로 생성하는 것이 싱글톤 스코프이며, 
스프링 컨테이너의 시작과 종료까지 유지되는 가장 넓은 범위의 스코프 입니다. 즉 컨테이너의 관리를 받습니다.

- 프로토타입 스코프는 요청시 빈 생성과 관계설정, 초기화 콜백 까지만 스프링 컨테이너의 관리를 받고 
요청한 클라이언트에 반환하여 더이상 관리하지 않습니다.

- request 스코프는 웹 요청이 들어오고 나갈 때까지 유지되는 스코프 입니다.
- session 스코프는 웹 세션이 생성되고 종료될 때까지 유지되는 스코프 입니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
기본적으로 생성하는 것이 왜 싱글톤 빈 일까요?
</strong></summary>

```text
웹 상에서 수많은 요청에 대해 항상 빈을 생성하면, 
아무리 가비지 컬렉터가 사용되지 않는 객체를 정리한다고 해도 한계점이 있을 것이고, 
많은 힙 메모리를 잡아먹습니다.  
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
싱글톤 빈의 주의할 점은 뭔가요?
</strong></summary>

```text
멀티스레드 환경에서 해당 빈을 공유하기 때문에, 상태를 가지는 필드를 사용할 때 주의해야 합니다. 
가변(mutable) 상태를 갖지 않도록 설계하는 것이 안전합니다. 
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
수동 빈 등록이 싱글톤 보장될 수 있는 이유
</strong></summary>

```text
스프링에선 @Bean 어노테이션을 사용해서 수동 빈 등록해도 싱글톤으로 등록됩니다. 
하지만, 내부 의존관계를 메소드 호출을 통해 주입하는 경우에 객체가 새로 생성되어 주입되기 때문에 싱글톤이 깨집니다.

이를 해결하기 위해 @Configuration 어노테이션을 통해 싱글톤을 보장할 수 있습니다. 
@Configuration이 적용된 클래스는 CGLIB에 의해 프록시 객체를 만들고, 
이후에 @Bean이 붙어있는 메소드가 컨테이너에 빈으로 등록되어있다면 해당 빈을 가져오고 
없다면 새롭게 등록하고 가져와서 싱글톤을 보장합니다.
```


</details>


---

<details>
<summary><strong style="font-size:1.17em">
프로토타입 빈은 어디에 쓰일까요?
</strong></summary>

```text
상태를 가진 빈이 필요할 때, 사용할 때마다 새로운 인스턴스가 필요할 때 사용합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
싱글톤 빈과 프로토타입 빈을 같이 사용할 때 문제점?
</strong></summary>

```text
싱글톤 코드 안에 프로토타입 빈을 주입하면 프로토타입 빈은 싱글톤 빈이 생성될 때 한 번만 생성되고
 그 이후로는 동일한 인스턴스가 계속 사용됩니다.
이는 프로토타입 빈의 의도한 생명 주기와 다르게 동작할 수 있다는 것입니다. 
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
이 문제를 해결하기 위한 방법
</strong></summary>

```text
ObjectProvider나 JSR330 Provider을 사용해서 DL을 사용합니다.
ScopedProxyMode.TARGET_CLASS 으로 실제 객체 대신 프록시 객체를 주입하고 
실제 요청 시에만 스프링컨테이너에 요청해 새롭게 프로토타입빈을 생성해서 해결합니다. 
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
Request 스코프랑 Session 스코프는 자주 쓰이나요? 어디에 쓰이나요?
</strong></summary>


```text
자주는 쓰이지 않는다고 알고 있습니다.

Request 스코프:
- 각 요청에 대한 로그를 독립적으로 관리
- 요청 처리 중에만 필요한 임시 데이터를 저장할 때 사용됩니다.

Session 스코프:
- 로그인 세션 동안 사용자 정보를 유지할 때 
- 여러 페이지에 걸쳐 사용자의 상태 정보를 유지해야 할 때
- 여러 단계로 이루어진 프로세스(예: 설문조사, 주문 과정)에서 진행 상태를 유지할 때 사용됩니다. 
```




</details>

---

<details>
<summary><strong style="font-size:1.17em">
DI가 뭔가요?
</strong></summary>

```text
외부에서 객체를 생성하여 다른 객체에 주입하는 방식입니다. 
이로써 객체 간의 결합도를 낮추고 코드의 재사용성과 유지보수성을 높입니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
DI 구현 방법을 알려주세요
</strong></summary>

```text
의존성 주입으로는 필드주입, 생성자주입,수정자주입이 있습니다. 
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
DI 방법 중 잘 안쓰는 방법이 있을까요? == DI 방법 중 필드 주입의 문제점과 생성자 주입의 장점
</strong></summary>

```text
필드 주입은 
- final을 사용하지 못해 불변성을 보장받지 못합니다.
- 스프링 컨테이너 말고는 외부에서 주입할 수 있는 방법이 없어 테스트하기 어렵습니다. 
- 순환문제를 미리 잡지못하고 추후 런타임 도중에 순환참조 문제로 스택오버플로우가 발생할 수 있습니다.

수정자 주입은
- 의존성이 변경될 가능성이 있기 때문에 불변성을 확보하기 어렵습니다.
- NullPointerException이 발생할 수 있습니다. 
- 이 역시 순환 참조 문제가 발생할 수 있습니다. 

생성자 주입을 사용하면 
- 필드에 final 키워드를 사용할 수 있습니다. 따라서 의존성을 불변하게 유지할 수 있습니다.
- 테스트코드를 작성하는데 용이합니다. 
- 스프링 애플리케이션 컨텍스트가 띄어질 시점에 순환참조문제를 감지할 수 있습니다. 
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
필드주입에서 final을 왜 사용 못하죠?
</strong></summary>

```text
final을 왜 사용못하면, 인스턴스변수에 final 키워드를 사용하려면 객체 생성과 동시에 반드시 초기화해야하는데, 
필드주입은 객체 생성 후에 리플렉션을 통해 주입됩니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
Autowired 쓰면 안되는 이유
</strong></summary>

```text
- @Autowired를 필드에 직접 사용하면 final 키워드를 사용할 수 없어 불변성을 보장하기 어렵습니다.
- @Autowired를 필드에 사용하면 의존성이 "숨겨져" 클래스의 외부에서 의존성을 파악하기 어렵습니다
- @Autowired로 주입된 의존성은 Spring 컨테이너 없이는 테스트하기 어렵습니다.
- SRP 위반하기 쉽습니다. 생성자는 리펙토링 신호를 보기쉬운데 필드는 발견하기 쉽지 않습니다.
- @Autowired는 스프링 프레임워크에 특화된 애노테이션이라 프레임워크 독립성이 떨어집니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
순환 참조가 뭐죠?
</strong></summary>

```text
A클래스가 B클래스를 의존하는 데, B클래스 역시 A클래스를 의존하는 것을 말합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
순환 참조가 왜 문제가 될까요?
</strong></summary>

```text
예를들어, A클래스의 toString()을 호출할 때 B클래스를 의존하면 B클래스도 출력할테고, 
이때 B클래스에서 A클래스를 의존하면 이게 무한 참조되어 스택오버플로우가 발생합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
왜 필드주입과 수정자주입은 순환참조 문제가 발생할까요?
</strong></summary>


```text
생성자 주입은 빈 인스턴스를 생성하는 과정에서 한번에 관계가 설정되기 때문에 
순환참조 문제가 발생할 경우 바로 예외를 터트리기 때문에 런타임 도중에 문제 생길 일이 없습니다.

하지만, 필드주입과 수정자주입은 먼저 인스턴스부터 생성하고, 관계 설정은 다음단계에 진행됩니다. 
이렇게 단계가 분리되있기 때문에 스프링 빈 생성 단계에서는 발견할 수가 없습니다.  
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
순환 참조 문제를 방지하려면 어떻게 해야할까요?
</strong></summary>


```text
- 의존성을 단방향으로 유지하도록 설계해야 합니다. 
왜냐하면 순환참조문제가 발생하는 이유가 SRP 원칙을 지키지 않기 때문이라고 생각합니다.

- 응용서비스클래스와 같이 공통 기능을 별도의 서비스로 추출합니다.
```


</details>

---

<details>
<summary><strong style="font-size:1.17em">
빈팩토리랑 애플리케이션 컨텍스트의 차이점을 아시나요?
</strong></summary>


```text
빈 팩토리는 빈(Bean)의 생성, 의존성 주입, 초기화,소멸 콜백 등 빈 라이프 사이클 관리의 기능을 제공합니다.

애플리케이션 컨텍스트는 빈 팩토리의 기능을 확장한 컨테이너로서, 빈 팩토리의 모든 기능을 포함하며 추가적인 기능을 제공합니다.
   - 메세지 국제화 기능, 환경변수 처리, 애플리케이션 이벤트, 편리한 리소스 조회
   - 지연로딩, 프로토타입 스코프 기능을 제공하여 더 복잡한 빈 관리 기능
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
빈 라이프 사이클에 대해 설명해 보세요.
</strong></summary>

```text
0. Configuration 이 붙은 클래스들을 식별합니다. 이는 리플렉션을 사용하여 수행되며, Component나 Bean 어노테이션이 붙은 것들을 모두 찾습니다.
1. 빈 정의를 합니다.  
2. 빈 definition을 꺼내서 Bean 범위가 싱글톤인지, 로딩이 지연되지 않는지, FactoryBean이 아닌지를 확인하고 빈을 인스턴스화 합니다.
3. 생성자주입의 경우 빈 인스턴스화하면서 관계가 설정되고, 수정자 주입의 경우 객체 생성 후 별도의 단계로 나눠 의존성을 주입합니다.
4. 생성된 객체를 빈 저장소에 등록하기 직전에 빈 후처리기에 전달합니다.
5. 빈 후처리기 과정에서  
    1. 모든 Advisor 빈 조회
    2. 앞서 조회한 Advisor에 포함되어 있는 포인트컷을 사용해서 해당 객체가 프록시를 적용할 대상인지 아닌지 판단합니다. 
    포인트컷 조건에 하나라도 만족하면 프록시 적용 대상이 됩니다. 
    3. 프록시 적용 대상이면 프록시를 생성하고 반환해서 프록시를 스프링 빈으로 등록합니다. 
    4. 초기화 콜백 메소드 호출
6. 사용
7. 소멸전 콜백메소드 호출 
8. 빈 후처리기 작동
9. 스프링 종료
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
스프링은 왜 객체의 생성과 초기화를 분리시킨건가요? == 초기화,소멸 콜백을 어떨때 사용할 수 있는지
</strong></summary>

```text
생성은 말 그대로 객체 생성에만 집중하고, 

초기화 작업은 보통 외부 커넥션과 연결하는 등 리소스 초기화 작업에 사용하거나, 
로그를 달거나 외부 API에 연결, 
미리 자주쓰는 정보를 캐시에 저장할 때 사용합니다. 
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
DL이 뭔가요?
</strong></summary>

```text
DL은 애플리케이션 코드에서 컨테이너의 API를 직접 사용하여 
필요한 빈(객체)을 검색하는 방법입니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
DL은 주로 어디에 쓰이나요
</strong></summary>

```text
- 런타임에 동적으로 빈을 선택해야 하는 경우에 유용합니다.
- 프로토타입 빈을 생성할 때 주로 DL 방식으로 사용합니다. 
```

</details>


---

<details>
<summary><strong style="font-size:1.17em">
트랜잭션이 뭐죠?
</strong></summary>

```text
트랜잭션이란, 하나 이상의 SQL문을 묶은 작업 단위를 말합니다. 
그리고 이 트랜잭션은 ACID 원칙에 따릅니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
ACID가 뭔가요
</strong></summary>

```text
Atomic인 원자성은 트랜잭션의 모든 연산이 완전히 수행되거나 전혀 수행되지 않아야 합니다.
Consistency인 일관성은 트랜잭션 실행 전후에 데이터베이스가 일관된 상태를 유지해야 합니다.
Isolation인 고립성은 동시에 실행되는 트랜잭션들이 서로 영향을 미치지 않아야 합니다. 이 부분은 ACID 속성 중에서 가장 지키기 어렵습니다
Durability인 지속성은 성공적으로 완료된 트랜잭션의 결과는 영구적으로 반영되어야 합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
Isolation이 왜 지키기 어렵죠?
</strong></summary>

```text
그 이유는 성능과 직접적인 trade-off 관계에 있기 때문입니다. 
완벽한 고립성을 보장하려면 동시성문제를 해결하기 위해
트랜잭션을 하나씩 실행하면
시스템 성능에 부정적인 영향을 미칩니다.
 
그래서 실제 시스템에서는 격리 수준을 조절하여 성능과 
데이터 일관성 사이의 균형을 맞추는 것이 중요합니다.
```

</details>  

---

<details>
<summary><strong style="font-size:1.17em">
트랜잭션 격리 수준에 대해 설명하세요
</strong></summary>

```text
DEFAULT 는 데이터베이스의 기본 격리 수준을 사용합니다.
READ_UNCOMMITTED 는 Dirty Read, Non-Repeatable Read, Phantom Read 문제가 발생할 수 있습니다.
READ_COMMITTED는 Dirty Read 방지, 나머지 두 현상 발생 가능합니다.
REPEATABLE_READ는  Dirty Read와 Non-Repeatable Read 방지, Phantom Read 발생 가능합니다.
SERIALIZABLE는 모든 현상 방지, 그러나 성능 저하가 가장 큽니다. 
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
Dirty Read, Non-Repeatable Read, Phantom Read가 뭐죠?
</strong></summary>

```text
Dirty Reads는 한 트랜잭션이 아직 커밋되지 않은 다른 트랜잭션의 변경사항을 읽는 현상입니다.
Non-Repeatable Read 는 한 트랜잭션 내에서 같은 쿼리를 두 번 실행했을 때 서로 다른 결과를 얻는 현상입니다.
Phantom Read 는 한 트랜잭션 내에서 같은 쿼리를 두 번 실행했을 때, 첫 번째에는 없던 로우가 두 번째에는 나타나는 현상입니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
트랜잭션 전파 옵션에 대해 아는대로 설명하세요
</strong></summary>

```text
REQUIRED는 이미 시작된 트랜잭션에 참여하거나, 없으면 새로 생성해 시작합니다. 즉, 트랜잭션을 하나로 묶습니다
REQUIRES_NEW 인 경우 완전히 독립적인 트랜잭션을 사용합니다. 즉, 독립적으로 커밋하거나 롤백할 수 있습니다.
NESTED 인 경우 내부 트랜잭션이 롤백이 일어나도 외부 트랜잭션에 영향을 주지 않습니다. 그러나 외부 트랜잭션의 커밋과 롤백은 내부 트랜잭션에서도 일어납니다.
SUPPORT 인 경우 현재 진행 중인 트랜잭션이 있으면 그 트랜잭션에 참여합니다. 진행 중인 트랜잭션이 없으면 트랜잭션 없이 실행됩니다.
MANDATORY 인 경우 반드시 기존 트랜잭션 내에서 실행되야 합니다. 만약 진행 중인 트랜잭션이 없으면 예외가 발생합니다.
UNSUPPORTED 경우 항상 트랜잭션 없이 실행됩니다. 기존 트랜잭션이 있다면 그 트랜잭션은 일시 중단됩니다.
NEVER 인 경우 트랜잭션 없이 실행되어야 합니다. 만약 현재 진행 중인 트랜잭션이 있으면 예외가 발생합니다.
```

</details>


---

<details>
<summary><strong style="font-size:1.17em">
ReadOnly가 뭐죠?
</strong></summary>

```text
트랜잭션 읽기 전용으로 성능을 최적화하기 위해 사용됩니다. 
또는 특정 트랜잭션 작업 안에서 쓰기 작업이 일어나는 것을 의도적으로 방지하기 위해 사용합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
ReadOnly가 왜 빠르죠?
</strong></summary>

```text
JPA를 사용한다면 영속성 컨텍스트를 사용하지 않습니다. 
그래서 성능에 영향가는 더티체킹이 없고, 스냅샷을 저장하지 않습니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
프록시 객체가 뭐죠
</strong></summary>

```text
프록시란, 타깃과 동일한 인터페이스를 구현하고 
클라이언트와 타깃 사이에 존재하며 기능의 부가기능을 담당하는 오브젝트 입니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
프록시 객체를 왜 사용하나요
</strong></summary>

```text
- 원본 객체에 대한 코드 수정 없이, 런타임 시점에서 프록시 객체를 통해 부가적인 처리를 추가하기 위해서 입니다.
- 실제 객체의 기능이 반드시 필요한 시점까지 객체의 생성을 미룰수 있습니다.
- 객체에 대한 접근 권한을 제어할 때 사용합니다.
- 실제 객체를 생성하기 이전에 전처리하거나, 기존 객체의 응답을 캐싱할 수 있습니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
JDK 다이나믹프록시와 CGLIB 차이점
</strong></summary>


```text
JDK 다이내믹 프록시는 리플렉션 방식으로 
런타임시점에 타깃객체의 인터페이스를 구현하고 
모든 메소드를 받아 타깃 객체의 메소드가 실행될 수 있도록 위임합니다

CGLIB는 런타임시점에 바이트코드를 조작하여 타깃객체를 상속받은 클래스를 생성합니다. 
이때는 인터페이스 유무가 필요없으며, 
리플렉션 방식도 사용안합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
JDK 다이나믹프록시의 단점이 뭔가요
</strong></summary>

```text
인터페이스를 무조건 사용해야하고, 리플렉션은 성능이 좋지 않습니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
리플렉션이 왜 성능이 안좋죠?
</strong></summary>

```text
리플렉션을 사용하면 JVM이 일반적으로 수행하는 많은 최적화를 적용하기 어려워집니다.
리플렉션을 통한 동적 호출은 CPU 캐시 효율성을 떨어뜨려 캐시미스가 더 자주 발생할 수 있습니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
그럼 CGLIB가 좋은데 그동안 왜 JDK를 썼을가요?
</strong></summary>

```text
오픈소스라 보안면에서 미뤘습니다.
그리고 그전엔 디폴트 생성자가 필요하고 생성자를 2번 호출하는 문제가 있었습니다.
현재는 opensis 라이브러리로 해결하고 spring에서 CGLIB를 디폴트로 채택했습니다. 
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
AOP가 뭐죠?
</strong></summary>

```text
AOP란, 여러 클래스에 걸쳐 있는 공통 관심사를 분리하여 모듈화한 것을 aop라고 합니다.
Spring AOP는 Proxy의 메커니즘을 기반으로 AOP Proxy를 제공하고 있습니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
AOP 용어에 대해 설명해주시죠
</strong></summary>

```text
Aspect: 여러 객체에 걸쳐 있는 공통 관심사를 모듈화한 것
Join Point: aspect가 적용될 수 있는 특정 지점입니다.
Pointcut: Join Point의 부분 집합을 선별하는 표현식으로 어떤 Join Point에 Advice를 적용할지 지정합니다.
Advice: 특정 Join Point에서 Aspect가 취하는 행동입니다. 
Weaving: Pointcut에 의해서 결정된 타겟의 Join Point에 부가기능(Advice)를 삽입하는 과정을 뜻합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
Advice 종류 알려주세요
</strong></summary>

```text
- Before : 메소드 호출 이전에 실행됩니다.
- After: 결과에 관계없이 메서드 호출 이후에 실행됩니다.
- AfterReturning : 메서드가 결과를 반환한 후에 실행되지만 예외가 발생하는 경우에는 실행되지 않습니다.
- Around :  메서드 실행 전후에 로직을 추가할 수 있습니다.
- AfterThrowing : 메서드에서 예외가 발생하면 실행됩니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
PSA가 뭐죠?
</strong></summary>

```text
PSA는 여러 기술들을 추상화시켜 편하게 사용할 수 있도록 합니다.
Spring에서의 PSA는 트랜잭션 추상화, 캐시 추상화, ORM 추상화가 있어 
특정 기술에 종속되지 않고 쉽게 바꿀 수 있습니다.  
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
서블릿과 디스패처 서블릿 차이점
</strong></summary>

```text
- 서블릿: 각 서블릿이 특정 URL 패턴에 매핑되어 해당 요청을 직접 처리합니다.
- 디스패처 서블릿: 모든 요청을 먼저 받아 적절한 핸들러(컨트롤러)에게 위임합니다.

- 서블릿: web.xml 또는 애노테이션을 통해 개별적으로 설정해야 합니다.
- 디스패처 서블릿: 스프링의 설정을 통해 더 유연하게 요청 매핑과 처리를 구성할 수 있습니다.

- 서블릿: 기본적인 요청/응답 처리 기능을 제공합니다.
- 디스패처 서블릿: 요청 전처리, 뷰 리졸빙, 예외 처리 등 추가적인 기능을 제공합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
서블릿과 디스패처 과정의 차이를 말해주세요
</strong></summary>

```text
둘은 처리과정이 다릅니다.

일반 서블릿의 처리 과정은
a. 클라이언트가 HTTP 요청을 보냅니다.
b. 웹 서버가 요청을 받아 서블릿 컨테이너로 전달합니다.
c. 서블릿 컨테이너는 URL 매핑을 확인하여 해당 서블릿을 찾습니다.
d. 서블릿의 service() 메서드가 호출됩니다.
e. HTTP 메서드에 따라 doGet(), doPost() 등의 메서드가 실행됩니다.
f. 서블릿이 직접 비즈니스 로직을 처리하고 응답을 생성합니다.
g. 생성된 응답이 클라이언트에게 반환됩니다.

디스패처 서블릿의 처리 과정은
1. DispatcherServlet의 doService메소드에서 웹 요청 처리가 진행됩니다.이때 HttpServletRequest에 여러 속성들을 넣는 작업을 한 후, doDispatch()를 호출합니다.
2. doDispatch 작업에서는 먼저, getHandler()를 통해 핸들러를 찾습니다.
    1. 이때 핸들러는 6개의 HandlerMappings 중 RequestMappingHandlerMapping 객체를 이용하여 요청에 대한 핸들러를 찾습니다.
    2. 찾은 핸들러를 바로 반환하지 않고, HandlerExecutionChain객체에 담아 리턴하는데, 이때 요청에 대한 interceptor 들이 있다면 함께 담아 리턴합니다. 
3. doDispatch() 내에서 HandlerAdapter 를 찾는 작업을 합니다.
4. 실행될 interceptor들이 있다면 interceptor의 preHandle 메소드를 차례로 실행합니다.
5. HandlerAdapter의 handle()가 실행하는데, 이때 핸들러가 실행됩니다.
    1. 이때, 리플렉션을 통해서 실행되며
    2. argumentResolvers
    3. returnValueHandlers 도 실행됩니다.
6. interceptor의 postHandle 메소드가 실행됩니다.
7. View 객체의 render 메소드가 수행합니다.
8. 응답 객체를 반환합니다.
```

</details>


---

<details>
<summary><strong style="font-size:1.17em">
HandlerMapping과 HandlerAdapter를 분리한 이유가 뭘까요?
</strong></summary>

```text
HandlerMapping은 요청을 적절한 핸들러에 매핑하는 책임만 갖고, 
HandlerAdapter는 매핑된 핸들러를 실행하는 책임만 갖도록 SRP를 지키기 위함입니다.

새로운 유형의 핸들러나 매핑 전략을 추가할 때, 각 컴포넌트를 독립적으로 확장할 수 있습니다. 
예를 들어, 새로운 HandlerMapping을 추가하더라도 기존 HandlerAdapter에는 영향을 주지 않습니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
Rest template이 뭐죠?
</strong></summary>

```text
- 스프링에서 제공하는 HTTP 통신에 유용하게 쓸 수 있는 템플릿

- 다양한 HTTP 메서드(GET, POST, PUT, DELETE 등)를 사용하며 원격 서버와 ‘동기식 방식’으로 
JSON, XML 등의 다양한 데이터 형식으로 통신합니다.

- HTTP 요청 및 응답을 ‘자동’으로 변환하고 역직렬화하는 기능을 제공합니다. 
이를 위해 RestTemplate은 기본적으로 MessageConverter를 사용합니다.

```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
레스트 탬플릿의 다양한 옵션에 대해 아는대로 설명하세요 
</strong></summary>

```text
커넥션 타임아웃 : 클라이언트가 서버에 연결하는데 기다리는 최대 시간
리드 타임아웃 : 서버에서 로직을 수행하는 데 최대시간
소켓 타임아웃 : 각 패킷간의 시간 Gap을 의미 
요청/응답 로깅 설정하기 위에 레스트템플릿의 인터셉터에 적용
일정횟수만큼 요청을 재시도하는 인터셉터 적용
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
소켓 타임아웃은 언제 쓰이죠?
</strong></summary>

```text
대용량 데이터 전송할때

- 큰 파일을 다운로드하거나 스트리밍 데이터를 받을 때 유용합니다.
- 네트워크 상태가 불안정할 때 패킷 손실이 발생할 수 있는 상황에서 사용합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
타임아웃은 왜 필요할까요?
</strong></summary>

```text
응답 시간이 길어지는 연결이 많으면 리소스가 모두 소진되어 장애로 이어질 수 있습니다 
```

</details>


---

<details>
<summary><strong style="font-size:1.17em">
Filter, Interceptor, AOP 차이
</strong></summary>

```text
Filter:
"Filter는 서블릿 컨테이너 레벨에서 작동합니다. 
즉, 스프링의 범위 밖에서 동작합니다. HTTP 요청과 응답을 필터링하고 변경할 수 있어, 
주로 인코딩 변환이나 XSS 방어 등 웹 어플리케이션 전반에 걸친 로직에 사용됩니다. 
모든 요청에 대해 가장 먼저 실행되며, 스프링의 디스패처 서블릿에 도달하기 전에 동작합니다.

Interceptor:
"Interceptor는 스프링 컨텍스트 내부에서 동작합니다. 
디스패처 서블릿이 컨트롤러를 호출하기 전후에 요청과 응답을 가로챕니다. 
주로 인증이나 로깅 등에 사용되며, 스프링 빈을 주입받아 사용할 수 있습니다. 
Filter보다 정교한 처리가 가능하고, 특정 컨트롤러에 대해서만 적용할 수 있는 유연성이 있습니다."

AOP (Aspect-Oriented Programming):
"AOP는 어플리케이션 전반에 걸쳐 사용되는 부가 기능을 모듈화할 수 있게 해줍니다. 
메소드 실행 전후나 예외 발생 시점 등 다양한 시점에 로직을 삽입할 수 있습니다. 
주로 트랜잭션 관리, 로깅, 보안 등 횡단 관심사를 처리하는 데 사용됩니다. 
Filter나 Interceptor와 달리 메소드 레벨에서 동작하여 
더욱 세밀한 제어가 가능합니다."

```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
Filter, Interceptor, AOP 사용시기
</strong></summary>

```text
요청이 들어오면 보통 Request → Filter → Dispatcher Servlet → Interceptor → Controller -> AOP 순으로 처리됩니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
스프링 시큐리티가 뭐죠
</strong></summary>

```text
Spring Security는 Java 애플리케이션에 인증과 권한 부여를 모두 제공하는 데 중점을 둔 프레임워크입니다. 
서블릿 필터 기반의 체인 구조를 사용합니다. 
```


</details>

---

<details>
<summary><strong style="font-size:1.17em">
 스프링 시큐리티는 어떨 때 쓰이나요 
</strong></summary>

```text
- 인증 및 권한 부여
- 세션 고정, 클릭재킹, SQL 인젝션, CSRF 등과 같은 공격으로부터 보호
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
공격에 대해 간단히 설명해보세요
</strong></summary>

```text
세션 고정 (Session Fixation):
세션 고정 공격은 공격자가 사용자의 세션 ID를 미리 결정하거나 알아내어, 사용자가 로그인한 후에도 그 세션을 악용하는 공격입니다.
 
클릭재킹 (Clickjacking):
클릭재킹은 사용자가 의도하지 않은 동작을 수행하도록 속이는 UI 기반 공격입니다. 
주로 투명한 레이어를 이용해 사용자의 클릭을 가로챕니다. 
이를 방지하기 위해 X-Frame-Options 헤더를 사용하여 페이지가 프레임 내에 로드되는 것을 제한할 수 있습니다. 

CSRF (Cross-Site Request Forgery):
CSRF는 앞서 설명한 크로스 사이트 요청 위조의 약자입니다. 
이 공격은 사용자의 브라우저를 이용해 인증된 세션으로 원치 않는 동작을 수행하게 합니다.

SQL 인젝션
악의적인 SQL 구문을 애플리케이션의 입력을 통해 주입하여 
데이터베이스를 비정상적으로 조작하는 공격 기법입니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
인증/인가 과정에 대해 설명해보세요
</strong></summary>

```text
1. 사용자가 로그인 정보와 함께 인증 요청을 합니다.
2. `AuthenticationFilter`가 요청을 가로채고, 가로챈 정보를 통해 `UsernamePasswordAuthenticationToken`의 인증용 객체를 생성합니다.
3. `AuthenticationManager`의 구현체인 `ProviderManager`에게 `UsernamePasswordAuthenticationToken`을 전달합니다.
4. `AuthenticationManager`는 등록된 `AuthenticationProvider`들을 조회하여 인증을 요구합니다.
5. 각 `AuthenticationProvider`는 `UserDetailsService`에 사용자 정보를 넘겨줍니다.
6. `UserDetailsService`는 사용자 정보를 통해 DB에서 찾은 사용자 정보를 `UserDetails` 객체로 만듭니다.
7. `AuthenticationProvider`는 `UserDetails`를 넘겨받고 요청한 사용자정보와 비교합니다.
8. 인증이 완료되면, 권한등의 사용자정보를 담은 `Authentication` 객체를 반환합니다.
9. `AuthenticationFilter`는 이 `Authentication` 객체를 받고 `SecurityContext`에 저장합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
인증과 인가 차이
</strong></summary>

```text
인증
- 식별 가능한 정보로 서비스에 등록된 사용자의 신원과 일치하는지 입증하는 과정입니다.

인가
- 인증된 사용자에 대해 특정 자원의 접근 권한을 확인하는 과정
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
SecurityContext 란?
</strong></summary>

```text
Authentication가 저장되는 저장소이며, 
일반적으로 ThreadLocal 에 저장되며 덕분에 전역적으로 SecurityContext 접근 가능합니다.
```

</details>

---

## 스프링부트

---

<details>
<summary><strong style="font-size:1.17em">
MVC 패턴이 뭐죠?
</strong></summary>


```text
애플리케이션을 세 가지 주요 구성 요소로 나누어 설계하는 방법입니다
Model (모델) 역할: 데이터와 관련된 로직을 처리합니다.

View (뷰) 
역할: 사용자에게 보여지는 화면을 담당합니다. 
사용자 인터페이스(UI)를 구성하고, Model에서 가져온 데이터를 화면에 적절히 렌더링하는 역할을 합니다

Controller (컨트롤러)
역할: 사용자의 입력을 처리하고, 이를 해석하여 Model과 View 사이를 연결하는 중재자 역할을 합니다.

```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
Spring SpringBOot 차이점
</strong></summary>

```text
Spring은 IoC/DI, AOP, 빈관리 등 핵심 기능을 제공하고 메시지 국제화, 환경변수, PSA 기술로 트랜잭션관리, JPA등을 지원합니다.

SpringBoot는 Spring 기반 애플리케이션을 더 쉽게 만들고 설정할 수 있도록 돕는 프레임워크입니다.
Auto-Configuration으로 설정을 자동 구성하고
스타터 패키지를 제공해 의존성들을 한번에 포함할 수 있습니다.
또한 톰켓이 내장되어있습니다. 
마지막으로 YAML이나 application.properties 파일로 대부분의 설정을 처리할수있습니다.
```

</details>
