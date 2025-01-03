## JPA

<details>
<summary><strong style="font-size:1.17em">JPA가 뭔가요?</strong></summary>

```text
- 객체와 데이터베이스 테이블 간의 매핑:
- SQL 추상화
- 특정 데이터베이스에 종속되지 않는다
- 반복적인 CRUD(Create, Read, Update, Delete) 작업을 단순화
- 객체지향적 접근
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">영속성 컨텍스트가 뭐죠?</strong></summary>

```text
영속성 컨텍스트란, 엔티티를 영구 저장하는 환경으로, 애플리케이션과 데이터베이스 사이에 엔티티를 보관하는 가상의 데이터베이스 역할을 합니다.

엔티티매니저에 엔티티를 저장하거나 조회하면, 엔티티매니저는 영속성 컨텍스트에 엔티티를 보관하고 관리합니다. 
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">영속성 컨텍스트를 왜 쓰죠?</strong></summary>

```text
1. 1차 캐시
    - 데이터베이스에 조회없이 1차 캐시에 조회하려는 엔티티가 있으면 반환하기 때문에 성능이 좋아집니다. 
2. 쓰기 지연 
    - 쿼리를 영속성 컨텍스트의 쓰기 지연 저장소에 보관하다 트랜잭션이 커밋하면 데이터베이스에 저장소에 담겨있던 쿼리들을 실행합니다 
3. 더티 체킹 
    - 커밋 시점에 영속화된 엔티티의 스냅샷과 비교 → 변경된 부분이 있다면 업데이트 쿼리를 만듭니다.  
4. 지연 로딩
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">N+1 문제가 뭔가요?</strong></summary>

```text
N+1 문제란, 1번의 쿼리를 날렸을 때, 의도하지 않은 N번의 쿼리가 추가적으로 실행되는 것을 말합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">JPA의 N+1 문제 해결 방법과 각 방법의 단점</strong></summary>

```text
1. @BatchSize
   - 해결 방법: 연관 엔티티를 IN 쿼리를 통해 일정 크기의 배치로 조회
   - 장점: 지정된 크기만큼의 연관 엔티티를 IN절로 한 번에 조회해서 N+1문제를 해결
   - 단점: 
     - 최적의 배치 크기를 찾기 어려움
     - 통일되게 배치사이즈를 정하면, 필요없는 쿼리가 발생하거나 필요없는 데이터까지 조회합니다

2. Native SQL 사용
   - 해결 방법: JPA 대신 Native SQL을 사용하여 최적화된 쿼리 작성
   - 장점: 데이터베이스에 최적화된 쿼리 사용 가능
   - 단점: 
     - JPA의 장점 (객체 지향적 접근, 데이터베이스 독립성) 상실
     - SQL에 의존적인 코드 증가
     
3. @Fetch(FetchMode.SUBSELECT)
   - 연관된 엔티티들을 조회할 때 서브쿼리를 사용합니다.
   - 장점: N+1 문제를 효과적으로 해결할 수 있습니다.
          Fetch Join과 달리 페이징과 함께 사용할 수 있습니다.
   - 단점: 
     - 항상 연관 엔티티를 모두 가져오므로, 필요하지 않은 경우에도 데이터를 로드할 수 있습니다.
     - 대량의 데이터를 다룰 때는 메모리 사용량에 주의해야 합니다.
     
4. Fetch Join (페치 조인) 과 @EntityGraph
   - 해결 방법: JPQL의 JOIN FETCH 또는 EntityGraph를 사용하여 연관 엔티티를 함께 조회
   - 장점: 한 번의 쿼리로 연관 엔티티를 모두 가져옴
   - 단점: 
     - 1:N 관계에서 페이징 처리가 어려움 
     - 여러 컬렉션을 페치 조인하면 카테시안 곱이 발생하여 데이터 중복 증가 (Set으로 해야하거나 단, 순서 잘못,컬렉션 하나만 페치조인,쿼리분리) 
```


</details>

---

<details>
<summary><strong style="font-size:1.17em">페치조인의 1:N 관계에서 페이징 처리가 왜 어렵죠?</strong></summary>

```text
OneToMany 관계에서 Fetch Join과 페이징을 함께 사용할 경우 문제가 발생합니다. 
이 경우 JPA는 LIMIT과 OFFSET을 무시하고 모든 데이터를 메모리에 로드한 후 애플리케이션 레벨에서 페이징을 수행합니다. 
이는 대용량 데이터 처리 시 Out of Memory(OOM) 오류를 야기할 수 있습니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">왜 LIMIT와 OFFSET을 무시하나요?</strong></summary>

```text
OneToMany 관계에서 Fetch Join을 사용하면 데이터베이스 결과 집합에 중복된 행이 포함될 수 있습니다.

