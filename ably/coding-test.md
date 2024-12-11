
## 문자열 압축 문제

<details>
<summary><strong style="font-size:1.17em">문자열 압축 문제</strong></summary>

```text
긴 단어들을 압축하여 기억하기 쉽게 만들기 위해 몇 가지 작업을 수행하려고 합니다.
그 중 하나는 k개의 연속된 동일한 문자 그룹을 선택하여 제거하는 것입니다. 
이 작업을 더 이상 수행할 수 없을 때까지 반복합니다.
모든 작업이 완료된 후의 최종 단어를 구하는 compressWord 함수를 작성하세요

함수의 매개변수:
- string word: 소문자로 이루어진 영어 문자열
- int k: 연속된 동일 문자 개수 

함수의 반환값:
string: 최종 단어를 나타내는 문자열

제약 조건 1 <= |word| <= 10의 5승

설명
- 최종 단어는 반드시 하나 이상의 문자를 포함합니다 

예시 1.
word = "abbcccb", k = 3
-> "a"
```

## char 배열

```java
public static String compressWord(String word, int k) {
    // 결과 문자들을 저장할 배열
    char[] result = new char[word.length()];
    // 각 문자의 연속 등장 횟수를 저장할 배열
    int[] count = new int[word.length()];
    // 현재까지 처리된 문자의 위치를 가리키는 포인터
    int top = 0;

    // 입력 문자열의 각 문자를 순회하며 처리
    for (char c : word.toCharArray()) {
        // 스택이 비어있거나 이전 문자와 현재 문자가 다른 경우
        if (top == 0 || result[top - 1] != c) {
            // 새로운 문자를 스택에 추가하고 카운트를 1로 초기화
            result[top] = c;
            count[top] = 1;
            top++;
        }
        // 이전 문자와 현재 문자가 같은 경우
        else {
            // 해당 문자의 카운트를 증가
            count[top - 1]++;
            // 카운트가 k에 도달하면 해당 문자 그룹을 제거
            if (count[top - 1] >= k) {
                top--;
            }
        }
    }

    // 최종 결과 문자열 생성
    StringBuilder sb = new StringBuilder();
    // 각 문자를 해당 카운트만큼 반복하여 추가
    for (int i = 0; i < top; i++) {
        for (int j = 0; j < count[i]; j++) {
            sb.append(result[i]);
        }
    }
    return sb.toString();
}
```

</details>


---

<details>
<summary><strong style="font-size:1.17em">시간복잡도와 공간복잡도는 어떻게 되나요?</strong></summary>

```text
시간 복잡도는 문자열을 한 번만 순회하므로 O(n)입니다. 
공간 복잡도도 입력 문자열 길이만큼의 배열만 사용하므로 O(n)입니다. 

StringBuilder를 사용한 것도 공간 효율성을 고려한 선택이었습니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">왜 스택 기반의 접근방식을 선택하셨나요?</strong></summary>

```text
연속된 문자를 처리하고 더 이상 수행할 수 없을 때까지 반복하면서 제거해야 하는 문제의 특성상 
스택이 가장 적합했습니다.
 
특히 k개의 연속된 문자를 제거할 때 스택을 사용하면 이전 상태로 쉽게 돌아갈 수 있기 때문입니다.
```

</details>


---

<details>
<summary><strong style="font-size:1.17em">예외적인 상황에 대한 처리는 어떻게 하셨나요?</strong></summary>

```text
현재 구현에서는 기본적인 입력 제약 조건(문자열 길이 제한 등)을 가정했지만, 
실제 프로덕션 환경에서는 입력값 검증(null 체크, 길이 검증 등)을 추가할 수 있습니다
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">다른 방식으로도 이 문제를 해결할 수 있었을까요?</strong></summary>

```text
처음에는 Queue를 사용한 접근방식을 시도했습니다. 
이유는

문자를 순차적으로 처리하는 FIFO 특성이 문제와 잘 맞는다고 생각했고
Pair 클래스를 만들어서 문자와 카운트를 함께 관리하면 직관적일 것이라 판단했기 때문입니다.

하지만 이 접근방식에는 몇 가지 문제가 있었습니다

Queue 연산과 객체 생성으로 인한 오버헤드가 발생
문자열 처리 과정에서 불필요한 객체 생성이 많이 발생
매 단계마다 큐의 원소들을 재확인하는 과정이 필요해 시간복잡도가 O(n2)증가했습니다.
```

</details>


---


## 정렬 문제

---

<details>
<summary><strong style="font-size:1.17em">커스텀 정렬 문제</strong></summary>


```text
다음 커스텀 정렬 알고리즘은 n개의 서로 다른 정수로 구성된 배열을 정렬하는 데 사용됩니다.

커스텀 정렬 알고리즘

크기가 n인 입력 배열 arr에 대해
다음과 같은 가장 작은 인덱스 쌍 0 <= i < j < n-1을 찾습니다.
arr[i]와 arr[j]를 교환하고 다음 쌍을 찾습니다.
만약 그러한 쌍이 없다면 중단합니다.

여기서 가장 작은 인덱스 쌍이란, (index1, index2) < (index3, index4)는 아래
두 조건 중 적어도 하나를 만족합니다.

index1 < index3 혹은
index1 = index3 이면서 index2 < index4

이 정렬 알고리즘 정확성엔 문제가 없지만, 몇번의 교환을 하는지 알고싶습니다.
총 교환 횟수를 반환하는 함수 howManySwaps를 작성하세요.

예시
arr = [5,1,4,2]
- > 4
```

