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

이진탐색 + dp 사용

### 문제 2 ✅

<details>
<summary><strong style="font-size:1.17em">https://leetcode.com/problems/longest-increasing-subsequence/solutions/74824/java-python-binary-search-o-nlogn-time-with-explanation/?envType=study-plan-v2&envId=dynamic-programming</strong></summary>

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


