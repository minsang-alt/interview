## Java

## 객체지향

---

<details>
<summary><strong style="font-size:1.17em">
객체지향이 뭔가요?
</strong></summary>

```text
주변에서 볼 수 있는 사물의 속성과 기능을 모두 포함된 객체로 만듭니다. 
그리고 객체지향에서는 이렇게 만들어진 객체들 간의 결합과 조합을 통해 
하나의 프로그램을 만드는 패러다임을 말합니다.

그리고 이런 객체지향을 사용하는 이유는 
캡슐화, 상속화, 추상화, 다형성을 특징으로 인해 
코드의 재사용을 늘리고, 변경을 쉽게 할 수 있습니다. 
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
이렇게 코드의 재사용성과 변경을 쉽게 하는게 왜 중요한가요?
</strong></summary>

```text
재사용성을 늘릴 수 있다는 것은 코드 양을 줄여 
복잡도를 낮추고 이로써 개발자가 실수할 일이 줄어듭니다.

또한, 변경이 쉬우면 개발이 확장되고, 집중하고 있는 부분만 수정하면 되기 때문에 
이 또한, 복잡도를 낮추고 개발자가 실수할 일이 줄어들며
결과적으로 유지보수를 어렵게하지 않으며, 
쓸데없는 시간과 비용을 낭비하지 않습니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
객체지향의 4가지 특징을 말해주세요
</strong></summary>

```text
- 캡슐화는 속성과 행위를 하나로 묶고 구현 내용을 외부에 감춘다는 것입니다. 
  
- 상속은 기존의 클래스를 재활용해서 새로운 클래스를 작성하고 기능을 확장할 수 있게 합니다.

- 추상화는 객체들의 공통적인 속성과 기능을 추출하여 정의하는 것을 말합니다. 
그리고 이 추상화를 구현할 수 있는 방법은 추상클래스와 인터페이스가 있습니다.

- 다형성은 오버로딩, 오버라이딩, 함수형 인터페이스와 같이 
같은 이름으로 여러 형태를 처리할 수 있는 능력을 말합니다. 
즉, 같은 메서드 호출이지만, 상황에 따라 다르게 동작하는 것을 말합니다 
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
오버라이딩과 오버로딩을 프로젝트에 많이 쓰나요
</strong></summary>

```text
오버라이딩은 인터페이스를 정의하고 구현하는 과정에서 많이 쓰고, 
오버로딩은 생성자 오버로딩을 많이 씁니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
오버로딩 단점이 뭘까요? 다형성이 주는 장점은 지금 말했다. 단점은 뭐가 있어요
</strong></summary>

```text
단점은 복잡성이 증가한다는 점입니다. 
동일한 이름의 메서드나 연산자를 사용하기 때문에 코드를 이해하기 어렵습니다
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
객체지향 특징중 중요하다 느끼는게 뭔가요?
</strong></summary>

```text
캡슐화가 중요하다고 느낍니다.

내부의 상태가 다른 클래스들에 의해 변경되면 
유지보수면에서 어렵고 단일책임원칙인 SRP도 쉽게 깨집니다.  
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
이러한 4가지 특성을 효과적으로 활용한 설계기법을 말해주세요
</strong></summary>


```text
SOLID는 객체 지향 프로그래밍 및 설계의 다섯 가지 기본 원칙이며, 
디자인 패턴은 더 특정한 상황에 적용될 수 있는 설계 기법입니다.

- 먼저, 단일책임원칙인 SRP 는 한 클래스에 하나의 책임만 가져야 한다는 원칙입니다.

실제로, 제가 한 프로젝트에서 
초기에는 Task 클래스가 작업 정보 관리, 상태 변경, 담당자 할당 등 모든 기능을 담당했습니다. 
Task, TaskStatus, TaskAssignment 클래스로 분리하여
 각 클래스가 단일 책임을 갖도록 리팩토링했습니다.


- 개방폐쇄원칙인 OCP 는 한 클래스의 변경은 최소화하면서, 확장에는 열려있게 해야합니다.

실제로, 새로운 작업 유형을 만들기 위해 예를들면 버그유형, 디자인유형 등을 추가할 때마다 
기존 코드를 수정해야 했습니다.
그것을 리팩토링하여 TaskType 인터페이스를 만들고, 
각 작업 유형을 구현 클래스로 만들었습니다.

- 리스코프치환원칙인 LSP 는 서브타입은 언제나 자신의 기반 타입으로 교체할 수 있어야 합니다.
 그리고 하위 클래스의 인스턴스는 상위 클래스의 인스턴스 역할을 수행하는데 문제가 없어야 합니다.

예를들어, 포유류라는 부모클래스로 오리너구리라는 자식클래스는 
새끼가 아닌 알을 낳기 때문에 부모클래스로 대체할 수 없어 부적절한 방식입니다.

- 인터페이스 분리 원칙 ISP 는 SRP와 비슷하며, 
특정 클라이언트를 위한 인터페이스 여러 개가 
기능 여러개 갖고 있는 범용 인터페이스 하나보다 낫습니다.

- 의존관계 역전 원칙인 DIP 는 상위 모듈(정책 결정)은 하위 모듈(세부 사항)에 의존하지 않아야 합니다. 
대신, 상위와 하위 모듈 모두 추상화에 의존해야 합니다
```

</details>

---

## 추상클래스,인터페이스

---

<details>
<summary><strong style="font-size:1.17em">
추상 클래스와 인터페이스의 차이를 말씀해주세요
</strong></summary>

```text
추상클래스란, 클래스 내 추상메소드가 하나 이상 포함되어 있거나, 
abstract로 정의된 경우를 말합니다.

인터페이스 역시 추상메소드와 default 키워드를 통한 일반 메소드 구현이 가능하지만, 
결정적 차이점은 인터페이스에서는 상수를 제외한 변수를 선언할 수 없습니다.

보통 추상클래스는 기능확장을 위해 사용되며, 오직 하나의 클래스만을 상속받을 수 있습니다.
반면, 인터페이스는 인터페이스에 정의된 추상메서드 내용이 반드시 구현클래스에서 구현해야합니다. 
즉, 해당 인터페이스를 구현한 객체들에 대해서 일관된 동작을 보장합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
마커 인터페이스라는 것을 혹시 아시나요
</strong></summary>

```text
자바의 마커인터페이스는 일반적인 인터페이스와 동일하지만, 
어떠한 메소드를 포함하지 않은 인터페이스입니다.

이러한 마커인터페이스는 컴파일러나 JVM에게 
추가적인 정보를 제공하기 위해 사용됩니다.

예를들어, Serializable 인터페이스가 있는데, 
Serializable 인터페이스를 구현하지 않은 클래스의 객체를 직렬화하려고 시도하면, 
컴파일 타임에 타입 체크를 통해 NotSerializableException이 발생합니다. 
```

</details>


---

<details>
<summary><strong style="font-size:1.17em">
Serialization이 뭔가요?
</strong></summary>

```text
직역하면 직렬화라고 부릅니다. 
이 직렬화는 객체의 상태를 바이트 스트림으로 변환합니다. 
반대는 역직렬화라고 합니다.

이러한 직렬화가 필요한 이유는 자바의 객체를 데이터베이스 또는 파일에 저장하거나 
네트워크를 통해 전송하기 위해 바이트 스트림으로 변환하는 것 입니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
transient 키워드를 알고 있나요? 이건 뭔가요?
</strong></summary>

```text
어떤 객체를 네트워크를 통해 전송하거나 파일에 저장하려고 할 때 
객체에 민감한 정보가 든 데이터는 포함되지 않도록 하기 위해서
transient 키워드를 사용합니다. 

이 키워드를 사용하면 해당 필드는 직렬화에 포함되지 않습니다.
```

</details>


---

<details>
<summary><strong style="font-size:1.17em">
SerialVersionUID는 왜 선언해야 하나요?
</strong></summary>

```text
직렬화된 데이터의 버전 관리를 위함입니다.
만약 시간이 흘러 바이트스트림을 객체로 역직렬화 할때 
해당 클래스가 변경사항이 생기면 함부로 역직렬화하다가 문제가 생길 수 있습니다. 
그래서 이를 방지하기 위해 차라리 버전관리를 해서 예외가 발생하도록 하는 것 같습니다. 
```

</details>

---

## JVM, 메모리 관점

---

<details>
<summary><strong style="font-size:1.17em">
콜바이 레퍼런스와 콜바이 밸류의 차이점은 무엇인가요?
</strong></summary>

```text
콜바이밸류는 복사된 데이터를 전달하기 때문에 
값의 수정이 일어나도 원본 데이터에는 영향을 주지 않습니다.

자바는 기본타입 변수와 레퍼런스타입 변수 모두 콜바이밸류로 동작합니다.

콜바이 레퍼런스는 주소 값을 전달하여 
실제 값에 대한 Alias를 구성하기 때문에 값을 수정하면 원본의 데이터가 수정됩니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
변수를 메모리에 어떻게 할당하나요?
</strong></summary>

```text
기본 타입 변수는 변수에 실제 값을 저장하고, 메소드 내에 있는 
지역변수나 파라미터변수의 경우에는 스택프레임 형태로 스택에 할당됩니다.

반면 레퍼런스 타입은 new 키워드로 객체를 생성하면 실제 객체는 힙 메모리에 저장하고, 
레퍼런스 변수에는 그 객체를 가리키는 메모리 주소를 저장합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
스택 메모리와 힙 메모리를 이야기 하셨는데 이 둘의 차이점에 대해 더 자세히 설명해주세요
</strong></summary>