중복된 행으로 인해 LIMIT와 OFFSET을 데이터베이스 수준에서 적용하면 예상치 못한 결과가 나올 수 있습니다.
예를들어, LIMIT 10을 적용했을 때 실제로는 2-3개의 '일(One)' 쪽 엔티티만 포함될 수 있습니다.

이러한 문제를 방지하기 위해 JPA는 OneToMany Fetch Join에서 LIMIT와 OFFSET을 무시합니다.
대신 모든 데이터를 메모리로 로딩한 후, 애플리케이션 레벨에서 중복을 제거하고 페이징을 수행합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">일대일 매핑에서 주의해야할 점이 뭔가요?</strong></summary>

```text
- 객체의 단방향 관계가 주(Main) 엔티티에서 대상(Target) 엔티티로 향할 때, 
데이터베이스에서 대상 테이블에 외래 키를 두는 구조는 지원되지 않습니다

- 연관관계의 주인이 아닌 쪽에서 주인인 엔티티를 조회 시 지연 로딩이 동작하지 않고 즉시로딩으로 작동됩니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">지연로딩으로 설정했는 데 왜 즉시로딩이되나요?</strong></summary>

```text
프록시의 한계 때문입니다. 
OneToOne 관계에서 연관관계 주인인 쪽에서 조회시, 
지연로딩할때 외래키로 연관맺은 객체의 아이디를 얻을 수 있고, 프록시를 생성할 수 있습니다.

반면, 연관관계 주인이 아닌 객체는 외래키가 없기 때문에 연관객체의 존재여부를 파악할 수가 없습니다. 
이 상태로 프록시를 생성하기에는 null값을 처리하는 등 모호한 부분이 있어서 불가능하다 판단하에 조회쿼리를 결국 날려서 즉시로딩방식으로 진행합니다. 
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">그럼 OneToMany에서는 이러한 현상이 발생하지 않나요?</strong></summary>

```text
일(1)에 해당하는 엔티티의 다(N) 에 해당하는 연관 관계 필드는 컬렉션 타입입니다.
지연 로딩을 적용할 때 엔티티에 컬렉션이 있으면 컬렉션을 추적하고 관리할 목적으로 하이버네이트는 컬렉션 래퍼(PersistentBag)라는 것을 제공합니다.
이것이 컬렉션에 대한 프록시 역할을 합니다. 
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">JPA 1차 캐시 , 2차 캐시 차이점이 뭔가요?</strong></summary>

```text
1차 캐시는 영속성 컨텍스트 내부에 위치하며, 트랜잭션 범위에서 동작합니다.
주요 이점은 동일 트랜잭션 내에서 반복 조회 시 1차 캐시에 담겨있던 엔티티를 넘겨, 데이터베이스 접근을 줄여 성능을 향상시킵니다. 

2차캐시는 애플리케이션 전체에서 공유되는 캐시입니다. 
2차 캐시는 조회한 객체를 그대로 반환하는 것이 아니라 복사본을 반환합니다.
주로 자주 변경되지 않는 데이터에 효과적입니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">하이버네이트의 Cache 어노테이션의 속성에 대해 설명해주세요</strong></summary>

```text
usage: 캐시 동시성 전략을 지정합니다 (NONE, READ_ONLY, NONSTRICT_READ_WRITE, READ_WRITE, TRANSACTIONAL)

- NONE: 전략이 없습니다.
- READ_ONLY: 읽기 전용입니다. 불변값에 적합합니다.
- NONSTRICT_READ_WRITE: 
    동작 방식: 읽기 작업은 캐시에서 직접 데이터를 읽습니다. 쓰기 작업은 데이터베이스에 먼저 쓰고, 그 후 캐시를 갱신합니다.
    특징: 동시성 제어가 엄격하지 않습니다. 짧은 시간 동안 캐시와 데이터베이스 간 불일치가 발생할 수 있습니다.
- READ_WRITE: 
    읽기 작업은 캐시에서 데이터를 읽되, 매번 유효성을 검사합니다. 쓰기 작업은 데이터베이스와 캐시를 동시에 갱신하며, 락(lock)을 사용합니다.
    동시성 제어가 엄격합니다 그리고 캐시와 데이터베이스의 일관성을 항상 유지합니다. 단, 클러스터 환경에서는 사용하면 안됩니다.
- TRANSACTIONAL: JTA 환경에서 사용됩니다. 

region: 캐시 영역의 이름을 지정할 수 있습니다. 이름을 달리 주어, 각 리전마다 다른 캐시 전략을 구축할 수 있습니다.

include 속성은 엔티티의 관계(연관)들을 어떻게 캐시할지 지정합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">왜 분산환경에서 READ_WRITE 보다 NONSTRICT_READ_WRITE를 사용해야 하나요?</strong></summary>

```text
READ_WRITE는 동기화 처리 때문에 성능에 문제가 있습니다. 
그리고 분산 환경에서 캐시에 대한 동기화처리를 한다고 해도 DB에서는 디비에 대한 락킹이 아니기 때문에 일관성 보장이 안될수 있습니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">스프링에서 지원하는 캐시에 대해 설명해주세요</strong></summary>

