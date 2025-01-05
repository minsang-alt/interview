<details>
<summary><strong style="font-size:1.17em">Product of Array Except Self</strong></summary>

https://leetcode.com/problems/product-of-array-except-self/solutions/1342916/3-minute-read-mimicking-an-interview/


```java
class Solution {
    public int[] productExceptSelf(int[] nums) {

        int[] prefix = new int[nums.length];
        int[] suffix = new int[nums.length];

        prefix[0] = 1;
        suffix[nums.length-1] = 1;

        for(int i = 0; i < nums.length-1; i++){
            prefix[i+1] = prefix[i] * nums[i];
        }

        for(int i = nums.length-1; i>0; i--){
            suffix[i-1] = suffix[i]*nums[i];
        }

        int[] answer = new int[nums.length];

        for(int i = 0; i < nums.length; i++){
            answer[i] = prefix[i] * suffix[i];
        }

        return answer;


    }

    // 1,2,3,4
    // 2*3*4, 1*3*4, 1*2*4, 1*2*3

    // 1     1  1*2 1*2*3
    // 2*3*4 3*4 4 1
}
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">Find the Duplicate Number</strong></summary>

https://leetcode.com/problems/find-the-duplicate-number/description/

시간복잡도: O(nlogn) / 공간복잡도: O(1)

```java
class Solution {
    public int findDuplicate(int[] nums) {
        if(nums.length <= 2){
            return nums[0];
        }

        int n = nums.length;

        // [1,n-1] 정수가 있다. 

        Arrays.sort(nums);
        int prev = nums[0];

        for(int i = 1; i < n; i++){
            int num = nums[i];
            if(prev == num){
                System.out.println(prev);
                return prev;
            }
            prev = num;
        }

        return nums[0];
    }
    // 처음에는 그냥 Map으로 1,3,4 담으면서 1이 증가하면 그걸 판단 
    // 문제점은 공간복잡도가 Map과 함께 숫자를 넣야되기 때문에 선형 공간이 안됨

    // 1,3,4,2,2
    // 정렬?
}
```


---

브루드포스는 O(n^2)이라서 시간 초과 

```java
    // 2 Loops
    public static int findDuplicate_2loops(int[] nums) {
        int len = nums.length;
        for (int i = 0; i < len; i++) {
            for (int j = i + 1; j < len; j++) {
                if (nums[i] == nums[j]) {
                    return nums[i];
                }
            }
        }

        return len;
    }
```

---

숫자 카운트로 배열에 업데이트

시간복잡도 O(n), 공간 복잡도 O(n)

```java
class Solution {
    public int findDuplicate(int[] nums) {

        // 5이면 [1,4]
        int len = nums.length;
        int[] cnt = new int[len];

        for(int i = 0; i < len; i++){
            cnt[nums[i]]++;
            if(cnt[nums[i]]> 1){
                return nums[i];
            }
        }

        return -1;

    }
}
```

---

비둘기집 원리로 푸는 이진 탐색

시간복잡도 O(nlogn), 공간복잡도 O(1)

```java
class Solution {
    // 1,2,3,3,4
    public int findDuplicate(int[] nums) {
        int left = 1;
        int right = nums.length -1;

        while(left < right){
            int mid = left + (right-left)/2;
            int cnt = 0;

            for(int num : nums){
                if(num <= mid){
                    cnt++;
                }
            }
            // count가 mid보다 크다면, 중복은 left와 mid 사이에 있습니다
            if(cnt > mid){
                right = mid;
            }else{
                left = mid+1;
            }


            
        }

        return left;
    }
}
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">Find All Duplicates in an Array</strong></summary>

https://leetcode.com/problems/find-all-duplicates-in-an-array/