```text
스택은 메소드 호출이나 로컬 변수등을 
스택 프레임 형태로 저장하고 스택에 할당합니다. 
또한, 각 스레드는 자신의 스택이 있으며, 
해당 스택은 LIFO 순서를 따릅니다. 
또한 값을 직접 저장하기 때문에 힙에 비해 접근속도가 빠릅니다.

힙은 객체를 저장하는 데 유리합니다. 
또한 힙 메모리는 모든 스레드에서 공유하기 때문에 
객체의 상태등을 설정할 때 
동시성에 유의해야하며, 
가비지 컬렉터에 의해 참조되지않는 객체는 자동으로 정리되며 메모리 관리를 합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
JVM에는 어떤게 있죠?
</strong></summary>

```text
클래스로더, 런타임메모리영역, 실행엔진이 있습니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
자바의 메모리 구조에 대해 상세히 설명해 주세요
</strong></summary>

```text
힙 메모리, 스택 메모리, PC 레지스터, 메타스페이스 , 네이티브 메서드 스택이 있습니다.

- 힙 영역은 실제 객체 및 배열 할당을 위한 
스레드의 공유 공간이자 가비지 수집을 합니다.

- 스택 영역은 각 스레드 별로 따로 할당되는 영역이며 
로컬 변수 및 참조변수 등에 대해 스택 프레임을 사용하여 스택에 할당

- PC 레지스터는 각 스레드의 현재 명령을 추적합니다.

- 메타스페이스는 상수 풀이나 
클래스 및 메서드 정보를 포함한 클래스 수준 데이터를 저장하는 영역

- 네이티브 메서드 스택은 네이티브 메서드 실행을 위한 스택입니다. 
```


</details>

---

<details>
<summary><strong style="font-size:1.17em">
Java 컴파일 과정에 대해 자세히 설명해주세요
</strong></summary>

```text
1. 개발자가 자바 코드를 작성한 .java 파일을 
javac 컴파일러를 이용해 바이트코드로 변환합니다.

2. 컴파일된 class 파일은 클래스로더에 의해 JVM 메모리에 할당합니다. 
이 과정은 loading, linking, initialising 과정을 거칩니다.

3. 인터프리터는 바이트코드를 명령어 단위로 해석하여 실행합니다.

4. 성능 개선을 위해 JIT 컴파일러는 지속적으로 컴파일된 코드를 추적 합니다. 
JIT 컴파일러는 자주 실행되는 코드인 hotspot을 식별합니다.

5. JIT 컴파일러가 hotspot인 코드를 컴파일하여 만든 네이티브 코드를 Code Cache에 배치합니다. 
향후 중복된 메소드는 캐시에 저장된 네이티브 코드를 실행하여 성능을 향상시킵니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
JVM이 바이트코드를 실행하는 방식에 대해 설명해보세요
</strong></summary>

```text
JVM은 두 가지 방식으로 바이트코드를 실행합니다

인터프리터 방식

바이트코드를 한줄씩 해석하면서 실행합니다
각 바이트코드 명령어에 대응하는 미리 만들어진 네이티브 코드를 실행합니다
예: iadd 바이트코드 → 정수 덧셈용 네이티브 코드 실행
장점: 바로 실행 가능
단점: 매번 해석이 필요해서 느림


JIT(Just-In-Time) 컴파일러 방식

자주 실행되는 코드(핫스팟)를 발견하면 바이트코드 전체를 네이티브 코드로 변환합니다
한번 컴파일된 코드는 캐시에 저장해두고 재사용합니다
장점: 변환된 네이티브 코드를 직접 실행하므로 매우 빠름
단점: 초기 컴파일 시간이 필요함
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
JDK, JRE, JVM 차이
</strong></summary>

```text
JDK는 Java 애플리케이션을 개발하는 데 사용하는 소프트웨어개발 환경 입니다. 
여기에는 JRE와 javac 컴파일러, 디버거 등 개발도구를 포함합니다.

JRE는 JVM과 자바 클래스 라이브러리로 구성됩니다. 
자바프로그램을 실행시키기위한 최소한의 환경입니다.

JVM은 자바 바이트코드를 실행하는 가상머신입니다. 
플랫폼 독립성을 제공하며, Interpreter와 JIT 컴파일러인 실행엔진이 있습니다. 
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
클래스의 멤버 변수 초기화 순서를 말해보세요
</strong></summary>

```text
정적(static) 변수: 클래스 로딩 시 초기화됩니다. 
먼저 기본값으로 초기화된 후, 명시적 초기화와 static 블록이 순서대로 실행됩니다.

인스턴스 변수: 객체 생성 시 초기화됩니다. 
기본값 초기화 후, 명시적 초기화와 인스턴스 초기화 블록이 순서대로 실행됩니다.

생성자: 마지막으로 생성자에서 추가적인 초기화가 이루어집니다.
```

</details>

---

## GC

---

<details>
<summary><strong style="font-size:1.17em">
가비지 컬렉터를 이야기 했는데 이게 정확히 뭐고 가비지 컬렉션의 과정과 어떤 종류가 있는 지 자세히 설명해주세요
</strong></summary>

```text
가비지 컬렉터란, 참조되지 않은 객체를 추적하여 메모리를 회수합니다. 이렇게 메모리 관리를 하는 실행엔진입니다.

이제 과정을 말씀드리면, 
1. JVM은 가비지 컬렉션을 실행하기 위해 애플리케이션의 실행을 멈추는 stop-the-world를 먼저 실행합니다.

2. stop-the-world를 실행하면 GC를 실행하는 쓰레드를 제외한 모든 쓰레드가 작업을 멈춥니다.

3. 가비지 컬렉션 작업은 Young 영역에 대한 Minor GC와 Old 영역에 대한 Major GC로 구분됩니다.

4. Young 영역은 1개의 Eden 영역, 2개의 Survivor 영역으로 구성되며, 
처음 생성된 객체는 Eden 영역에 생성됩니다.

5. Eden 영역이 가득차면, Minor GC가 발생하고, 
Eden 영역과 Survivor 영역에 있는 살아있는 객체는 비어진 Survivor공간으로 재배치됩니다. 
즉, Survivor 영역 중 한 곳은 반드시 비어져있습니다.

6. 이 동작이 반복되어 특정 aging 만큼 살아남은 객체는 Old 영역으로 이동됩니다.

7. 그리고 Old 영역이 가득차서 Survivor 영역에서 Old 영역으로 승격이 불가능할 때 Old 영역에 대한 Major GC가 발생합니다.

가비지 컬렉션의 알고리즘 종류에는 Serial GC, Parallel GC, Parallel Old GC, CMS, G1 GC, ZGC가 있습니다.

- Serial GC는 Young 영역에선 mark & copy 방식을 사용하며, 
Old 영역에서는 mark&sweep&compact 방식을 사용합니다. 
이는 GC를 위해 단일 스레드를 사용합니다.

- Parallel GC는 Serial GC와 기본적인 알고리즘은 같습니다. 
하지만 Minor GC를 처리하는 스레드가 여러개 있습니다. 

- Parallel Old GC는 
Old 영역에서 Mark summary compact 방식을 사용합니다. 
이 mark summary compact 방식은 여러 스레드를 사용하여 old 영역을 탐색하고 정리합니다.

- CMS GC는 Concurrent Mark Sweep의 약자로,
대부분의 GC 작업을 애플리케이션 실행과 동시에 수행합니다. 
Initial Mark, Concurrent Mark, Remark, Concurrent Sweep 단계로 구성됩니다. 

- G1 GC는 힙을 균등한 크기의 영역으로 나누어 관리합니다. 
각 영역은 Eden, Survivor, Old, Humongous 중 하나의 역할을 합니다.

1) Young GC
   - Eden Region이 가득 차면 실행
   - 살아있는 객체를 Survivor Region으로 이동

2) Mixed GC
   - Old Region의 점유율이 임계값을 넘으면 실행
   - Young GC와 함께 일부 Old Region도 수집

3) Full GC
   - 메모리가 부족하거나 다른 GC가 실패할 경우 실행
   - 전체 힙을 대상으로 수행
   

또한 'Garbage First'라는 이름처럼 가비지가 많은 영역을 우선적으로 수집합니다. 
전체 힙에 대한 Compact 작업 없이 조금씩 압축하고 병렬, 동시 처리를 모두 사용하여 효율성을 높입니다.

- ZGC는 힙을 고정 크기의 영역(ZPage)으로 나누어 관리합니다. 
물리적 메모리 압축 없이 논리적으로 메모리를 재배치합니다.  
대부분의 GC 작업을 애플리케이션 실행과 동시에 수행합니다.
```


</details>

---

<details>
<summary><strong style="font-size:1.17em">
minor gc는 왜 mark copy고 major gc는 mark sweep compact인가요?
</strong></summary>

```text
Young Generation은 대부분의 객체가 빠르게 사라지는 특성을 가집니다.
살아있는 객체만 복사하므로, 대부분의 객체가 죽는 Young 영역에서 매우 효율적입니다.

Old Generation은 오래 살아남은 객체들이 있어 대부분의 객체가 살아있는 특성을 가집니다. 
대부분의 객체가 살아있기 때문에, 모든 객체를 복사하는 것은 비효율적입니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
Young 영역과 Old 영역을 나눈 이유가 뭔가요?
</strong></summary>

```text
약한 세대 가설에 따르면, 대부분의 객체는 일찍 죽는다 입니다. 
즉, 새롭게 만들어진 객체들 중
대부분은 아주 빨리 쓸모가 없어져서 제거된다는 뜻입니다. 

또한, 어떤 객체들은 일정 시간 동안 살아남으면, 그 이후로도 계속 오래 살아남는 경향이 있습니다.

이런 가설은 수많은 관찰로 사실로 입증되었고, 
새로 만들어진 객체들과 오래된 객체들을 다르게 
메모리 정리 작업을 적용하면 더 효과적으로 성능좋게 수행할 수 있습니다.
```

</details>


---

