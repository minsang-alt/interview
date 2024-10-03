## AgileHub

### 애자일 방법론이 뭐죠?

### from에 서브쿼리를 사용했는 데 왜 조회속도가 단축되었나요?

### QueryDsl이 from 절 사용이 불가능하다고 했는데 다른 해결 방법이 있는데 혹시 아시나요?

```text
- id검색 쿼리, 조회쿼리를 나눠서 실행합니다. 단, 이는 대용량 데이터를 조회할 때 DB마다의 MAX된 IN절 제한으로 불가능할 수도 있습니다.
- 네이티브쿼리, JDBC Template
- QueryDSL의 JPASQLQuery를 사용하여 네이티브 SQL과 유사한 기능을 구현할 수 있습니다. 
  단, from절 sub-query외부에서는 QClass의 형태로 참조가 불가능합니다.
```

### 네이티브 쿼리와 projection이 뭐죠?