```java
class Solution {
    public List<Integer> findDuplicates(int[] nums) {
        Map<Integer,Integer> map = new HashMap<>();

        List<Integer> ans = new ArrayList<>();
        for(int num : nums){
            if(map.containsKey(num)){
                ans.add(num);
            }else{
                map.put(num,1);
            }
        }

        return ans;
    }
}
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">Set Matrix Zeroes</strong></summary>

https://leetcode.com/problems/set-matrix-zeroes/description/

```java
class Solution {
    public void setZeroes(int[][] matrix) {
        int m = matrix.length;
        int n = matrix[0].length;

        // 0행에 0이 있으면 flag 갖고있기
        boolean rowflag = false;
        for(int i = 0; i < n; i++){
            if(matrix[0][i] == 0){
                rowflag = true;
                break;
            }
        }

        // 0열에 0이 있으면 flag 갖고있기
        boolean colflag = false;
        for(int i = 0; i < m; i++){
            if(matrix[i][0]==0){
                colflag = true;
                break;
            }
        }

        // 순회하면서 0을 찾고 해당 0을 왼쪽 끝, 위쪽 끝에 0을 세팅
        for(int i = 1; i < m; i++){
            for(int j = 1; j < n; j++){
                if(matrix[i][j]==0){
                    matrix[i][0] = 0;
                    matrix[0][j] = 0;
                }
            }
        }

        // 0행 순회하면서 0있으면 그 행의 열에 모두 0채우기
        for(int i = 1; i < n; i++){
            if(matrix[0][i] == 0){
                for(int j = 1; j < m; j++){
                    matrix[j][i] = 0;
                }
            }
        }

        // 0열 순회하면서 0있으면 그 열의 행에 모두 0채우기
        for(int i = 1; i < m; i++){
            if(matrix[i][0]==0){
                for(int j = 1; j < n; j++){
                    matrix[i][j] = 0;
                }
            }
        }

        

        if(rowflag){
            for(int i = 0; i < n; i++){
                matrix[0][i] = 0;
            }
        }

        if(colflag){
            for(int i = 0; i < m; i++){
                matrix[i][0] = 0;
            }
        }


    }

    // 공간복잡도가 O(1) 이어야 함 
    // 만약 순회하면서 0을 마주하면 거기의 행과 열을 다 0으로 바꿔버리면 순회할때 진짜 0을 못찾아서 문제가 생긴다.
    // 그렇다고, 미리 0인 곳을 저장하기에도 공간복잡도를 어기니깐 배열을 조작해서 해나가야 한다.

    // 일단 순회하면서 
}

```

</details>

---

<details>
<summary><strong style="font-size:1.17em">Find Minimum in Rotated Sorted Array</strong></summary>

https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/description/

```java
class Solution {
    public int findMin(int[] nums) {

        int left = 0;
        int right = nums.length -1;

        if(nums[left] <= nums[right]){
            return nums[left];
        }

        while(left <= right){

            if(right-left == 1){
                return Math.min(nums[left],nums[right]);
            }

            int mid = left + (right-left)/2;

            if(nums[mid] > nums[right]){
                left = mid;
            }else if(nums[mid] < nums[right]){
                right = mid;
            }
        }
        
        return nums[left];
    }

    // 그냥 최솟값 구하는 거고, nums는 정렬된 형태에서 n번 오른쪽으로 이동한 채로 제공
    // 그냥 순회하면 O(n)으로 구할 수 있지만, O(logn)으로 풀어야 하는 요구사항을 받았습니다.

    // O(logn)은 이진검색트리

    // 회전해도 어차피 증가함 그런데 어느 지점에서 갑자기 순서가 뒤틀릴 때가 있음 
    // 그니깐 위로 갔다가 갑자기 퐉 떨어지는 구간 있음

    // 목표는 가장 작은 걸 찾아야 함 
    // 3,4,5,1,2
}
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">Longest Consecutive Sequence</strong></summary>

https://leetcode.com/problems/longest-consecutive-sequence/description/

hashset에 넣고, 순회하면서 연속된 숫자를 찾아나가기
O(n)이지만, 최악의 경우 O(n^2)이 될 수 있음

```java
class Solution {
    public int longestConsecutive(int[] nums) {
        Set<Integer> numbers = new HashSet<>();

        int longestlength = 0;

        for(int num : nums){
            numbers.add(num);
        }

        for(int num : nums){
            if(!numbers.contains(num-1)){
                int t = 1;

                while(numbers.contains(num+t)){
                    t++;
                }

                longestlength = Math.max(longestlength, t);
            }
        
        }

        return longestlength;
    }

    // 100,99,101,98
    // 4가 나와야 됨 
    
    // 100 1
    // 순회 99+1




}
```

O(nlogn)이지만 실제 문제에서는 제일 빠름

```java
class Solution {
    public int longestConsecutive(int[] nums) {
        
        ArrayList<Integer> arrs = Arrays.stream(nums)
              .sorted()
              .distinct()
              .boxed()
              .collect(Collectors.toCollection(ArrayList::new));


        int count = 1;
        int longestLen = 1;

        if(nums.length == 0){
            return 0;
        }

        for(int i = 1; i < arrs.size(); i++){
            if(arrs.get(i) == arrs.get(i-1)+1){
                count++;
            }else{
                count = 1;
            }

            longestLen = Math.max(count,longestLen);
        }

        return longestLen;

    }
}
```


</details>

---

<details>
<summary><strong style="font-size:1.17em">Top K Frequent Elements</strong></summary>

https://leetcode.com/problems/top-k-frequent-elements/description/


시간복잡도 O(nlogk) 이며 k <=n 이고, 조건인 nlogn 보다는 조금 빠름
map으로 순회하면서 발견숫자 업데이트하고 우선순위큐로 뽑는데 우선순위 큐는 offer이든 poll이든 logk이기 때문에 O(nlogk)가 됨