<details>
<summary><strong style="font-size:1.17em">
Stop-the-world가 필요한 이유가 뭔가요?
</strong></summary>

```text
compaction단계에서 살아있는 객체의 메모리이동이 일어나면서 참조주소가 바뀌게되는데 
이때, 옮길려는 곳에 갑자기 누군가 참조한다면 문제가 생깁니다.

그리고 더이상 참조되지 않는 객체를 수집하려고하는데 
동시에 애플리케이션에서 해당 객체를 참조하게된다면 문제가 생길 수 있습니다.
```


</details>

---

<details>
<summary><strong style="font-size:1.17em">
CMS GC에 대해 설명해주세요 
</strong></summary>

```text
CMS GC는 애플리케이션의 응답 시간을 최적화하기 위해 설계된 가비지 컬렉터입니다. 
가장 큰 특징은 가비지 컬렉션 작업의 대부분을 애플리케이션 스레드와 동시에 수행한다는 점입니다.

Old Generation에서는 Initial Mark, Concurrent Mark, Remark, Concurrent Sweep 이렇게 4단계로 동작하는데, 
이 중 Initial Mark와 Remark 단계에서만 짧은 STW(Stop-The-World)가 발생하고 
나머지는 애플리케이션과 동시에 실행됩니다.

Young Generation에서는 ParNew 콜렉터를 사용하여 STW 방식으로 동작합니다.

단, CMS는 CPU 사용량이 높고 메모리 단편화 문제가 있으며, 
Compaction을 기본적으로 수행하지 않는다는 단점이 있습니다. 

그래서 일반적으로 응답 시간이 중요한 애플리케이션에서 
힙 크기가 작은 경우(4GB 미만)에 주로 사용됩니다
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
G1 GC에 대해 설명해주세요
</strong></summary>

```text
G1GC는 Java 9부터 기본 GC로 채택된 가비지 컬렉터입니다. 

가장 큰 특징은 힙 영역을 동일한 크기의 Region들로 나누어 관리한다는 점입니다.
각 Region은 Eden, Survivor, Old 등 역할이 동적으로 부여되며, 
G1GC는 'Garbage First'라는 이름처럼 가비지가 가장 많은 Region부터 수집하는 방식으로 동작합니다. 

그리고 GC 과정은 크게 Young GC와 Mixed GC로 나뉩니다

Young GC는 Eden Region이 차면 발생하며, Remember Set을 봐서 
살아있는 객체를 Survivor Region으로 복사합니다.

Mixed GC는 Old Region의 점유율이 임계값을 넘으면 발생하며, 
Young Region과 일부 Old Region을 함께 수집합니다.

이런 특성 때문에 G1GC는 대용량 메모리를 사용하는 애플리케이션에서 특히 효과적입니다.
```


</details>

---

<details>
<summary><strong style="font-size:1.17em">
G1GC에서 Remembered Set와 Collection Set이 무엇인지 설명해주세요 
</strong></summary>

```text
Remembered Set은 각 Region마다 존재하는 자료구조로, 
다른 Region에서 이 Region을 참조하는 객체들의 정보를 담고 있습니다.

Collection Set은 GC를 수행할 때 수집 대상이 되는 Region들의 집합입니다. 
Young GC 때는 Young Region만, Mixed GC 때는 Young Region과 일부 Old Region이 포함됩니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
CMS GC보다 G1 GC가 더 좋은 이유가 뭐고, 뭐땜에 교체되었나요?
</strong></summary>

```text
G1은 메모리 단편화 문제를 더 효과적으로 해결합니다.
CMS는 Compaction을 기본적으로 수행하지 않아 메모리 단편화가 심각한 문제였지만, 
G1은 Region 기반으로 메모리를 관리하며 필요할 때 자동으로 지정된 리전에만 Compaction을 수행하여
효율적으로 관리합니다.

G1은 더 예측 가능한 GC 중단 시간을 제공합니다. 사용자가 목표 일시 중지 시간을 설정할 수 있고
G1은 이 목표를 맞추기 위해 동적으로 조절합니다.

G1은 큰 힙 메모리에서 더 효율적으로 동작합니다. 
Region 기반 수집으로 전체 힙이 아닌 필요한 영역만 GC를 수행할 수 있어, 
대용량 메모리 환경에서 더 나은 성능을 보입니다.

```

</details>

---


## final, equals, hashcode

---

<details>
<summary><strong style="font-size:1.17em">
final 설명해주세요
</strong></summary>

```text
final 키워드는 크게 변수, 메서드, 클래스 에 사용할 수 있습니다. 

변수에 final 을 사용하면, 해당 변수는 더이상 '재할당' 할 수 없게 됩니다. 

메서드에 사용하면, 해당 메서드는 자식클래스에서 '오버라이드' 될 수 없습니다.

클래스에 사용되면, 해당 클래스는 '상속' 할 수 없습니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
Object에서 사용되는 equals와 hashcode는 무엇이고, 사용 시 유의할 점
</strong></summary>

```text
equals는 두 객체가 동일한지 비교하고, 
hashcode는 객체의 메모리 주소를 기반으로 정수값을 생성합니다.

유의할 점은 equals를 동일성과 동등성을 보장받기 위해 재정의를 하게 되는데, 
이때 hashcode()도 반드시 재정의 해야합니다.

왜냐하면 만약 equals만 재정의를 했다면 
동등성이 보장된 객체들의 hashcode는 다른 정수값을 반환 합니다. 

즉, 이때 equals에서는 동등성을 보장받아 true을 반환하는 데, 
HashMap이나 HashSet에서 해당 객체들을 저장한다면
서로 다른 객체로 판단하여 해시테이블에 두 객체 모두를 저장합니다.

또 다른 유의할 점은
hashcode를 재정의할 떄,
최대한 중복되지 않게 반환해야합니다.
안그러면 같은 버킷에 여러 객체들이 저장되어
시간복잡도가 O(1)에서 O(N)으로 증가합니다. 
```


</details>

---

## 자료구조,알고리즘

---

<details>
<summary><strong style="font-size:1.17em">
컬렉션 프레임워크에는 뭐가 있나요? 그리고 자세히 구현체 클래스들에 대해 설명해주세요
</strong></summary>

```text
컬렉션 프레임워크는 객체들을 그룹화하고, 관리하기 위한 자료구조 입니다.
해당 프레임워크에는 List, Set, Queue, Map 등의 인터페이스와 구현체들이 존재합니다.

- ArrayList는 동적으로 크기가 조정가능한 배열입니다. 
또한 읽기에 걸리는 시간은 시간복잡도 O(1)이 걸리며, 
만약 특정 위치에 요소의 추가나 제거가 일어날 경우
그 뒤의 요소들이 뒤로 밀려나가기 때문에 최악의 경우 O(N) 시간이 걸립니다. 
메모리 위치는 연속적이며, 캐시 친화적입니다.

- LinkedList는 List 인터페이스와 Deque 인터페이스를 모두 구현한 이중 연결리스트입니다.
삽입,제거 작업이 O(1)이며, 
탐색 작업은 최악의 경우 O(N)의 시간이 걸립니다.
앞과 뒤를 기억하는 포인터도 저장하기 때문에 
메모리를 더 많이 사용합니다.

- Vector는 컬렉션 프레임워크가 나오기 전이였고, 
Thread-Safe 하기위해서 동시성을 보장하기 때문에 ArrayList에 비해 성능이 떨어집니다.
- Queue 역시 Vector를 상속받은 클래스라 Thread-safe하고 성능이 느립니다.

Set 인터페이스에는 HashSet, LinkedHashSet, TreeSet, EnumSet이 있습니다. 

- HashSet은 고유한 요소를 저장하며, null값 허용하고, 
내부적으로 HashMap을 사용하여 요소의 해시코드를 키로 사용하여 해시 테이블에 저장됩니다. 
이를 통해 요소를 추가, 제거, 검색 시간복잡도가 일반적으로 O(1)입니다.

- LinkedHashSet는 삽입 순서를 보장하고, 중복요소 허용하지 않습니다.
- TreeSet은 요소를 정렬된 순서로 유지합니다.
- EnumSet은 Enum타입을 위한 특별한 Set 구현체로, 비트 백터 기반으로 구현합니다. 
모든 기본 연산이 상수시간이며, 오직 Enum 타입의 요소만 가능합니다.

Map 인터페이스는 HashMap, LinkedHashMap, TreeHashMap이 있습니다. 
- HashMap은 해시테이블에 키-값 쌍을 저장하는 자료구조입니다. 
이를 통해 키를 기반으로 값에 액세스할 수 있습니다.
HashMap에서 키는 고유하지만, 중복된 키를 추가하려면 키에 연결된 값이 새 값으로 덮어쓰여집니다.
그리고 만약 서로 다른 키가 동일한 인덱스로 해시가 될 때, 
Seperate Chaining 방식으로 동일한 버킷에 담겨지고 
데이터가 6개일때는 연결리스트, 8개일때는
레드-블랙 트리로 저장하며 충돌을 해결합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
concurrnetHashMap 은 어떻게 구현되어 있나요?
</strong></summary>

```text
get 메소드는 synchronized 키워드가 없습니다. 
즉, 동시성제어가 없어 조회성능이 좋습니다. 

put 메소드는 빈 bucket에 노드를 삽입하는 경우엔 
CAS 알고리즘을 사용해 synchronized 없이 노드를 삽입합니다.

그리고 다른 버킷 사이에 노드를 삽입할때는 동시에 삽입이 가능합니다

이미 bucket에 Node가 존재하는 경우엔 synchronized를 이용해 
다른 스레드가 접근하지 못하도록 lock을 걸어 
다른 thread의 Node가 같은 hash bucket에 접근을 차단합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
HashMap 시간복잡도
</strong></summary>

```text
HashMap의 시간 복잡도는 기본적으로 O(1)입니다.
이는 해시 함수를 통해 키의 저장 위치를 바로 찾아갈 수 있기 때문입니다. 
하지만 실제로는 해시 충돌이 발생할 수 있습니다.

