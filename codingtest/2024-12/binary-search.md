## 문제 1

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
