
---

<details>
<summary><strong style="font-size:1.17em">Minimum ASCII Delete Sum for Two Strings</strong></summary>

https://leetcode.com/problems/minimum-ascii-delete-sum-for-two-strings/description/?envType=study-plan-v2&envId=dynamic-programming

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

---

<details>
<summary><strong style="font-size:1.17em">Maximum Length of Pair Chain</strong></summary>

https://leetcode.com/problems/maximum-length-of-pair-chain/?envType=study-plan-v2&envId=dynamic-programming

### 풀이 1. 그리디로 풀기 (정렬 후 순회) O(nlogn)

```java
class Solution {
    public int findLongestChain(int[][] pairs) {
        if(pairs.length == 1){
            return 1;
        }


        Arrays.sort(pairs, new Comparator<int[]>() {
            public int compare(int[] a, int[] b){
                return Integer.compare(a[1],b[1]);
            }
        });

        int prev = 0;
        int res = 1;

        for(int i = 1; i < pairs.length; i++){
            if(pairs[prev][1] < pairs[i][0]){
                prev = i;
                res++;
            }
        }

        return res;


    }
    // 형성될 수 있는 가장 긴 체인의 길이를 반환
    // 두번째 인덱스로 정렬 -> 순서가 바뀌어도 상관없으니(어차피 긴 길이 반환) 스테블이든,언스테블이든 어떤 정렬 알고리즘 써도 상관 x
    // prev로 비교하고 조건에 만족하면 +1 후 이동 
    // [1,2] [2,3] [3,4] [5,8]

}

```

### 풀이 2. LIS O(N^2)

```java
class Solution {
    public int findLongestChain(int[][] pairs) {
        if(pairs.length == 1){
            return 1;
        }

        int n = pairs.length;
        int[] length = new int[n];

        Arrays.fill(length,1);
        Arrays.sort(pairs, (a,b)-> Integer.compare(a[1],b[1]));

        for(int i = 1; i < n; i++){
            for(int j = 0; j < i; j++){
                if(pairs[j][1] < pairs[i][0] && 1 + length[j] > length[i]){
                    length[i] = length[j] +1;
                }
            }
        }

        int maxLength = 1;
        for(int l : length){
            maxLength = Math.max(l, maxLength);
        }

        return maxLength;

    }
    // 형성될 수 있는 가장 긴 체인의 길이를 반환
    // 두번째 인덱스로 정렬 -> 순서가 바뀌어도 상관없으니(어차피 긴 길이 반환) 스테블이든,언스테블이든 어떤 정렬 알고리즘 써도 상관 x
    // prev로 비교하고 조건에 만족하면 +1 후 이동 
    // [1,2] [2,3] [3,4] [5,8]

}
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">Longest Arithmetic Subsequence of Given Difference</strong></summary>

https://leetcode.com/problems/longest-arithmetic-subsequence-of-given-difference/?envType=study-plan-v2&envId=dynamic-programming

시간복잡도 O(n)으로 하기 위해 map 사용

```java
import java.util.*;
class Solution {
    public int longestSubsequence(int[] arr, int difference) {
        
        int n = arr.length;
        Map<Integer, Integer> map = new HashMap<>();



        for(int i = 0; i < n; i++){
            map.put(arr[i], map.getOrDefault(arr[i] - difference, 0) + 1);
        }

        return Collections.max(map.values());
    }
}
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">Longest Arithmetic Subsequence</strong></summary>

https://leetcode.com/problems/longest-arithmetic-subsequence/description/?envType=study-plan-v2&envId=dynamic-programming