```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {

        Map<Integer,Integer> map = new HashMap<>();
        for(int num : nums){
            map.put(num, map.getOrDefault(num, 0) + 1);
        }

        PriorityQueue<int[]> pq = new PriorityQueue<>((a,b)-> b[1]-a[1]);

        for(Map.Entry<Integer,Integer> entry : map.entrySet()){
            pq.offer(new int[]{entry.getKey(),entry.getValue()});
        }


        int[] ans = new int[k];

        for(int i = 0; i < k; i++){
            int[] p = pq.poll();
            ans[i] = p[0];
        }

        return ans;
        
    }

    // 1,1,1,2,2,3 k=2
    // 1,2
}
```

</details>


---

<details>
<summary><strong style="font-size:1.17em">Reorder List</strong></summary>

연결리스트의 중간지점 부터 찾아야되므로 slow, fast 포인터로 중간지점 찾기
중간지점부터 뒤집기
두 리스트 합치기

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public void reorderList(ListNode head) {
        if(head==null) return;

        ListNode slow = head; ListNode fast = head;
        while(fast != null && fast.next != null){
            slow = slow.next;
            fast = fast.next.next;
        }

        ListNode pointer = slow.next;
        slow.next = null;
        ListNode node = null;

        while(pointer != null){
            ListNode temp = pointer.next;
            pointer.next = node;
            node = pointer;
            pointer = temp;
        }


        ListNode first = head;
        ListNode second = node;

        while(second != null){
            ListNode temp1 = first.next;
            ListNode temp2 = second.next;
            first.next = second;
            second.next = temp1;
            first = temp1;
            second = temp2;
        }




    }
}
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">Find All Numbers Disappeared in an Array</strong></summary>

https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/description/

```java
class Solution {
    public List<Integer> findDisappearedNumbers(int[] nums) {
       int n = nums.length; 

       for(int i = 0; i < nums.length; i++){
            
            // swap
            // 다를 때만
            while(true){
                int num = nums[i];
                int tmp = num; // 4
                int comp = nums[tmp-1];
                if(tmp == comp){
                    break;
                }
                nums[i] = comp;
                nums[tmp-1] = tmp;
            }

       }

       List<Integer> list = new ArrayList<>();
       for(int i = 0; i < nums.length; i++){
         if(i+1 != nums[i]){
            list.add(i+1);
         }
       }

        return list;
    }

    // nums의 요소가 [1,n] 없는 요소 반환
    // O(n), O(1)

    // [4,3,2,7,8,2,3,1]
    // 인덱스로 생각
    // 7,3,2,4,8,2,3,1
    // 7,2,3,4,8,2,3,1
    // 7,2,3,4,1,2,3,8
    // 7,2,3,4,1,2,3,8



}
```

음수로 표시

```java
class Solution {
    public List<Integer> findDisappearedNumbers(int[] nums) {
        List<Integer> list = new ArrayList<>();

        for(int i = 0; i < nums.length; i++){
            int ele = Math.abs(nums[i])-1;

            if(nums[ele] > 0){
                nums[ele] = nums[ele] * -1;
            }

        }

        for(int i = 0; i < nums.length; i++){
            if(nums[i] > 0){
                list.add(i+1);
            };
        }

        return list;
    }
}
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">Partition Equal Subset Sum</strong></summary>

https://leetcode.com/problems/partition-equal-subset-sum/description/

냅색 문제고 0/1 배낭문제와 비슷한 문제 인데 이해하기 ㅈㄴ 어려움
밑에 주석 참고

```java
class Solution {
    public boolean canPartition(int[] nums) {
        int sum = 0;
        for(int num : nums){
            sum+=num;
        }

        if(sum % 2 != 0){
            return false;
        }

        int target = sum / 2;

        boolean[][] dp = new boolean[nums.length+1][target+1];
        dp[0][0] = true;

        for(int i = 1; i <= nums.length; i++){
            for(int j = 1; j <= target; j++){
                dp[i][j] = dp[i-1][j];
                if(j>=nums[i-1]){
                    dp[i][j] = dp[i-1][j] || dp[i-1][j-nums[i-1]];
                }
            }
        }

        return dp[nums.length][target];


    }

    // [1,5,11, 5] target = 11
    // {0,1,5,6,11,12,16,17,10}

    // i번 인덱스까지의 수로 0~target까지 완성시킬수있는 지 확인 
    // dp[i][j] i까지 원소에서 j를 만들 수 있나??  ->
    //  i-1부터 j까지 true이면 원소 i에선 선택안하면 된다
    // 또는 i원소를 선택하고 dp[i-1][j-nums[i]]가 true이면 됨 
    // e.g. dp[1][1] = dp[0][1] || dp[0][1-1]