이런 충돌을 처리하기 위해 체이닝 방식을 사용합니다. 
즉, 같은 버킷에 여러 데이터가 들어가면 링크드 리스트 형태로 연결합니다. 
이 경우, 최악의 상황에서는 모든 데이터가 하나의 버킷에 들어가 O(n)의 시간 복잡도를 가질 수 있습니다.

그런데, 자바 8부터는 하나의 버킷에 데이터가 8개 이상 쌓이면, 
그 구조를 링크드 리스트에서 레드-블랙 트리로 바꿉니다. 
레드-블랙 트리는 균형 이진 탐색 트리의 일종으로, 
이를 통해 최악의 경우에도 O(log n)의 시간 복잡도를 보장할 수 있게 됩니다.
```


</details>

---

<details>
<summary><strong style="font-size:1.17em">
Map에 저장할 객체가 Comparable 인터페이스를 구현하면 성능이 좋아지는 이유
</strong></summary>

```text
HashMap은 버킷에 담겨진 데이터의 개수가 많아질 때(6개 -> 8개) LinkedList 구현에서 Red-Black Tree로 구성합니다. 
이때 각 노드들이 ordering이 되야하는데, 즉 정렬을 위해서는 객체를 서로 비교해야한다는 것입니다. 
그때 해당 객체가 comparable 인터페이스를 구현하지 않았을 경우, 내부에서 자체 비교함수를 호출합니다. 
근데 이 비교함수에는 연산이 더 많기 때문에 성능이 떨어집니다. 
따라서 comparable 인터페이스를 구현한 클래스로 만들면 좋습니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
정렬알고리즘에 대해 아는 거 설명해주세요
</strong></summary>
https://gmlwjd9405.github.io/2018/05/10/algorithm-heap-sort.html

```text
1. 버블 정렬
   버블정렬은 배열내의 두개의 인접한 Index를 비교하여 더 큰 숫자를 뒤로 보내 차곡차곡 쌓아 정렬하는 방법입니다.
   결론적으로 말하자면 배열의 뒷쪽부터 정렬하는 방법이라고 생각하시면 될 듯 합니다.
   - 시간복잡도: O(n²)
   - 특이사항: 스테블한 정렬

2. 선택 정렬
   선택정렬은 해당 순서에 원소를 넣을 위치는 이미 정해져 있고, 
   그 위치에 어떤 원소를 넣을지 선택하는 알고리즘입니다
   - 시간복잡도: O(n²)
   - 특이사항: 불안정 정렬

3. 삽입 정렬
   삽입정렬은 배열의 모든 요소를 앞에서부터 차례대로 이미 정렬된 배열 부분과 비교하여 자신의 위치를 찾아 삽입하는 것입니다.
   - 시간복잡도: O(n²), 최선의 경우 O(n)
   - 특이사항: 스테블한 정렬,
   Selection Sort나 Bubble Sort과 같은 O(n^2) 알고리즘에 비교하여 상대적으로 빠릅니다.

4. 퀵 정렬
   - 로직: 피벗을 선택하고 피벗보다 작은 원소와 큰 원소로 분할, 재귀적으로 정렬
   - 시간복잡도: 평균 O(n log n), 최악의 경우 O(n²)
   - 특이사항: 불안정 정렬 

5. 병합 정렬
   - 로직: 리스트를 반으로 나누고, 각각을 정렬한 후 병합
   - 시간복잡도: O(n log n)
   - 특이사항: stable한 정렬, 연결 리스트 정렬에 효과적

6. 힙 정렬
   - 로직: 배열을 힙으로 만들고, 최대 힙에서 루트를 반복적으로 제거하여 정렬
   완전 이진 트리의 일종으로 우선순위 큐를 위하여 만들어진 자료구조입니다.
   - 시간복잡도: O(n log n)
   - 특이사항: 추가 메모리 사용이 거의 없음, Non stable 합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
정렬알고리즘에 구현
</strong></summary>

```text
선택정렬
import java.util.Arrays;

// 선택 정렬
public class SelectionSort {

    public static void main(String[] args) {
        int[] number = {15,3,23,64,77,46,42,174,68,78,91,5,76,310,84,342,176,120,33,41};

        // swap 할 공간
        int temp;

        for (int i = 0; i < number.length-1; i++) {			// 1
            int indexMin = i;
            for (int j = i+1; j < number.length; j++) {		// 2
                // > 내림차순, < 오름차순
                if(number[j] < number[indexMin]) {			// 3
                    indexMin = j;
                }
            }
            
            // 4
            temp = number[indexMin];
            number[indexMin] = number[i];
            number[i] = temp;
        }

        System.out.println(Arrays.toString(number));
    }
}


// 버블 정렬
public class BubleSort {

    public static void main(String[] args) {
        int[] number = {11,234,23,4,1,5,6,2,65,764,825,46,72,47,26,69,793,25,498,245};

        for (int i = 0; i < number.length; i++) {				//1
            for (int j = 0; j < number.length -i -1; j++) {		//2
                // < 내림차순, > 오름차순
                if(number[j] > number[j+1]) {					//3
                    int temp = number[j+1];
                    number[j+1] = number[j];
                    number[j] = temp;
                }
            }
        }

        System.out.println(Arrays.toString(number));
    }
}


// 삽입정렬
	public static void main(String[] args) {
		nums = new int[10];
		for (int i = 0; i < 10; i++) {
			nums[i] = (int) (Math.random() * 10);
		}
		System.out.println("<정렬 전>");
		System.out.println(Arrays.toString(nums));
		
		for(int i = 1; i < nums.length; i++) {
			// 현재 선택된 원소의 값을 임시 변수에 저장해준다.
			int temp = nums[i];
			// 현재 원소를 기준으로 이전 원소를 탐색하기 위한 index 변수.
			int prev = i - 1;
			// 현재 선택된 원소가 이전 원소보다 작은 경우까지만 반복. 단, 0번째 원소까지만 비교한다.
			while(prev >= 0 && nums[prev] > temp) {
				// 현재 선택된 원소가 현재 탐색중인 원소보다 작다면, 해당 원소는 다음 인덱스로 미뤄버린다.
				nums[prev + 1] = nums[prev];
				// 다음 대상 원소를 탐색한다.
				prev--;
			}
			// 탐색이 종료된 지점에 현재 선택되었던 변수의 값을 삽입해준다.
			nums[prev + 1] = temp;
		}
		
		System.out.println("<정렬 후>");
		System.out.println(Arrays.toString(nums));
	}
}
```

</details>

---

## 싱크,논싱크,블로킹,논블로킹 

---

<details>
<summary><strong style="font-size:1.17em">
동기,비동기,블로킹,논블로킹 차이에 대해 아나요?
</strong></summary>

```text
동기/비동기는 IO 작업의 완료 여부를 누가 담당하는지에 관한 것입니다.

동기 방식은 프로세스가 IO 작업의 완료 여부를 계속 체크하면서 직접 결과를 처리합니다.
반면 비동기는 IO 작업의 완료 시 커널이 시그널이나 콜백으로 프로세스에게 알려주고, 결과 처리는 이벤트 핸들러를 통해 이루어집니다.


블로킹/논블로킹은 시스템 콜 호출 시 제어권에 관한 것입니다.

블로킹은 시스템 콜이 완료될 때까지 프로세스가 대기 상태(wait queue)에 들어가고 제어권이 커널에 넘어갑니다.
논블로킹은 시스템 콜 호출 시 작업 완료 여부와 관계없이 즉시 리턴하여 프로세스가 제어권을 계속 가지고 있습니다.

실제 구현에서는

동기 블로킹: read() 시스템 콜처럼 IO 완료까지 프로세스 대기
동기 논블로킹: non-blocking read()처럼 즉시 반환되지만 완료를 계속 체크
비동기 논블로킹: aio_read()처럼 요청 후 이벤트로 완료 통지 받음

이런 방식이 됩니다. 비동기 블로킹은 개념적으로 모순되어 구현되지 않습니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
동기,비동기,블로킹,논블로킹의 조합을 설명해주세요
</strong></summary>

```text
블로킹+동기: 다른 함수가 작업이 끝날때까지 기다리고 결과를 반환하면 
그 결과를 토대로 자신의 다음 작업을 시작합니다.

블로킹+비동기: 다른함수가 끝날때까지 기다렸는데 
그 결과를 호출한 함수가 다음 작업을 실행하는데 필요한 결과가 아니라서 
아무때나 그 결과에 대해 처리할 수 있습니다.
즉, 결과가 본인의 다음작업에 의존되지 않기때문에 기다릴 필요도 없는것 입니다.

논블로킹+동기: 다른 작업이 있어도 바로 반환받고 자신의 작업을 실행합니다. 
그런데 동기는 결과에 관심이 있기때문에 중간마다 계속 결과여부를 물어봅니다.

논블로킹+비동기: 다른 작업이 시작되어도 본인 작업을 수행합니다
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
싱크 블로킹과 싱크 논블로킹 차이
</strong></summary>

```text
싱크블로킹은 제어권 자체가 호출된 함수로 넘어가고 병렬처리가 안됩니다.
싱크논블로킹은 제어권이 본인에게 있기 때문에 멀티스레드환경에서 동시에 작업을 처리할 수가 있습니다. 
```


</details>


---

## 스레드

---

<details>
<summary><strong style="font-size:1.17em">
프로세스와 스레드 차이점이 뭐죠? == 스레드는 뭔가요?
</strong></summary>

```text
프로그램은 실행파일입니다. 여기에는 코드나 프로세서 명령집합이 
파일형태로 디스크에 저장되어있습니다.

