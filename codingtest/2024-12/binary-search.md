
---

<details>
<summary><strong style="font-size:1.17em">Search in Rotated Sorted Array</strong></summary>

문제링크: https://leetcode.com/problems/search-in-rotated-sorted-array/description/?envType=problem-list-v2&envId=binary-search&difficulty=MEDIUM%2CEASY

### Search in Rotated Sorted Array

네, "Search in Rotated Sorted Array" 문제의 핵심 아이디어를 더 깊게 설명해드리겠습니다.

1. **회전된 배열의 특징**
```
원래 배열:    [0, 1, 2, 4, 5, 6, 7]
회전된 배열:   [4, 5, 6, 7, 0, 1, 2]
```
- 중요한 점은 회전된 배열에서도 **항상 한쪽은 정렬되어 있다**는 것입니다
- 어떤 지점을 잡더라도, 왼쪽 또는 오른쪽 중 하나는 반드시 정렬되어 있습니다

2. **정렬된 부분 찾기**
```
[4, 5, 6, 7, 0, 1, 2]
 L     M        R
```
- mid 값과 left 값을 비교하여 왼쪽이 정렬되어 있는지 확인:
    - nums[left] <= nums[mid]: 왼쪽이 정렬됨
    - 그렇지 않으면: 오른쪽이 정렬됨

3. **왼쪽이 정렬된 경우의 예시**
```
[4, 5, 6, 7, 0, 1, 2]
 L     M        R
```
- nums[left] <= nums[mid]이므로 왼쪽 [4,5,6,7]은 정렬되어 있음
- target이 4와 7 사이에 있다면 오른쪽 부분은 볼 필요가 없음
- target이 이 범위를 벗어나면 오른쪽을 봐야 함

4. **오른쪽이 정렬된 경우의 예시**
```
[6, 7, 0, 1, 2, 4, 5]
 L     M        R
```
- nums[left] > nums[mid]이므로 오른쪽 [1,2,4,5]가 정렬되어 있음
- target이 1과 5 사이에 있다면 왼쪽 부분은 볼 필요가 없음
- target이 이 범위를 벗어나면 왼쪽을 봐야 함

5. **실제 동작 예시**
   target = 0을 찾는 경우:
```
Step 1: [4, 5, 6, 7, 0, 1, 2]
         L     M        R
- 왼쪽이 정렬됨 [4,5,6,7]
- 0은 이 범위에 없음 -> 오른쪽으로 이동

Step 2: [4, 5, 6, 7, 0, 1, 2]
                  M     R
- 오른쪽이 정렬됨 [0,1,2]
- 0은 이 범위에 있음 -> 찾음!
```

6. **경계 조건들**:
- 배열의 길이가 0인 경우
- 배열의 길이가 1인 경우
- target이 배열의 최소값보다 작은 경우
- target이 배열의 최대값보다 큰 경우

이 알고리즘이 효율적인 이유:
1. 항상 절반을 제거할 수 있음 (O(log n))
2. 추가 공간이 필요하지 않음 (O(1) 공간)
3. 한 번의 순회로 결과를 찾을 수 있음

이렇게 정렬된 부분을 활용하여 이진 탐색을 수행하는 것이 이 문제의 핵심 아이디어입니다. 기존의 이진 탐색을 회전된 배열에 맞게 약간 수정한 것이라고 볼 수 있습니다.


### 코드

```java
class Solution {
    public int search(int[] nums, int target) {
        
        if(nums == null || nums.length==0){
            return -1;
        }

        int left = 0;
        int right = nums.length-1;
        
        while(left <= right){
            int mid = left + (right-left)/2;

            // 중간값과 타겟이 같다면 반환
            if(nums[mid] == target){
                return mid;
            }

            // 왼쪽이 정렬되어있을 경우
            if(nums[left] <= nums[mid]){
                //그리고 타겟이 왼쪽 정렬에 있을 경우
                if(nums[left] <= target && nums[mid] > target){
                    right = mid-1;
                }else{
                    left = mid+1;
                }
            }else{

                // 타겟이 오른쪽 정렬에 있을 경우
                if(nums[mid]< target && target <= nums[right]){
                    left = mid+1;
                }else{
                    right = mid-1;
                }
            }
        }

        return -1;
        
    }
}
```

</details>


---

<details>
<summary><strong style="font-size:1.17em">Find First and Last Position of Element in Sorted Array</strong></summary>

https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/description/?envType=problem-list-v2&envId=binary-search&difficulty=MEDIUM%2CEASY

