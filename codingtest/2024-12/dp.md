## 문제 1 ✅

<details>
<summary><strong style="font-size:1.17em">https://leetcode.com/problems/minimum-ascii-delete-sum-for-two-strings/?envType=study-plan-v2&envId=dynamic-programming</strong></summary>

```java

class Solution {
    public int minimumDeleteSum(String s1, String s2) {
        int m = s1.length();
        int n = s2.length();
        int[][] dp = new int[m+1][n+1];

        // s2의 문자를 순차적으로 삭제
        for(int i = 1; i <= n; i++){
            dp[0][i] = dp[0][i-1] + s2.charAt(i-1);
        }

        // s1의 문자를 순차적으로 삭제 
        for(int i = 1; i <= m; i++){
            dp[i][0] = dp[i-1][0] + s1.charAt(i-1);
        }

        for(int i = 1; i <= m; i++){
            for(int j = 1; j <= n; j++){
                char c1 = s1.charAt(i-1);
                char c2 = s2.charAt(j-1);
                
                
                if(c1 == c2){
                    // 문자가 같은 경우, 삭제할 필요가 없음 
                    dp[i][j] = dp[i-1][j-1];
                }else{
                    // 다를 경우, 둘 중 하나를 삭제
                    dp[i][j] = Math.min(dp[i-1][j] + c1, dp[i][j-1]+c2);
                }
            }
        }

        return dp[m][n];
    }
}
```

</details>

---

## Longest Increasing Subsequence

tails 배열 만듦 -> tails[i] = x: 길이가 i+1인 증가하는 부분 수열의 마지막 값이 x, 이 때 x는 가장 작은 값
예를들어 [4, 5, 6, 3] 이라면 tails[0]일때, 후보가 [4],[5],[6],[3]이 있지만 가장 작은 값인 3을 선택한다.
tails[1]일때, 후보가 [4,5], [4,6], [5,6] 이 있지만 마지막 값이 5가 가장 작으므로 5를 선택한다. 

이진탐색 + dp 사용 (O(nlogn))

하지만 위로는 못푸니 O(n^2)방식으로 푸는 문제도 있다.

---

<details>
<summary><strong style="font-size:1.17em">Longest Increasing Subsequence</strong></summary>

https://leetcode.com/problems/longest-increasing-subsequence/solutions/74824/java-python-binary-search-o-nlogn-time-with-explanation/?envType=study-plan-v2&envId=dynamic-programming

```java
class Solution {
    public int lengthOfLIS(int[] nums) {
        if(nums == null || nums.length == 0){
            return 0;
        }

        int[] tails = new int[nums.length];
        int len = 0;

        for(int num : nums){
            int left = 0;
            int right = len;

            while(left < right){
                int mid = left + (right-left)/2;
                if(tails[mid] < num){
                    left = mid +1;
                }else{
                    right = mid;
                }

            }

            tails[left] = num;
            if(left == len){
                len++;
            }
        }


        return len;
    }
}
```


</details>


---

<details>
<summary><strong style="font-size:1.17em">Number of Longest Increasing Subsequence</strong></summary>

https://leetcode.com/problems/number-of-longest-increasing-subsequence/description/?envType=study-plan-v2&envId=dynamic-programming

가장 긴 증가하는 부분 수열(LIS)의 개수를 찾는 문제는 다음과 같이 접근할 수 있습니다:

1. 두 개의 DP 배열이 필요합니다:
    - `length[]`: 각 인덱스에서 끝나는 LIS의 길이
    - `count[]`: 각 인덱스에서 끝나는 LIS의 개수

2. 핵심 아이디어:
   ```java
   // 예시 구현의 기본 틀
   for (int i = 0; i < nums.length; i++) {
       for (int j = 0; j < i; j++) {
           if (nums[i] > nums[j]) {
               // 여기서 length[i]와 count[i]를 업데이트
           }
       }
   }
   ```

3. 각 위치에서:
    - 현재 숫자보다 작은 이전 숫자들을 찾습니다
    - 그 중에서 가장 긴 증가 수열을 만들 수 있는 길이를 찾습니다
    - 같은 길이의 수열이 여러 개 있을 수 있으므로, 그 개수도 함께 세야 합니다

예를 들어 `[1,3,5,4,7]`의 경우:
- `[1,3,5,7]`과 `[1,3,4,7]` 두 개의 서로 다른 최장 증가 수열이 있습니다
- 따라서 답은 2가 됩니다

```java
class Solution {
    public int findNumberOfLIS(int[] nums) {
        int[] length = new int[nums.length];
        int[] count = new int[nums.length];

        Arrays.fill(length,1);
        Arrays.fill(count,1);

        for(int i = 1; i < nums.length; i++){
            for(int j = 0; j <i; j++){
                if(nums[j] < nums[i]){
                    // 수열의 긴 개수가 업데이트 될때는 카운트 초기화
                    if(length[j]+1 > length[i]){
                        length[i] = length[j]+1;
                        count[i] = count[j];
                    }else if(length[j]+1 == length[i]){
                        // 카운트개수만 이전꺼에서 증가
                        count[i] += count[j];
                    }
                }
            
            }
        }


        int maxLength = 0;

        for(int len : length){
            maxLength = Math.max(maxLength,len);
        }

        int result = 0;
        for(int i = 0; i< nums.length; i++){
            if(maxLength == length[i]){
                result += count[i];
            }
        }

        return result;

    }
}
```

</details>