    // target = 11 입니다.
//        0 1 2 3 4
//   0 // t t f f f
//   1 // f f f f f
//   2 // f f f f f
//   3 // f f f f f
//   4 // f f f f f
//   5 // 
//   6
//   7
//   8
//   9
//   10
//   11
}
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">Combination Sum</strong></summary>

https://leetcode.com/problems/combination-sum/


백트래킹

```java
class Solution {

    private List<List<Integer>> result = new ArrayList<>();

    public List<List<Integer>> combinationSum(int[] candidates, int target) {


        combPath(candidates, target, new ArrayList<>(),0);

        return result;
    }

    private void combPath(int[] cand, int target, List<Integer> comb,int st){
        if(target == 0){
            result.add(new ArrayList<>(comb));
            return;
        }else if(target < 0){
            return;
        }


        for(int i = 0; i < cand.length; i++ ){
            if(st > i)continue;
            int c = cand[i];
            comb.add(c);
            combPath(cand, target-c, comb,i);
            comb.remove(comb.size()-1);
        }
    }

    // 중복되고, 
    // 2,3,6,7 target=7
    // 
}
```

dp로 풀었을 때
공간복잡도, 시간복잡도가 매우 증가

```java
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        // dp[i]는 합이 i가 되는 모든 조합들을 저장
        List<List<Integer>>[] dp = new List[target+1];

        for(int i = 0; i <= target; i++){
            dp[i] = new ArrayList<>();
        }

        dp[0].add(new ArrayList<>());

        for(int candidate : candidates){
            for(int j = candidate; j <= target; j++){
                for(List<Integer> comb : dp[j-candidate]){
                    List<Integer> newComb = new ArrayList<>(comb);
                    newComb.add(candidate);
                    dp[j].add(newComb);
                }
            }
        }

        return dp[target];
    }
}
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">Minimum Height Trees</strong></summary>

https://leetcode.com/problems/minimum-height-trees/description/

리프노드를 계속 제거해서 1,2개 남았을 때 노드를 반환한다.
-> 이 생각은 노드를 한개 , 두개 늘려가면서 규칙을 찾을 수 있다. 

```java
class Solution {
    public List<Integer> findMinHeightTrees(int n, int[][] edges) {
        // 노드가 1개나 2개인 경우의 예외처리
        if(n <= 2){
            List<Integer> centroids = new ArrayList<>();
            for(int i = 0; i < n; i++){
                centroids.add(i);
            }
            return centroids;
        }

        // 인접리스트 그래프로 표현
        List<Set<Integer>> graph = new ArrayList<>();
        for(int i = 0; i < n; i++){
            graph.add(new HashSet<>());
        }

        // edges 배열을 이용해 그래프 구성
        for(int[] edge : edges){
            graph.get(edge[0]).add(edge[1]);
            graph.get(edge[1]).add(edge[0]);
        }

        List<Integer> leaves = new ArrayList<>();
        // 초기 리프 노드 찾기
        for(int i = 0; i < n; i++){
            if(graph.get(i).size() == 1){
                leaves.add(i);
            }
        }

        // 남은 노드 수
        int remainingNodes = n;

        // 노드가 1개 또는 2개만 남을 때까지 반복
        while(remainingNodes > 2){
            remainingNodes -= leaves.size();
            List<Integer> newLeaves = new ArrayList<>();

            // 현재 리프 노드들을 제거
            for(int leaf : leaves){
                // 리프노드의 이웃 노드 찾기 (무조건 1개임)
                int neighbor = graph.get(leaf).iterator().next();
                // 이웃 노드에서 현재 리프 노드 제거
                graph.get(neighbor).remove(leaf);

                //이웃 노드가 새로운 리프 노드가 되었는지 확인
                if(graph.get(neighbor).size()==1){
                    newLeaves.add(neighbor);
                }
            }

            leaves = newLeaves;
        }

        return leaves;
    }
}
```

</details>


---

<details>
<summary><strong style="font-size:1.17em">Maximum Subarray</strong></summary>

https://leetcode.com/problems/maximum-subarray/description/

prefix가 음수이면 0으로 초기화하고 다음부터 계산해야 최대크기를 구할 수 있다.

```java
class Solution {
    public int maxSubArray(int[] nums) {
        if(nums.length==1){
            return nums[0];
        }
        
        int sum = nums[0];
        int max = sum;
        for(int i = 1; i < nums.length; i++){
            if(sum < 0){
                sum = 0;
            }
            max = Math.max(max, sum + nums[i]);
            sum+= nums[i];
        }
        return max;
    }
}
```

</details>