```text
- 캐시 구현 기술에 종속되지 않도록 추상화 기술인 PSA 를 제공합니다. (CacheManager)
- AOP를 통해 적용하기 때문에 애플리케이션 코드를 수정하지 않고, 캐시 부가 기능을 추가할 수 있습니다.
- 구현체로는 카페인,EhCache, Redis 등등이 있으며 로컬 캐시 혹은 글로벌 캐시로 사용가능합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">로컬 캐시와 글로벌 캐시 차이점이 뭐죠?</strong></summary>

```text
- Local Cache

서버마다 캐시를 따로 저장한다.
다른 서버의 캐시를 참조하기 어렵다.
대신 서버 내에서 작동하기 때문에 속도가 빠르다.
로컬 서버 장비의 Resource를 이용한다. (Memory, Disk)

만약 캐시에 저장된 데이터가 변경되는 경우 정합성을 맞추기 위해 
해당 서버를 제외한 모든 peer에 변경 사항 전달해야하기 때문에 
WAS 인스턴스가 늘어나고, 캐시 저장 데이터 크기가 커지면 성능이 저하됩니다.

- Global Cache

여러 서버에서 캐시 서버에 접근하여 참조 할 수 있습니다.
별도의 캐시 서버를 이용하기 때문에 서버 간 데이터 공유가 쉽습니다.
네트워크 트래픽을 사용해야 해서 로컬 캐시보다는 느리다.
데이터를 분산하여 저장 할 수 있습니다. 
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">2차 캐시를 현업에서 잘 안쓰는 이유가 뭔가요?</strong></summary>

```text
설정이 복잡하고, 지원하는 캐시 라이브러리도 적습니다.(EhCache, Infinispan 등) 

또한, 외부 API를 조회하고 여러 엔티티를 조회하면서 DTO를 생성할텐데 2차캐시는 엔티티만 캐시가 지원됩니다.
그래서 보통 스프링이 지원하는 캐시를 사용하여 DTO를 저장하고 다양한 라이브러리 예를들면 Redis등을 사용할 수가 있습니다. 

다중서버환경에서는 로컬 캐시보다는 글로벌 캐시를 사용합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">하이버네이트가 제공하는 2차 캐시는 무엇이 있나요</strong></summary>

```text
해당 캐시는 크게 3가지를 지원합니다.

엔티티 캐시 : 엔티티 단위로 캐시한다.
컬렉션 캐시 : 엔티티와 연관된 컬렉션을 캐시한다. 컬렉션이 엔티티를 담고 있으면 식별자 값만 캐시한다.
쿼리 캐시 : 쿼리와 파라미터 정보를 키로 사용해서 캐시한다. 결과가 엔티티면 식별자 값만 캐시한다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">엔티티 매니저는 thread-safe 한가요? == EntityManger는 thread-safe 해야 할까요?</strong></summary>

```text
EntityManager는 thread-safe 하지 않습니다.
그리고 의도적으로 그렇게 설계되었습니다.

왜냐면
스프링에서는 트랜잭션 단위로 엔티티매니저를 생성하고
스레드로컬을 사용하여 스레드 당 하나의 엔티티매니저를 보장합니다.

따라서 엔티티매니저가 스레드세이프하지 않은것은 
장점이 됩니다. 그 이유는 동기화할 필요가 없어 오버헤드도 없고
데이터 정합성을 보장하기에도 쉽습니다. 
```
</details>

---

<details>
<summary><strong style="font-size:1.17em">JPQL과 SQL의 차이점이 뭔가요?</strong></summary>

```text
- 테이블이 아닌 객체를 검색하는 객체지향 쿼리
- SQL을 추상화 했기 때문에 특정 DB에 종속적이지 않음
- JPA는 JPQL을 분석하여 SQL을 생성한 후 DB에서 조회
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">JPQL의 특징</strong></summary>

```text
- 엔티티와 속성은 대소문자를 구분합니다.
- JPQL에서 엔티티의 별칭은 필수적으로 명시해야 합니다. (별칭을 명시하는 AS 키워드는 생략해도 자동으로 부여됩니다 )
- DTO로 객체 반환 받을 수 있습니다.
- 파라미터 바인딩도 가능합니다.  
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">쿼리DSL과 크리테리아 API의 차이점이 뭔가요</strong></summary>