```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int[] result = {-1,-1};
        // 엣지 케이스 처리
        if(nums == null || nums.length == 0 ) return result;

        // 여기에 로직을 구현하겠습니다.
        result[0] = findPosition(nums, target, true);

        if(result[0] != -1){
            result[1] = findPosition(nums, target, false);
        }


        return result;
    }
    
    
    private int findPosition(int[] nums, int target, boolean isFirst){
        int left = 0;
        int right = nums.length -1;
        int position = -1;

        while(left <= right){
            int mid = left + (right-left)/2;

            // 중간값이 target값과 같을때
            if(nums[mid] == target){
                //먼저 해당 위치 저장
                position = mid;

                //만약 isFirst 즉, 첫 위치를 찾는거면 
                if(isFirst){
                    right = mid-1;
                }else{
                    left = mid+1;
                }
            }else if(target < nums[mid]){
                right = mid -1;
            }else{
                left = mid + 1;
            }

        }

        return position;
    }


}
```

</details>


---

<details>
<summary><strong style="font-size:1.17em">Search a 2D Matrix</strong></summary>

https://leetcode.com/problems/search-a-2d-matrix/description/?envType=study-plan-v2&envId=binary-search

이해하기 어려운 부분을 차근차근 설명해드리겠습니다.

2D 행렬(matrix)에서 특정 원소의 위치를 찾는 방법에 대한 설명이었는데요. 예시를 들어 설명해보겠습니다:

```python
matrix = [
    [1,  2,  3,  4],
    [5,  6,  7,  8],
    [9, 10, 11, 12]
]
```

이런 3x4 행렬이 있다고 해봅시다. 여기서 각 숫자의 위치를 1차원 인덱스로 나타내면:
- 1은 인덱스 0
- 2는 인덱스 1
- 5는 인덱스 4
- 6은 인덱스 5
  이런 식입니다.

이제 1차원 인덱스(i)에서 행과 열의 위치를 구하는 방법은:
1. 행 번호 = i ÷ 열의 개수 (몫)
2. 열 번호 = i ÷ 열의 개수 (나머지)

예를 들어 숫자 6의 위치(인덱스 5)를 구해보면:
- 열의 개수는 4
- 행 번호 = 5 ÷ 4 = 1 (몫)
- 열 번호 = 5 ÷ 4 = 1 (나머지)
  따라서 6은 [1][1] 위치에 있습니다.

이런 방식으로 계산하는 이유는 행렬에서 한 행이 끝나면 다음 행으로 넘어가기 때문입니다. 열의 개수로 나누면 몫은 몇 번째 행인지, 나머지는 그 행에서 몇 번째 열인지를 알려주게 됩니다.

이걸 더 직관적으로 이해해보겠습니다.

위의 3x4 행렬을 일렬로 나열해보면 이렇게 됩니다:

```
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]
 0  1  2  3  4  5  6  7  8  9  10  11  (인덱스)
```

여기서 중요한 패턴이 있습니다:
- 첫 번째 행: 인덱스 0,1,2,3
- 두 번째 행: 인덱스 4,5,6,7
- 세 번째 행: 인덱스 8,9,10,11

보시면 각 행은 4(열의 개수)개씩 묶여있죠.

이제 예를 들어 인덱스 6의 위치를 찾아봅시다:
- 6 ÷ 4 = 1 남은 2
- 몫이 1이라는 건 "4개씩 묶었을 때 1개의 묶음이 완전히 지나갔다"는 뜻입니다
    - 즉, 첫 번째 행을 지나 두 번째 행에 있다는 의미
- 나머지가 2라는 건 "현재 행에서 2번째 위치"라는 뜻입니다

다른 예시로 인덱스 11을 보면:
- 11 ÷ 4 = 2 남은 3
- 몫이 2: "4개씩 두 묶음이 지나감" = 세 번째 행
- 나머지가 3: "현재 행에서 3번째 위치"

이렇게 열의 개수로 나누면:
1. 몫은 "몇 개의 완전한 행이 지나갔는지" = 현재 행 번호
2. 나머지는 "현재 행에서의 위치" = 열 번호

를 자연스럽게 알려주게 되는 것입니다.

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int m = matrix.length;
        int n = matrix[0].length;

        int left = 0;
        int right = (m*n)-1;

        while(left <= right){
            int mid = left + (right-left)/2;

            if(matrix[mid/n][mid%n] == target){
                return true;
            }else if(matrix[mid/n][mid%n] < target){
                left = mid+1;
            }else{
                right = mid-1;
            }


        }

        return false;
        
    }
}
```
</details>

---

<details>
<summary><strong style="font-size:1.17em">Binary Search</strong></summary>

https://leetcode.com/problems/binary-search/description/?envType=study-plan-v2&envId=binary-search

```java
class Solution {
    public int search(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;

        while(left <= right){
            int mid = left + (right-left)/2;

            if(nums[mid] == target){
                return mid;
            }else if(nums[mid] > target){
                right = mid-1;
            }else{
                left = mid+1;
            }
        }

        return -1;
    }
}
```

</details>