프로그램의 코드가 메모리에 로드되고
프로세서에 의해 실행되면 프로세스가 됩니다. 

스레드는 프로세스 내에서 실행되는 작업 단위 입니다. 

```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
스레드는 메모리 공간을 공유한다는데, 정확히 어디 영역이 공유되죠?
</strong></summary>

```text
코드영역과 데이터영역,힙영역은 공유되며, 
데이터 영역의 일부(전역변수,정적변수, BSS영역에 있는 초기값없는 변수)는 
read-write 부분이라 동기화가 필요합니다.

스택영역은 스레드마다 부여되기 때문에 공유되지 않습니다.
```

</details>


---

<details>
<summary><strong style="font-size:1.17em">
스레드를 실행할 때 start()와 run()의 차이가 뭔가요? 그냥 run()으로 실행하면 안되나요?
</strong></summary>

```text
run()을 직접 호출하는 경우, 새로운 스레드가 생성되지 않고, run을 호출한 스레드에 run() 스택 프레임이 올라갑니다. 
결과적으로 호출한 스레드에서 모든 것을 처리하게 됩니다.

start()는 내부적으로 네이티브메소드를 통해 커널 스레드 생성을 요청하고 JVM 스레드와 매핑하는 작업을 합니다. 
그리고 만들어진 스레드에 스택을 할당한다음, 만들어진 스레드에 run() 메서드를 실행합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
스레드 생명주기를 말하세요
</strong></summary>

```text
NEW 상태는 새로운 스레드 객체가 생성된 직후의 상태를 의미합니다.
 아직 시작되지 않은 상태로, start() 메소드가 호출되지 않은 상태입니다.

RUNNABLE: 실행가능한 상태로, 운영체제 스케줄러의 대기열에 있거나, CPU에서 실제 실행되고 있는 상태입니다.

BLOCKED: 스레드가 다른 스레드에 의해 모니터 락을 얻기 위해 기다리는 상태입니다.

WAITING: 대기상태로, 스레드가 다른 스레드의 특정 작업이 완료되기를 무기한 기다리는 상태입니다. 
이는 wait(), join() 메소드가 호출될 때, 해당 상태로 변합니다.

Timed Waiting: Wating과 마찬가지로 
다른 스레드의 작업이 끝날 때까지 기다리지만 주어진 시간이 경과하면
이 상태에서 벗어납니다. 

Terminated: 스레드의 실행이 완료되어 정상적으로 종료되거나, 
예외가 발생하여 종료된 경우 이 상태로 바뀝니다. 
스레드는 한 번 종료되면 다시 시작할 수 없습니다.
```


</details>

---

<details>
<summary><strong style="font-size:1.17em">
synchronized 단점이 뭔가요?
</strong></summary>

```text
무한대기와 공정성 문제가 있습니다.
즉,
- 락을 획득하지 못하면 계속 대기하고, 락을 포기하고 나갈 방법이 없습니다.
- 어떤 스레드가 장기간 락을 획득하지 못하는 기아 현상(starvation)이 발생할 수 있습니다.

그외에도
- 하나의 스레드만 진입가능하므로 성능 문제
- 데드락 위험 
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
데드락이 걸리는 조건이 뭐죠?
</strong></summary>

```text
데드락이 발생하려면 4가지가 충족되어야 합니다.

상호배제: 한 번에 하나의 트랜잭션만 자원 사용 가능
점유와 대기: 자원1 점유하고 있으면서 다른 자원2를 요청
비선점: 다른 트랜잭션이 락을 강제로 빼앗을 수 없음
순환 대기: A->B ,B->A가 가지고 있는 자원을 요청합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
인터럽트의 목적은 뭔가요? wait()으로 대기중인 스레드를 깨우기 위해 notify()를 사용한 것과 달리 뭘 위한 걸까요?
</strong></summary>

```text
인터럽트는 스레드에게 "현재 작업을 중단하고 다른 행동을 취하라"는 신호로 사용됩니다. 
단지, 깨우는게 목적이 아니라 
스레드의 동작을 제어하고 
비정상적인 상황(시간 초과, 사용자 요청 등)에 대응하기 위한 메커니즘입니다. 
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
생산자,소비자 문제가 무엇인가요?
</strong></summary>

```text
생산자 소비자 문제는 멀티스레드 프로그래밍에서 자주 등장하는 동시성 문제 중 하나로, 
여러 스레드가 동시에 데이터를 생산하고 소비하는 과정에서 발생합니다.

예를들어, 생산자 스레드가 데이터를 너무 빨리 생성하여 버퍼가 가득차면 
이후 생성한 데이터를 버리는 문제가 발생합니다. 

또는 소비자 스레드가 너무 빨라 버퍼가 비었는데, 
이로인해 더이상 소비할 데이터가 없어 소비자 스레드는 null 값을 꺼내는 문제가 발생합니다.

예를들면, 로그처리시스템에서
한쪽은 로그쓰고 한쪽은 로그를 파일에 쓰는 점이 있을 것 같습니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
생산자-소비자 문제를 어떻게 해결할까요
</strong></summary>

```text 
먼저, synchronized와 wait()/notify() 사용하는 방법입니다. 
하지만 notify()는 스레드 대기 집합에 있던 어느 스레드가 깨어날지 알 수가 없습니다. 
다시 말해 같은 종류의 스레드가 깨어나면 락을 반납하고 다시 대기집합으로 이동하기 때문에 매우 비효율적입니다.

이를 해결하기 위해, ReentrantLock와 condition을 사용합니다. 
condition을 통해 생산자와 소비자 대기공간을 나눠서 
필요한 종류의 대기공간에 있는 스레드를 깨우는 방법으로,
앞서 문제를 해결할 수 있습니다.

마지막으로 자바에서는 이런 문제를 해결하기 위해  Java의 concurrent 패키지에서 
제공하는 BlockingQueue를 사용해서 
스레드 안전 큐를 사용하는 방법입니다. 
가장 간단하고 권장되는 방식 중 하나입니다
```

</details>


---

<details>
<summary><strong style="font-size:1.17em">
wait, notify, notifyAll에 대해 설명해주세요
</strong></summary>

```text
Object.wait() : 현재 스레드가 가진 락을 반납하고 WAITING 합니다. 
이 메소드는 현재 스레드가 synchronized 블록이나 메소드에서 락을 소유하고 있을때만 호출할 수 있습니다.

Object.notify() : 스레드 대기집합에 있는 대기 중인 스레드 중 하나를 깨웁니다. 
이 메소드는 synchronized 메소드나 블록 내에서 호출되야 하며, 
대기하다가 깨워진 스레드는 락을 다시 획득할 기회를 얻습니다.

Object.notifyAll() : 대기 중인 모든 스레드를 깨웁니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
자바에서 동시성을 해결하는 방법은 뭔가요
</strong></summary>

```text
동기화 할 수 있는 방법이 3가지가 있습니다.

synchronized 사용
java.util.concurrent.locks 사용
java.util.concurrent.atomic 사용
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
CAS 알고리즘이란 무엇이며, 어떻게 동작하나요?
</strong></summary>

```text
CAS 알고리즘은 동기화를 위해 사용되는 저수준의 원자적 연산입니다.

CAS의 동작 방식은
1. 메모리의 현재 값을 읽습니다.
2. 이 값을 기대하는 값(예상 값)과 비교합니다.
3. 두 값이 같다면, 새로운 값으로 업데이트합니다.
4. 같지 않다면, 작업을 실패로 처리하고 아무 변경도 하지 않습니다.

이 과정은 원자적으로 수행되어, 다른 스레드의 간섭 없이 안전하게 값을 변경할 수 있습니다.

atomic 패키지의 클래스의 incrementAndGet() 메소드는 내부적으로 CAS를 사용하며, 
실패 시 자동으로 재시도합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
Volitile이 뭔가요?
</strong></summary>

```text
메모리 가시성 문제를 해결하기 위한 방법입니다.

volatile키워드를 통해 값을 읽거나 쓸 때 CPU 캐시가 아닌 모두 메인 메모리에 직접 접근하도록 하여 해결합니다. 
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
메모리 가시성이 뭐죠
</strong></summary>

```text
멀티스레드 환경에서 한 스레드가 변경한 값이 다른 스레드에서 언제 보이는지 알 수 없는 문제입니다.

이는, 코어마다 캐시가 있는데, 각 코어가 메인메모리를 읽지 않고 캐시를 읽고, 
캐시에만 값을 수정하면서 캐시에 수정된 값이 다른 코어의 캐시에 적용되지않아
서로 다른 값을 읽게되면서 문제가 생깁니다.
```

</details>

---
<details>
<summary><strong style="font-size:1.17em">
스레드 로컬이 뭔가요?
</strong></summary>

```text
ThreadLocal은 멀티 스레드 환경에서 각각의 스레드가 별도의 변수를 저장하고 사용할 수 있습니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
스레드로컬은 어떻게 구현되어있나요?
</strong></summary>

```text
Java에서 ThreadLocal은 내부적으로 ThreadLocalMap이라는 내부 클래스를 사용하여 구현됩니다.

각 스레드는 Thread 객체 내부에 ThreadLocalMap을 가지고 있고, 
이 맵은 ThreadLocal 객체를 key로 사용하여 값(value)을 저장합니다. 
이를 통해 각 스레드는 자신만의 독립적인 값들을 저장하고 접근할 수 있습니다.

여기서 중요한 점은 ThreadLocalMap이 각 스레드의 내부에 저장되어 있기 때문에 
동기화 문제가 발생하지 않고, 각 스레드가 독립적으로 값을 관리할 수 있다는 것입니다.
```


</details>

---

<details>
<summary><strong style="font-size:1.17em">
스레드 로컬은 어디에 활용되나요?
</strong></summary>

```text
스레드 로컬은 사용자 인증 정보, 트랜잭션 컨텍스트 등 
스레드별로 독립적으로 유지해야 하는 정보를 저장하는 데 자주 사용됩니다.