5,1,4,2

```java
import java.util.*;

class Result {
    // 전체 교환 횟수를 저장할 전역 변수
    private static long swapCount = 0;
    
    public static long howManySwaps(List<Integer> arr) {
        // 교환 횟수 초기화
        swapCount = 0;
        // List를 배열로 변환 (배열이 더 빠른 접근 가능)
        int[] nums = arr.stream().mapToInt(Integer::intValue).toArray();
        // 머지소트 시작 (0부터 배열 끝까지)
        mergeSort(nums, 0, nums.length - 1);
        return swapCount;
    }
    
    private static void mergeSort(int[] arr, int left, int right) {
        // 분할한 배열의 크기가 1보다 클 때만 계속 진행
        if (left < right) {
            // 중간 지점 계산
            int mid = (left + right) / 2;
            
            // 왼쪽 절반 정렬
            mergeSort(arr, left, mid);
            // 오른쪽 절반 정렬
            mergeSort(arr, mid + 1, right);
            
            // 정렬된 두 절반을 병합
            merge(arr, left, mid, right);
        }
    }
    
    private static void merge(int[] arr, int left, int mid, int right) {
        // 왼쪽 부분 배열 복사 [left ~ mid]
        int[] leftArr = Arrays.copyOfRange(arr, left, mid + 1);
        // 오른쪽 부분 배열 복사 [mid+1 ~ right]
        int[] rightArr = Arrays.copyOfRange(arr, mid + 1, right + 1);
        
        // 각 배열의 현재 위치를 가리키는 인덱스
        int i = 0;  // 왼쪽 배열 인덱스
        int j = 0;  // 오른쪽 배열 인덱스
        int k = left;  // 원본 배열에서 채워넣을 위치
        
        // 왼쪽과 오른쪽 배열의 크기
        int leftSize = mid - left + 1;
        int rightSize = right - mid;
        
        // 왼쪽과 오른쪽 배열을 비교하면서 병합
        while (i < leftSize && j < rightSize) {
            if (leftArr[i] <= rightArr[j]) {
                // 왼쪽 배열의 수가 더 작거나 같으면
                // 교환 필요 없이 그대로 넣음
                arr[k++] = leftArr[i++];
            } else {
                // 오른쪽 배열의 수가 더 작으면
                // 왼쪽 배열에 남아있는 모든 수가 현재 오른쪽 수보다 크므로
                // (leftSize - i)개의 교환이 필요
                arr[k++] = rightArr[j++];
                swapCount += (leftSize - i);
            }
        }
        
        // 왼쪽 배열에 남은 요소들 복사
        while (i < leftSize) {
            arr[k++] = leftArr[i++];
        }
        
        // 오른쪽 배열에 남은 요소들 복사
        while (j < rightSize) {
            arr[k++] = rightArr[j++];
        }
    }
}
```

</details>


---
<details>
<summary><strong style="font-size:1.17em">이 문제를 어떻게 해결했나요?</strong></summary>

```text
이 문제는 결국 배열에서 Inversion의 수를 세는 문제로 볼 수 있습니다. 
Inversion이란 배열에서 i < j일 때 arr[i] > arr[j]인 모든 쌍을 의미하는데, 
이는 정렬 과정에서 필요한 교환 횟수와 일치합니다.

이 문제를 해결하기 위한 접근 방법으로는
단순하게
모든 수에서 모든 수를 돌아보면되지만,
O(N^2)의 시간복잡도를 가지므로 비효율적입니다.

따라서 Merge Sort를 사용하여 Inversion을 세는 방법을 사용했습니다.
배열을 계속 반으로 나누고
병합하는 과정에서 Inversion을 계산합니다
왼쪽 배열의 원소가 오른쪽 배열의 원소보다 클 때, 
한 번에 여러 개의 Inversion을 찾을 수 있습니다
이 방법은 시간 복잡도를 O(nlogn)으로 개선할 수 있습니다

예를 들어, [5,1,4,2]에서
5는 1,4,2보다 크므로 3개의 Inversion
4는 2보다 크므로 1개의 Inversion
총 4번의 교환이 필요합니다


```

```java
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">swapCount += (leftSize - i) 부분은 뭔가요?</strong></summary>

```text
이 부분이 단순히 +1이 아닌 (leftSize - i)를 더하는 이유는 
머지 소트의 중요한 특성을 활용하기 때문입니다.

예를 들어 설명드리면
왼쪽 배열: [5,7] ,오른쪽 배열: [1,4]일때
이렇게 있을 때, 1과 5를 비교하는 순간 
1은 5보다 작고,
왼쪽 배열은 이미 정렬되어 있으므로, 
1은 5 뿐만 아니라 7보다도 작다는 것이 보장됩니다.

따라서 1은 [5,7] 모두와 교환이 필요하고,
 이는 (leftSize - i) = (2 - 0) = 2로 한 번에 계산할 수 있습니다. 
 매번 교환마다 +1을 하는 대신, 한 번의 비교로 여러 교환을 동시에 계산하는 것이죠.
```

</details>