```java
class Solution {
    public int longestArithSeqLength(int[] nums) {
        int n = nums.length;
        Map<Integer,Integer>[] dp = new HashMap[n];
        for(int i = 0; i < n; i++){
            dp[i] = new HashMap<>();
        }

        int len = 0;

        for(int i = 0; i < n; i++){
            for(int j = 0; j < i; j++){
                int diff = nums[i] - nums[j];
                int d = dp[j].getOrDefault(diff,1);
                dp[i].put(diff,d+1);
                len = Math.max(len,d+1);
            }
        }

        return len;
    }

    // 가장 긴 산술적 부분 수열 길이 반환
    // seq[i+1] - seq[i]가 같은거 
    // 각 배열의 요소마다 맵을 만듦
    // 그리고 그 맵엔 각 요소의 차이에 대한 개수를 저장하는데, 그전에 비교하는 요소의 맵에 그 차이값만큼이 맵에 존재하면 그이전요소의 차이값의 value+1해서 저장
    // 가장 긴건 수시로 업데이트 
}
```


</details>


---

## LCS

---

<details>
<summary><strong style="font-size:1.17em">Uncrossed Lines</strong></summary>

https://leetcode.com/problems/uncrossed-lines/description/?envType=study-plan-v2&envId=dynamic-programming

O(N^2) 

```java
class Solution {
    public int maxUncrossedLines(int[] nums1, int[] nums2) {

        int nums1Len = nums1.length;
        int nums2Len = nums2.length;

        int[][] dp = new int[nums1Len+1][nums2Len+1];

        for(int i = 0; i <= nums1Len; i++){
            for(int j = 0; j <= nums2Len; j++){
                if(i==0 || j==0){
                    dp[i][j] = 0;
                }else if(nums1[i-1] == nums2[j-1]){
                    dp[i][j] = dp[i-1][j-1] + 1;
                }else{
                    dp[i][j] = Math.max(dp[i-1][j], dp[i][j-1]);
                }
            }
        }

        return dp[nums1Len][nums2Len];
        
    }

    // 앞 뒤로 길게  선을 그어 버리면 많은 선을 그을 수가 없음
    // 최장 공통 부분 수열 LCS
}
```

</details>

---

## Best Time to Buy & Sell Stock / State Machine

---

<details>
<summary><strong style="font-size:1.17em">Best Time to Buy and Sell Stock with Cooldown</strong></summary>

https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/submissions/1486103368/?envType=study-plan-v2&envId=dynamic-programming

상태가 중요

주식을 구매한 상태에서 다음 날이 되었을 때 아무것도 안해서 주식을 보유하거나, 판다.
주식을 판매한 상태는 다음 날이 되었을 때 쿨다운 상태이고 
쿨다운 상태는 다음날이 되었을 때 주식을 구매하거나 아무것도 안함

1일차 2일차 

```java
public class Solution {
    public int maxProfit(int[] prices) {
        if(prices == null || prices.length <= 1){
            return 0;
        }

        // 해당 날짜의 주식을 산 상태의 최대값 (전날 산 상태를 유지 or 판 상태에서 + 이번에 산 상태)
        // 판 상태에서 + 이번에 산 상태 라는 말은 이날 사게되면 전날은 무조건 cool 상태여야한다. 
        int[] buy = new int[prices.length];

        // 해당 날짜의 주식이 없는 상태의 최대값 (전날 판 상태를 유지 or 산 상태에서 + 이번에 판 상태)
        int[] sell = new int[prices.length];

        // 첫날
        buy[0] = -prices[0];
        sell[0] = 0;

        // 둘째날
        if(prices.length > 1){
            buy[1] = Math.max(buy[0], -prices[1]);
            sell[1] = Math.max(sell[0],buy[0] + prices[1]);
        }

        for(int i = 2; i < prices.length; i++){
            buy[i] = Math.max(buy[i-1],sell[i-2]-prices[i]);
            sell[i] = Math.max(sell[i-1],buy[i-1] + prices[i]);
        }

        return sell[prices.length-1];
        
    }
}
```


</details>

---

<details>
<summary><strong style="font-size:1.17em">Best Time to Buy and Sell Stock with Transaction Fee</strong></summary>