사용자 인증 정보란, 스프링 시큐리티의 SecurityContext 이고, 
트랜잭션 컨텍스트는 현재 실행 중인 트랜잭션의 상태와 관련 정보를 포함하는 객체입니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
스레드로컬 사용시 주의사항에 대해 알고있나요?
</strong></summary>

```text
스레드 풀을 사용하는 환경에서는 스레드 로컬을 사용할 때 스레드가 재사용되기 때문에, 
스레드 로컬의 데이터가 의도치 않게 공유될 수 있습니다.

따라서 개발자가 명시적으로 remove() 메소드를 호출하여 데이터를 제거해야합니다.
```


</details>

---

<details>
<summary><strong style="font-size:1.17em">
스레드 풀의 단점이 있을까요?
</strong></summary>

```text
데드락이 발생하거나, 메모리 누수나 리소스 스레싱이 발생할 수 있습니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
스레드 풀에서 데드락이 어떻게 발생되고 이를 어떻게 방지할 수 있나요?
</strong></summary>

```text
예를들어 스레드풀이 제한된 수의 스레드를 가지고 있고, 
작업A가 작업B의 결과를 기다리고 있는데, 
모든 스레드가 사용중이라 B를 실행할 여유 스레드가 없으면, 
데드락이 발생할 수 있습니다.

해결하기 위해 작업 타임아웃을 설정하거나 
스레드풀 크기를 적절히 조정하거나 
작업 간 우선순위를 부여하면 해당 위험을 방지할 수 있습니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
리소스 스레싱이 무엇이며, 어떻게 해결하나요?
</strong></summary>

```text
스레드 풀에 스레드 개수가 너무 많아 각자 CPU 시간을 갖는 시간이 짧아지게 되고, 
이는 잦은 컨텍스트 스위칭이 발생하여 
CPU 실행시간은 줄어들고, 교체시간만 늘어나
전체적인 성능이 저하됩니다.

역시, 적절한 스레드 개수를 설정해야 합니다.
```


</details>

---

<details>
<summary><strong style="font-size:1.17em">
스레드 풀의 적정 개수를 어떻게 계산하나요?
</strong></summary>

```text
스레드 풀 적정 크기는 사용 가능한 코어 개수 곱하기 1 플러스 서비스 시간 분의 대기시간 으로 계산합니다.

하지만, 실제로는 HTTP 커넥션 풀이나 JDBC 커넥션 풀, JMS로부터의 요청 등을 
고려해야하지만 공식에는 그게 빠져있습니다.
 
따라서 CPU 목표사용률을 추가적으로 공식에 추가할 수도 있습니다. 
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
스레드 풀을 사용하지 않는 경우의 단점은 무엇인가요?
</strong></summary>

```text
작업이 요청될 때마다 새로운 스레드를 생성하고 소멸시켜야 하므로 생성,소멸에 따른 오버헤드가 발생합니다. 
이러면 CPU, 메모리 사용 증가로 전체적인 성능이 저하됩니다.

또한, 스레드의 생성과 해제 관리를 직접해야하고 스레드 개수도 직접 조절해야합니다.

하지만, 스레드 풀을 사용하면 쓰레드 풀의 크기를 조절하여 
시스템 부하를 조절하고, 과도한 작업요청으로 인한 성능 저하를 방지할 수 있습니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
스레드 풀의 종류는 뭐가 있나요?
</strong></summary>

```text
ForkJoinPool과 ThreadPoolExecutor의 두가지 유형 스레드풀이 있습니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
포크조인 풀의 기본 구조와 동작 방식을 설명해주세요
</strong></summary>

```text
먼저 구조를 보면, 포크조인 풀은 여러 개의 작업자 스레드로 구성됩니다. 
각 작업자 스레드는 자신만의 덱(deque)을 가지고 있습니다. 
이 덱에는 해당 스레드가 처리할 작업들이 저장됩니다.

동작 방식을 살펴보면, 큰 작업이 풀에 제출되면 스레드에서 이 작업을 가져가고 
재귀적으로 더 작은 하위 작업들로 분할합니다. 이를 '포크' 라고 합니다.

작업자 스레드는 모든 하위 작업이 완료되면, 그 결과들을 합쳐서 최종 결과를 만듭니다. 
이 과정을 '조인' 이라고 합니다.

포크조인 풀의 핵심 특징 중 하나는 작업 훔치기(work stealing) 알고리즘입니다. 
만약 어떤 스레드가 자신의 덱에 있는 모든 작업을 처리하고 할 일이 없어지면, 
다른 바쁜 스레드의 덱에서 작업을 가져와 처리합니다. 
이를 통해 전체적인 작업 부하가 균형을 이루게 됩니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
Executors 전략에 대해 아는 대로 설명하세요 
</strong></summary>

```text
newFixedThreadPool(nThreads): 
스레드 풀에 nThreads 만큼의 기본 스레드를 생성합니다. 
초과 스레드는 생성하지 않습니다. 
스레드 수가 고정되어 있기 때문에 
CPU, 메모리 리소스가 어느정도 예측 가능한 안정적인 방식입니다.

newCachedThreadPool(): 
기본 스레드를 사용하지 않고, 60초 생존 주기를 가진 초과 스레드만 사용합니다, 
초과 스레드의 수는 제한이 없습니다. 사용자 트래픽 예측이 어려울 때 사용합니다.

newScheduledThreadPool: 
일정 주기마다 스레드로 작업 실행합니다.

newSingleThreadExecutor: 
스레드 풀에 스레드가 단 한개이며, 테스트 용도로 보통 사용합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
Executor, ExecutorService, Executors, Future 에 대해 아는 대로 설명해주세요
</strong></summary>

```text
1. Executor:
- 가장 기본적인 인터페이스로, 작업(task)을 실행하는 객체를 나타냅니다.
- 단 하나의 메소드 execute(Runnable)만 가지고 있습니다.
- 작업 제출과 실행 메커니즘을 분리하는 데 사용됩니다.


2. ExecutorService
- Executor를 확장한 인터페이스입니다.
- 비동기 작업의 라이프사이클을 관리합니다.
- submit(), invokeAll(), invokeAny() 등의 메소드를 제공합니다.
- Future 객체를 반환하여 작업 결과를 추적할 수 있게 합니다.
- 종료(shutdown(), shutdownNow())를 관리합니다.

3. Executors
- 다양한 종류의 Executor와 ExecutorService 인스턴스를 생성하는 팩토리 및 유틸리티 메소드를 제공하는 클래스입니다.
- 예: newFixedThreadPool(), newCachedThreadPool(), newSingleThreadExecutor() 등

4. Future
- 비동기 계산의 결과를 나타내는 인터페이스입니다.
- 작업의 완료 여부 확인, 결과 가져오기, 작업 취소 등의 기능을 제공합니다.
- get() 메소드로 결과를 받아올 수 있으며, 필요시 타임아웃을 설정할 수 있습니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
Future 불편한 점이 있을까요?
</strong></summary>

```text
- 여러 Future를 쉽게 연결하거나 조합할 수 없습니다.

- get() 메서드는 결과를 기다리는 동안 스레드를 블로킹합니다.

- 예외 처리를 하기 불편합니다.

- 콜백 지원 부재: 작업 완료 시 자동으로 다음 작업을 트리거하는 메커니즘이 없습니다. 
따라서 isDone과 같은 메소드로 계속 확인하는 동기 작업을 해야합니다.

- CompletableFuture는 이러한 한계를 극복하고 
더 유연하고 강력한 비동기 프로그래밍을 가능하게 합니다
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
컴플리터블 퓨처는 어떤 문제를 해결했나요?
</strong></summary>

```text
Future 인터페이스는 여러 연산을 결합하기 어렵고, 
비동기 처리 중에 발생하는 예외를 처리하기 어려운 문제가 있었는데, 
CompletableFuture 클래스는 이 문제들을 개선하기 위해 생겼습니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
Future는 왜 예외처리 하기가 어렵나요?
</strong></summary>

```text
- Future 내부에서 발생한 예외는 future.get() 메소드를 호출할 때까지 드러나지 않습니다. 
이는 예외가 지연되어 처리됩니다.

- Future 내부에서 발생한 실제 예외는 ExecutionException으로 감싸집니다. 
따라서 원래 예외를 확인하기 위해 언래핑과정이 필요합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
컴플리터블 퓨처와 퓨처 인터페이스의 차이점은 무엇인가요?
</strong></summary>

```text
Future 인터페이스는 비동기 작업의 결과를 표현하지만, 
결과를 기다릴 때 스레드를 블로킹하고, 
여러 Future를 조합하거나 체이닝하는 기능이 부족합니다.
또한, 예외 처리가 번거로워서 유연한 비동기 작업 처리에 한계가 있습니다.

반면에 CompletableFuture는 Future의 기능을 확장한 클래스로, 
비동기 작업을 더 유연하게 처리할 수 있습니다. 

주요 차이점은:
비동기 작업을 체이닝하거나 결합할 수 있는 메서드(thenApply, thenCompose 등)를 제공합니다.
작업 완료 후 콜백을 설정할 수 있어, 블로킹 없이 결과를 처리할 수 있습니다.
예외 처리도 exceptionally, handle 같은 메서드를 통해 더 직관적으로 처리할 수 있습니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
컴플리터블 퓨처의 주요 메서드를 설명해주세요.
</strong></summary>