```text
Criteria는 컴파일 시점에 에러를 잡아주는 장점이 있습니다. 
JPQL 처럼 String으로 쿼리를 작성하지 않아도 되고, 객체로 코드를 작성합니다.

하지만 이 CriteriaBuilder를 통해서 쿼리를 만들면 
실제 작성해야 하는 SQL 쿼리보다 훨씬 많은 양의 코드를 작성해야 합니다. 
또한 코드가 장황해지다 보니 가독성이 떨어지면서 실제로 어떤 쿼리가 생성되는 것인지 한눈에 파악하기 어렵습니다.

쿼리DSL은 Criteria의 단점이 없어지고, JPQL과 비슷해서 한 눈에 들어옵니다.
QueryDSL은 JPA 표준은 아니고 오픈소스 프로젝트입니다.
쿼리 대로 날라가기 때문에 예상치 못한 쿼리가 날라가 N+1문제 안생깁니다.
또한, 동적쿼리로 조건에 따라 다른 쿼리를 만들 수 있습니다. 
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">캐스케이드 영속성전이 와 orphan removal 차이를 설명해주세요</strong></summary>

```text
- CascadeType.REMOVE와 orphanRemoval = true는 부모 엔티티를 삭제하면 자식 엔티티도 삭제합니다.
- 부모 엔티티에서 자식 엔티티 제거할때는 CascadeType.REMOVE는 자식 엔티티가 그대로 남아있는 반면, orphanRemoval = true는 자식 엔티티를 제거합니다.
- OrphanRemoval 만 있는 것은 동작안합니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">하이버네이트의 세션이란 뭔가요?</strong></summary>

```text
- 세션 객체는 응용 프로그램과 데이터베이스에 저장된 데이터 간의 인터페이스를 제공
- 수명이 짧은 객체이며 JDBC 커넥션을 래핑합니다. 
- 데이터의 1차 캐시 (필수)를 보유합니다.
- org.hibernate.Session 인터페이스는 객체를 삽입, 갱신, 삭제하는 메소드를 제공
- Transaction, Query 및 Criteria에 대한 팩토리 메소드를 제공합니다.
- 참고로 세션팩토리는 2차 캐시를 선택적으로 보유및 관리합니다. 세션팩토리는 싱글톤 객체로, 여러 세션간에 공유됩니다.  
```


</details>

---

<details>
<summary><strong style="font-size:1.17em">HQL이란 뭔가요?</strong></summary>

```text
Hibernate를 통해 데이터베이스를 검색할 경우에 이용하는 쿼리입니다.
 
Hibernate가 어떤 데이터베이스를 이용하고 있는지 살펴보고 
알아서 HQL을 그에 맞는 SQL 로 변환하여 준다는 장점이 있습니다.

```

</details>

---

<details>
<summary><strong style="font-size:1.17em">entityManager랑 session이랑 뭔차이인가요?</strong></summary>

```text
EntityManager: JPA(Java Persistence API)의 표준 인터페이스입니다.
Session: Hibernate의 고유한 인터페이스로, JPA 표준을 확장한 것입니다.

따라서 
Session은 EntityManager의 모든 기능을 포함하며, 추가적인 Hibernate 특화 기능을 제공합니다.

또한 EntityManager의 Hibernate 구현체는 내부적으로 Session을 가지고 있어서,
필요할 때 unwrap()을 통해 Session을 얻을 수 있습니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">Spring Data JPA와 일반 JPA의 차이점을 말해주세요</strong></summary>

```text
스프링 데이터는 다양한 데이터 저장소에 대한 데이터 액세스를 단순화하고 통일된 방식으로 제공하는 프로젝트입니다. 

예를들어 Pageable객체로 페이징과 정렬, 메소드 이름으로 쿼리 생성, CRUD 메소드 제공, 
Repository 인터페이스를 정의하면 구현체를 자동 생성 등 개발자가 쉽게 사용할 수 있습니다. 

일반 JPA는 모든 메서드를 직접 구현하고, EntityManager를 직접 다뤄야 합니다. 
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">스프링 데이터 JPA 말고 다른 스프링 데이터 차이점</strong></summary>

```text
스프링 데이터 JPA
스프링 데이터 JDBC : @Query 어노테이션을 사용하여 직접 SQL을 작성
스프링 데이터 MongoDB : 메소드 이름으로 쿼리를 생성
스프링 데이터 Redis :  RedisTemplate을 사용하여 키-값 데이터를 저장하고 검색합니다.
스프링 데이터 Elasticsearch : 전문 검색을 위한 메소드를 정의합니다.
```

</details>

---