```java
class Solution {
    public int maxProfit(int[] prices, int fee) {
        if(prices == null || prices.length <= 1){
            return 0;
        }

        int[] buy = new int[prices.length];
        int[] sell = new int[prices.length];

        // 1day
        buy[0] = -prices[0];
        sell[0] = 0;

        //2day
        if(prices.length > 1){
            buy[1] = Math.max(buy[0],-prices[1]);
            sell[1] = Math.max(sell[0], buy[0] + prices[1] - fee);
        }

        for(int i = 2; i < prices.length; i++){
            buy[i] = Math.max(buy[i-1], sell[i-1] -prices[i]);
            sell[i] = Math.max(buy[i-1] + prices[i] -fee, sell[i-1]);
        }

        return sell[prices.length-1];

    }
}
```

</details>


---

## On Trees

---

<details>
<summary><strong style="font-size:1.17em">Unique Binary Search Trees</strong></summary>

https://leetcode.com/problems/unique-binary-search-trees/?envType=study-plan-v2&envId=dynamic-programming

n=1일 때 , 1번 루트를 통해서 왼쪽은 무조건 0개, 오른쪽도 0개 총 1개
n=2일 때, 1번 루트를 통해서 왼쪽은 무조건 0개, 오른쪽은 무조건 1개 총 1개, 2번 루트를 통해서 왼쪽은 1개, 오른쪽은 0개 총 1개
n=3일 때, 1번 루트를 통해서 왼쪽은 무조건 0개, 오른쪽은 2개 0이라는게 0의 묶음 하나이고, 오른쪽은 2,3 묶음이라는게 2개이니 1*2이므로 2,
2번 루트를 통해서 왼쪽은 1개, 오른쪽은 1개 총 1개, 3번 루트를 통해서 왼쪽은 2개, 오른쪽은 0개 총 2개

그림을 그려가며 숫자도 적어야 이해간다 그리고서 함수만들기
G(n) = F(1,n) + F(2,n) + ... + F(n,n) 1,2,...n은 루트가 될 수 있는 숫자이고 오른쪽 n은 구해달라는 값 
그리고 각 F(i,n)은 G(i-1) * G(n-i) 이다.


```text
class Solution {
    public int numTrees(int n) {
        int[] G = new int[n+1];
        G[0] = 1;
        G[1] = 1;

        for(int i = 2; i <=n; i++){
            for(int j = 1; j <= i; j++){
                G[i] += G[j-1]*G[i-j];
            }
        }

        return G[n];
    }
}
```


</details>

---

<details>
<summary><strong style="font-size:1.17em">Unique Binary Search Trees II</strong></summary>

https://leetcode.com/problems/unique-binary-search-trees-ii/?envType=study-plan-v2&envId=dynamic-programming

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {


    public List<TreeNode> generateTrees(int n) {
        if(n==0) return new ArrayList<>();
        return generateSubtrees(1,n);
    }

    private List<TreeNode> generateSubtrees(int left, int right){
        List<TreeNode> result = new ArrayList<>();

        if(left > right){
            result.add(null);
            return result;
        }

        // 각 숫자를 루트로 선택
        for(int i = left; i <= right; i++){
            // 왼쪽 서브트리 생성
            List<TreeNode> leftSubtrees = generateSubtrees(left, i-1);

            // 오른쪽 서브트리 생성
            List<TreeNode> rightSubtrees = generateSubtrees(i+1, right);

            // 가능한 모든 왼쪽/오른쪽 조합 생성
            for(TreeNode l : leftSubtrees){
                for(TreeNode r : rightSubtrees){
                    TreeNode root = new TreeNode(i);
                    root.left = l;
                    root.right = r;
                    result.add(root);
                }
            }


        }

        return result;


    }

    // 1 일때
    // 루트가 1만 있고, 1


    //  2일 때
    // 루트가 1이면 
    // 1 왼쪽은 null, 오른쪽은 2
    // 루트가 2이면
    // 2 왼쪽은 1, 오른쪽은 null 


    // 3일 때
    // 루트가 1이면  
    // 왼쪽은 null, 오른쪽은 (2,3) 
    // 루트가 2이면
    // 왼쪽은 1, 오른쪽은 2
    // 루트가 3이면
    // 왼쪽은 

}
```


</details>