```text
- runAsync: 반환값이 없는 경우이며 비동기로 작업 실행 콜
- supplyAsync: 반환값이 있는 경우이며 비동기로 작업 실행 콜

둘다 인자로 넘겨줄 때 사용할 스레드 풀을 넘길 수 있으며, 
기본 스레드 풀은 ForkJoinPool.commonPool() 입니다.
common pool은 JVM 내의 모든 CompletableFuture 작업에서 공유됩니다. 
이는 여러 개의 개별 스레드 풀을 생성하는 것보다 자원을 효율적으로 사용할 수 있게 해줍니다.
(I/O작업 같이 긴 작업은 커스텀한 스레드 풀 사용하기) 

또한, 시스템의 가용 프로세서 수에 기반하여 자동으로 크기가 조정됩니다.

- thenApply
이전 작업의 결과를 받아 새로운 값을 반환합니다.
Function<T, U> 함수형 인터페이스를 사용합니다.
반환값이 있으며, 그 값으로 새로운 CompletableFuture를 생성합니다.

- thenAccept
이전 작업의 결과를 받아 처리하지만, 새로운 값을 반환하지 않습니다.
Consumer<T> 함수형 인터페이스를 사용합니다.
반환값이 없으며, CompletableFuture<Void>를 반환합니다.

- thenRun
이전 작업의 결과를 받지 않고, 단순히 다음 작업을 실행합니다.
Runnable 함수형 인터페이스를 사용합니다.
이전 작업의 결과에 접근할 수 없으며, CompletableFuture<Void>를 반환합니다.

- thenCompose
반환된 CompletableFuture의 결과를 기다려 그 값을 최종 결과로 사용합니다.
중첩된 CompletableFuture를 평탄화(flatten)합니다.
현재 CompletableFuture의 결과를 사용해 새로운 비동기 작업을 시작할 때 사용합니다.(비동기 작업의 연쇄에 적합합니다.)

- thenCombine
두 CompletableFuture가 모두 완료되면 실행됩니다.
두 결과를 입력으로 받아 새로운 결과를 만듭니다.

- allOf
allOf는 여러 개의 CompletableFuture가 모두 완료될 때까지 기다립니다.
결과값은 없고 (CompletableFuture<Void> 반환), 모든 작업의 완료만을 보장합니다.

- anyOf
가장 빨리 끝난 1개의 작업에 대해서만 콜백 실행

- exeptionally
발생한 에러를 받아서 예외를 처리합니다.

- handle, handleAsync
(결과값,에러)를 반환받아 에러가 발생한 경우와 아닌 경우 모두를 처리할 수 있습니다.
```


</details>

---

<details>
<summary><strong style="font-size:1.17em">
thenApply와 thenCompose는 비슷한거 같은데 뭔차이 인가요?
</strong></summary>

```text
- thenApply는 단순히 값을 변환합니다. 비동기 작업의 결과에 1을 더합니다.
- thenCompose는 첫 번째 비동기 작업의 결과를 사용하여 새로운 비동기 작업을 시작합니다. 
이는 두 번째 작업이 첫 번째 작업의 결과에 의존하면서도 별도의 비동기 처리가 필요한 경우에 유용합니다.
```

</details>


---

<details>
<summary><strong style="font-size:1.17em">
join()과 allOf() 차이점
</strong></summary>

```text
join으로만 구현하면 CompletableFutures의 결과를 순차적으로 처리한다는 것입니다. 
결과적으로 값이 부분적으로 처리될 수 있습니다.

반면에 allOf()를 사용하여 세 인스턴스를 결합한 다음 
Join() 메서드를 호출하여 일종의 원자성을 달성할 수 있습니다. 

그렇게 하면 모든 요소를 한 번에 처리하거나 전혀 처리하지 않을 수 있습니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
스레드 상태가 왜 중요한가요?
</strong></summary>

```text
스레드 상태를 모니터링하면 애플리케이션의 성능 병목 현상을 식별할 수 있습니다.
예를 들어, 많은 스레드가 'BLOCKED' 상태라면 동기화 문제나 데드락이 있을 수 있습니다.
불필요하게 'RUNNABLE' 상태의 스레드가 많다면 CPU 사용량이 높아질 수 있습니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
이런 상태를 확인하려면 어떻게 해야하죠?
</strong></summary>

```text
스레드 덤프를 분석하여 각 스레드의 상태를 확인하면 문제의 원인을 찾는 데 도움이 됩니다.

Thread dump란 프로세스에 속한 모든 thread들의 상태를 기록. 즉, 스냅샷을 찍은 것
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
자바 9에 나온 Flow에 대해 설명해주세요
</strong></summary>

```text
리액티브 프로그래밍을 위한 표준 인터페이스를 제공합니다. 
이는 Reactive Streams 사양을 Java 표준 라이브러리에 통합한 것입니다. 

Flow API의 주요 구성 요소는 Publisher, Subscriber, Subscription, Processor를 지원하며,
백프레셔를 지원하고, 데이터 스트림을 비동기처리합니다. 
백프레셔란, Subscriber가 처리할 수 있는 만큼의 데이터만 요청할 수 있어, 과부하를 방지합니다. 
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
스레드 혹시 써보셨어요
</strong></summary>

```text
네, 외부 API를 호출할 때 스레드를 사용해본 적이 있습니다. 
예를 들어, 외부 API 응답 시간이 긴 경우 스레드를 활용하여 API 요청을 비동기로 처리하고, 
응답을 기다리는 동안 다른 작업을 진행할 수 있도록 구현했습니다. 
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
스레드 구현체 중에 뭘 써봤나요? 
</strong></summary>

```text
ExcutorService를 활용했습니다. 
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
사용하면서 불편한 점이 있을까요?
</strong></summary>

```text
- 여러 Future를 쉽게 연결하거나 조합할 수 없습니다.
- get() 메서드는 결과를 기다리는 동안 스레드를 블로킹합니다.
- 예외 처리를 하기 불편합니다.
- 콜백 지원 부재: 작업 완료 시 자동으로 다음 작업을 트리거하는 메커니즘이 없습니다. 따라서 isDone과 같은 메소드로 계속 확인하는 동기 작업을 해야합니다.
- CompletableFuture는 이러한 한계를 극복하고 더 유연하고 강력한 비동기 프로그래밍을 가능하게 합니다
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
스레드 구현체 중에 뭘 써봤나요? 했을 때 컴플리터블 퓨처 사용했다고 말하면 그리고 걔를 쓸 때 어떤 문제가 발생했냐 뭘 조심하며 썼냐고 물어봤을 때
</strong></summary>

```text
네, `CompletableFuture`를 사용할 때 스레드 풀 크기 관리에 고민을 많이 했습니다. 
기본적으로 `CompletableFuture`는 `ForkJoinPool.commonPool()`을 사용해 스레드를 관리하는데, 

많은 비동기 작업이 동시에 실행되면 스레드 풀이 포화될 수 있거나, 
스레드 수가 부족해 병목이 발생할 수 있습니다. 

그래서 저는 `Executor`를 명시적으로 지정해 커스텀 스레드 풀을 사용했고, 
작업의 특성에 따라 스레드 풀의 크기를 조정하며 성능을 최적화했습니다. 

특히 CPU 바운드 작업과 IO 바운드 작업을 구분해 
적절한 스레드 풀 크기를 설정하는 것이 중요했습니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
JDK 21 Virtual thread가 뭔가요?
</strong></summary>

```text
기존 자바 스레드 모델은 Native thread로, 자바의 유저 스레드를 만들면 
JNI를 통해 커널 영역을 호출해 OS가 커널 스레드를 생성하고 
매핑하여 작업을 수행하는 방식이였습니다.

Virtual Thread는 
기존 Java의 스레드 모델과 달리, 
플랫폼 스레드와 가상 스레드로 나뉩니다. 
플랫폼 스레드 위에서 여러 Virtual Thread가 번갈아 가며 실행되는 형태로 동작합니다. 
마치 커널 스레드와 유저 스레드가 매핑되는 형태랑 비슷합니다.

즉 Virtual Thread는 
기존 커널스레드(1) : 유저스레드(1)의 구조가 아닌 
커널스레드(1) : 플렛폼스레드(1) : 가상스레드(N)의 구조로 매칭됩니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
Virtual thread는 어떻게 수행되나요?
</strong></summary>

```text
1. 실행될 virtual thread의 작업을 
플랫폼스레드의 workQueue에 push 합니다.

2. Work queue에 있는 작업들은 forkJoinPool에 의해
work stealing 방식으로 여유있는 플랫폼스레드에 의해 처리됩니다.

3. 처리되던 작업들은 I/O나 Sleep이거나 작업 완료 시, 
work queue에서 pop되어 park과정에 의해 
그 작업은 다시 힙 메모리로 되돌아갑니다.

4. 그리고 힙에 있던 새로운 작업이 unPark()되어 다른 가상스레드에게 부여하고 
다시 플랫폼 스레드와 매핑되어 실행됩니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
요새 그걸 왜 많이 쓰나요?
</strong></summary>

```text
- 컨텍스트 비용이 저렴합니다. 
가상 스레드는 스케줄링이 가볍고 비용이 적습니다. 
가상스레드가 park 과정에서 플랫폼스레드와 해제되고 
unpark 과정에서 다시 매핑되기 때문입니다.

- 높은 동시성 처리가 가능합니다.  
또한, 가상 스레드가 I/O작업으로 인해 park() 상태가 되면 플랫폼 스레드는 다른 가상스레드를 처리하면 되니 최대한 많은 작업들을 처리할 수 있습니다.  
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
그럼 자주 쓰면 되겠네요?
</strong></summary>

```text
아닙니다. 유의할 점들이 있습니다.

- 일단 사용하게되면 스레드풀을 지양해야하고, 
제한적인 리소스를 접근할 때 세마포어를 활용해야하고,

