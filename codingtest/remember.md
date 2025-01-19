## 이진탐색 

**1. while 조건: `left <= right` vs `left < right`**

- `left <= right`를 사용할 때:
```java
while(left <= right) {
    int mid = left + (right-left)/2;
    if(arr[mid] == target) return true;
    if(arr[mid] < target) left = mid + 1;
    else right = mid - 1;
}
```
- 배열의 모든 원소를 하나하나 확인하고 싶을 때 사용
- 종료조건: left > right가 되면 종료
- 특징: `right = mid - 1`, `left = mid + 1` 사용

- `left < right`를 사용할 때:
```java
while(left < right) {
    int mid = left + (right-left)/2;
    if(arr[mid] == target) return true;
    if(arr[mid] < target) left = mid + 1;
    else right = mid;
}
```
- 범위를 좁혀가면서 "하나"의 답을 찾고 싶을 때 사용
- 종료조건: left == right가 되면 종료
- 특징: `right = mid`, `left = mid + 1` 사용

**2. 쉽게 기억하는 방법**

1. 일반적인 이진 탐색(특정 값 찾기)
   ```java
   while(left <= right) {
       // mid와 target이 같으면 바로 반환
       // left = mid + 1
       // right = mid - 1
   }
   ```

2. 최소값 찾기(Lower Bound)
   ```java
   while(left < right) {
       // mid와 target 비교
       // left = mid + 1
       // right = mid
   }
   ```

**3. 예시로 이해하기**
```java
arr = [1, 2, 3, 4, 5]
target = 3
```

`left <= right` 경우:
1. left=0, right=4, mid=2 (값:3) → 찾음!
2. 만약 못 찾았다면 left > right가 될 때까지 계속 검색

`left < right` 경우:
1. left=0, right=4, mid=2 (값:3)
2. 종료조건이 left == right이므로, 구간이 하나로 좁혀질 때까지 검색

현재 문제에서는 정확한 값을 찾아야 하므로 `left <= right`가 더 적절합니다!