- synchronized 키워드와 같은 사용으로 인한 Pinning 구간을 지양해야합니다. 
-> 장점을 해치기 때문입니다 대안으로 ReentrantLock 사용

- 가상 스레드가 아무리 많이 생성되더라도, 
DB나 톰켓 커넥션 수는 한계가 있고, 
서비스에 의존하는 다른 서비스들은 각각의 처리 용량이 존재하기 때문에 병목이 발생해 성능이 급격히 떨어집니다

- CPU 바운드가 많은 작업에서는 불필요합니다.  
```

</details>

---

## String

---

<details>
<summary><strong style="font-size:1.17em">
String, StringBuffer, StringBuilder의 차이점에 대해 말해주세요
</strong></summary>

```text
String 클래스는 불변하기 때문에 문자열을 변경할 때마다 새로운 객체를 생성합니다. 
이러한 작업은 메모리 낭비를 초래하며 새롭게 객체를 생성하는 비용 때문에 성능 저하를 일으킵니다.

StringBuilder는 Thread safe 하지 않습니다. 하지만 그만큼 속도가 빠릅니다.
 
StringBuffer는 멀티스레드 환경에 유리하게 임계영역을 설정했기때문에 
Thread safe 하지만 속도가 느립니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
문자열을 연결하는 내부구현 차이를 알려주세요 == String, StringBuilder 문자열 연결 차이
</strong></summary>

```text
String의 + 연산은 버전마다 계속 최적화 되었습니다. 
자바 5버전부터는 성능 향상을 목적으로 컴파일시 StringBuilder 혹은 StringBuffer로 변환되도록 변경되었습니다.
JDK 9부터 StringConcatFactory을 이용하여 더 효율적으로 처리를 합니다.

String concat 연산은 항상 concat 메소드를 사용할 때마다 
new 키워드를 사용해 새롭게 객체를 생성하기 때문에 매우 비효율적입니다.

StringBuffer와 StringBuilder append()는 
문자열을 CharSequence의 내부 버퍼에 저장하고 
참조변수 this를 통해 본인 인스턴스를 반환하기 때문에
객체를 새롭게 생성하는 과정이 없어 성능이 좋습니다.
```

</details>

---

## 내부클래스

---

<details>
<summary><strong style="font-size:1.17em">
Nested 클래스가 뭐죠? = 내부클래스가 뭐죠?
</strong></summary>

```text
Nested class는 static nested 클래스, 
내부클래스인 local 내부 클래스와 익명 내부 클래스가 있습니다.  
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
내부 클래스를 왜 쓰나요?
</strong></summary>

```text
로컬 내부 클래스는 외부클래스의 private 멤버를 이용해야 하고, 
만들려는 클래스가 외부에는 노출 시키고 싶지않을 때 사용합니다.

익명 내부 클래스는 해당 인터페이스를 구현한 클래스를 재활용할 필요가 없고 
일회용으로 사용할 때 사용됩니다.

static 클래스는 논리적으로 묶을 필요가 있을때와 
바깥쪽 클래스의 변수 접근이 필요가 없을 때 사용합니다.
```


</details>

---

## 제네릭

---

<details>
<summary><strong style="font-size:1.17em">
제네릭이 뭐고, 어디에 쓰이나요
</strong></summary>

```text
제네릭(Generic)은 클래스, 인터페이스, 메소드를 정의할 때 <> 기호 안에 
타입 파라미터를 선언하여 사용하고, 이를 통해 다양한 데이터 타입에 대해 
재사용 가능한 코드를 작성할 수 있습니다.

제네릭을 사용하면 컴파일 시점에 타입 체크를 할 수 있어 
잘못된 형변환을 방지하고, 불필요한 타입 캐스팅을 줄일 수 있습니다.

컬렉션 프레임워크와 사용자 정의 클래스를 만들 때 사용합니다.
저같은 경우, API 응답 객체를 만들 때 사용했었습니다.  
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
bounded 와일드 카드와 unbounded 와일드 카드 차이점
</strong></summary>

```text
Unbounded 와일드카드는 모든 타입을 허용하지만, 
오직 Object 객체로 조회만 가능하고 추가는 불가능합니다.

Bounded 와일드카드는 두가지 형태가 있습니다. 
Upper Bounded 와일드카드는 
extends 키워드를 사용하고, 읽기에 사용됩니다.

Lower Bounded 와일드카드는 s
uper 키워드를 사용하고, 쓰기에 사용됩니다. 이러한 원칙을 PECS라 부릅니다.  
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
제네릭 타입의 타입 소거(type erasure)에 대해 설명해 주세요
</strong></summary>

```text
제네릭에서는 타입정보가 런타임시 소거됩니다. 
즉, 원소타입을 컴파일 시에만 검사하고 런타임시에는 따로 확인을 하지않습니다.
```

</details>


---

## 그외

---

<details>
<summary><strong style="font-size:1.17em">
불변이 뭔가요?
</strong></summary>

```text
불변성(Immutability)은 객체가 생성된 후에 그 상태를 변경할 수 없는 특성을 말합니다.
따라서 여러 스레드에서 동시에 접근해도 값이 변하지 않아 동기화 없이 안전하게 사용할 수 있습니다. 
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
JDK 7에서 8로 올라가면서 바뀐거
</strong></summary>

```text
람다식: 복잡한 Comparator 구현을 한 줄로 줄인 경험이 있습니다.

함수형 인터페이스: 콜백 패턴 구현 시 익명 클래스 대신 사용해 코드량을 줄인 경험이 있습니다.

인터페이스 디폴트 메서드: 기존 인터페이스에 새 기능을 추가할 때 구현 클래스를 전부 수정하지 않아도 돼서 편했습니다.
 
스트림: "대용량 로그 파일 처리 시 parallel() 메서드로 멀티코어를 활용해 처리 속도를 2배 이상 높인 경험이 있습니다.

Optional: null 체크 로직이 간결해져서 특정 서비스의 NullPointerException 발생률을 줄였습니다.
 
날짜 API: Date 객체는 가변적이라 멀티스레드 환경에서 문제가 많았는데, 새 API의 LocalDate와 LocalTime은 불변이라 동시성 이슈가 크게 줄었어요
또 날짜 간 연산이 매우 복잡했는데, 새 API에선 plusDays(), minusMonths() 같은 메서드로 쉽게 처리할 수 있어요

CompletableFuture: 여러 외부 API를 호출하는 복잡한 비동기 프로세스를 구현할 때 코드 가독성이 크게 향상됐습니다.

JVM 메타스페이스: 
Java 8 이전에는 PermGen 영역이 Heap 메모리에 포함되어 있어 크기가 제한되었다. 
그래서 클래스가 많은 애플리케이션을 구동하다 보면 PermGen 영역의 OOM이 발생하는 경우가 종종 발생했습니다.
Java 8부터는 이 공간이 삭제되고 동일한 기능을 하는 Metaspace 영역이 새롭게 생겼다.
이곳은 Native 영역에 속하며 OS가 크기를 자동으로 조정한다. 
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
검색 알고리즘도 아는거 설명하세요
</strong></summary> 

```text
선형 검색 (Linear Search)

로직: 배열의 처음부터 끝까지 순차적으로 탐색
시간복잡도: O(n)
특이사항: 가장 단순하지만 대규모 데이터에는 비효율적


이진 검색 (Binary Search)

로직: 정렬된 배열에서 중간값과 비교하여 탐색 범위를 절반씩 줄임
시간복잡도: O(log n)
특이사항: 정렬된 데이터에서만 사용 가능, 매우 효율적


해시 검색 (Hash Search)

로직: 키를 해시 함수로 변환하여 직접 접근
시간복잡도: 평균 O(1), 최악의 경우 O(n)
특이사항: 매우 빠르지만 해시 충돌 관리 필요


깊이 우선 검색 (Depth-First Search, DFS)

로직: 그래프나 트리에서 가능한 깊이 들어가면서 탐색
시간복잡도: O(V + E) (V: 정점 수, E: 간선 수)
특이사항: 스택 또는 재귀로 구현


너비 우선 검색 (Breadth-First Search, BFS)

로직: 그래프나 트리에서 인접한 노드부터 탐색
시간복잡도: O(V + E)
특이사항: 큐로 구현, 최단 경로 문제에 유용
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">
리플렉션이 뭐죠?
</strong></summary>

```text
리플렉션은 힙 영역에 로드 된 Class 타입의 객체를 통해, 
접근 제어자 상관없이 원하는 클래스의 정보에 접근해서 
조작할 수 있도록 지원하는 API입니다. 

조작할 수 있는 기능들에는

필드 (목록) 가져오기
메소드 (목록) 가져오기
상위 클래스 가져오기
인터페이스 (목록) 가져오기
애노테이션 가져오기
생성자 가져오기
```

</details>

---

## 어노테이션

---

<details>
<summary><strong style="font-size:1.17em">
어노테이션 프로세서가 뭐죠?
</strong></summary>

```text
Annotation Processor는 
컴파일 단계에서 Annotation에 정의된 일렬의 프로세스를 동작하게 하는 것을 의미합니다.

컴파일 단계에서 실행되기 때문에, 빌드 단계에서 에러를 출력하게 할 수 있고, 
소스코드 및 바이트 코드를 생성할 수도 있습니다.

사용하는 예로 자바의 @Override가 있으며, Lombok(롬북)이라는 라이브러리가 있습니다.
```


</details>

---

<details>
<summary><strong style="font-size:1.17em">
어노테이션 retenstion 정책
</strong></summary>

```text
RetentionPolicy.SOURCE : 소스 코드(.java)까지 남아있는다.
RetentionPolicy.CLASS : 클래스 파일(.class)까지 남아있는다.(=바이트 코드)
RetentionPolicy.RUNTIME : 런타임까지 남아있는다.(=사실상 안 사라진다.)
```

</details>


