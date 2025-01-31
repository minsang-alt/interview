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

---

<details>
<summary><strong style="font-size:1.17em">Sort List</strong></summary>

https://leetcode.com/problems/sort-list/description/

조건이 시간복잡도 O(nlogn)이고 공간복잡도 O(1)이어야 한다.

정렬 알고리즘 중 하나인 병합정렬을 사용한다.
그리고 병합정렬을 링크드리스트로 구현하는 방법을 알아야 하며, 
이때 중간을 찾기위해 fast, slow 포인터를 사용한다.

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
    public ListNode sortList(ListNode head) {
        
        if(head == null || head.next == null){
            return head;
        }

        ListNode slow = head;
        ListNode fast = head;
        ListNode prev = null;

        while(fast != null && fast.next != null){
            prev = slow;
            slow = slow.next;
            fast = fast.next.next;
        }

        // 리스트 나누기
        prev.next = null;

        ListNode l1 = sortList(head);
        ListNode l2 = sortList(slow);

        return merge(l1,l2);
    }

    private ListNode merge(ListNode l1, ListNode l2){
        ListNode dummy = new ListNode(0);
        ListNode curr = dummy;

        while(l1 != null && l2 != null){
            if(l1.val <= l2.val){
                curr.next = l1;
                l1 = l1.next;
            }else{
                curr.next = l2;
                l2 = l2.next;
            }

            curr = curr.next;
        }

        if(l1 != null){
            curr.next = l1;
        }
        if(l2 != null){
            curr.next = l2;
        }

        return dummy.next;
    }
}
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">Minimum Number of Arrows to Burst Balloons</strong></summary>

https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/description/

```java
class Solution {
    public int findMinArrowShots(int[][] points) {
        if(points.length <= 1){
            return points.length;
        }

        Arrays.sort(points, (a,b)->Integer.compare(a[1],b[1]));
        int arrowPos = points[0][1];
        int arrowCnt = 1;

        for(int i = 1; i < points.length; i++){
            if(arrowPos >= points[i][0]){
                continue;
            }

            arrowCnt++;
            arrowPos = points[i][1];
        }

        return arrowCnt;
    }

    // 최소 화살 개수
    // [x1,x2] x1<= <=x2
    // 모든 풍선을 터뜨려야함
    // 쏜 화살이 x위치 사이에 있으면 터짐 
    
    // [1,6], [2,8], [3,4], [10,16]
    // -> [3,4], [1,6], [2,8], [10,16]

}
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">Maximum Width of Binary Tree</strong></summary>

https://leetcode.com/problems/maximum-width-of-binary-tree/description/

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
    class Pair {
        TreeNode node;
        int index;

        Pair(TreeNode node, int index){
            this.node = node;
            this.index = index;
        }
    }

    public int widthOfBinaryTree(TreeNode root) {
        return bfs(root);
    }

    private int bfs(TreeNode root){
        Deque<Pair> q = new LinkedList<>();
        q.offer(new Pair(root,0));
        int maxWidth = 0;

        while(!q.isEmpty()){
            // 현재 레벨의 노드 사이즈 
            int size = q.size();
            int left = q.peek().index;
            int right = left;

            for(int i = 0; i < size; i++){
                Pair current = q.poll();
                right = current.index;

                if(current.node.left != null){
                    q.offer(new Pair(current.node.left,current.index*2+1));
                }

                if(current.node.right != null){
                    q.offer(new Pair(current.node.right,current.index*2+2));
                }
            }

            maxWidth = Math.max(maxWidth, right-left + 1);




        }

        return maxWidth;

    }
}

// 레벨 너비 최대 구하고
// 그 너비란, null이 아닌 왼쪽 끝 노드부터 오른쪽 끝노드까지의 개수
// 그리고 그 사이의 null은 포함해서 계산 


// 1
// 2, 3
// 4, 5, 6,7
// 8, 9, 10, 11, 12, 13, 14
// 2n ~ 2n
```

</details>



---

<details>
<summary><strong style="font-size:1.17em">Unique Paths</strong></summary>

https://leetcode.com/problems/unique-paths/

겁나쉬운 dp

```java
class Solution {
    public int uniquePaths(int m, int n) {
        int[][] dp = new int[m][n];

        for(int i = 0; i < m; i++){
            dp[i][0] = 1;
        }

        for(int i = 0; i < n; i++){
            dp[0][i] = 1;
        }

        for(int i = 1; i < m; i++){
            for(int j = 1; j < n; j++){
                dp[i][j] = dp[i-1][j] + dp[i][j-1];
            }
        }

        return dp[m-1][n-1];
    }
}

// 1 1 1 1 1 1 1
// 1 2 3 4 5 6 7
// 1 3 6 10 15 21 28

```

</details>

---

<details>
<summary><strong style="font-size:1.17em">Spiral Matrix</strong></summary>

https://leetcode.com/problems/spiral-matrix/description/

```java
class Solution {
    int[] dx= new int[]{-1,0,1,0};
    int[] dy = new int[]{0,1,0,-1};

    public List<Integer> spiralOrder(int[][] matrix) {
        int m = matrix.length;
        int n = matrix[0].length;

        List<Integer> result = new ArrayList<>();

        int nx = 0;
        int ny = 0;
        while(nx < m && ny < n){
            //오른쪽
            for(int i = ny; i < n; i++){
                result.add(matrix[nx][i]);
            }
            nx = nx+1;

            // 아래쪽
            for(int i = nx; i < m; i++){
                result.add(matrix[i][n-1]);
            }
            n--;

            // 왼쪽
            if(nx < m){
                for(int i = n-1; i>= ny; i-- ){
                    result.add(matrix[m-1][i]);
                }
            }
            
            m--;

            // 위쪽
            if(ny < n){
                for(int i = m-1; i >= nx; i--){
                    result.add(matrix[i][ny]);
                }
            }
            
            ny++;

        }

        return result;


    }

    // 오른쪽 아래쪽 왼쪽 위쪽 
}
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">Find K Closest Elements</strong></summary>

https://leetcode.com/problems/find-k-closest-elements/description/

```java
class Solution {
    public List<Integer> findClosestElements(int[] arr, int k, int x) {
        List<Integer> result = new ArrayList<>();
        if(arr.length == 1){
            result.add(arr[0]);
            return result;
        }

        int minIdx = 0;
        int minElement = Math.abs(arr[0]-x);
        for(int i = 0; i < arr.length; i++){
            if(minElement > Math.abs(arr[i]-x)){
                minIdx = i;
                minElement = Math.abs(arr[i]-x);
            }
        }

        int left = minIdx;
        int right = minIdx;
        int cnt = 1;

        while(cnt < k){
            if(left <= 0){
                right++;
            }else if(right >= arr.length-1){
                left--;
            }else{
                if(Math.abs(arr[left-1]-x) <= Math.abs(arr[right+1]-x)){
                    left--;
                }else{
                    right++;
                }
            }

            cnt++;
        }

        for(int i = left; i <= right; i++){
            result.add(arr[i]);
        }

        return result;
    }
}

// 2 2 3 4 5 6
// 오름차순으로 주어지고
// 

// -1 1 if: x = -1  2 2 , -1 < 1 -1을 가져옵니다. 

// 반환할때도 오름차순으로 반환 

// 브루도포스로 진행하면
// [1,1,2,3,4,5] 
// x = 3

// [1,1,2,3,4,5] x = 3 k = 4 
// 2,2,1,0,1,2
// 2,3,4,5

// 1,2,3,4,5,6,7,8,9
// . . . . 
// 

// 순회하면서 절댓값으로 가장 작은 곳 포인터로 잡고, 즉 인덱스를 저장하고
```


</details>

---

<details>
<summary><strong style="font-size:1.17em">Longest Palindromic Substring</strong></summary>

https://leetcode.com/problems/longest-palindromic-substring/description/

```java
class Solution {
    public String longestPalindrome(String s) {
        if(s.length() == 1){
            return s;
        }

        String longest = s.substring(0,1);


        for(int i = 0; i < s.length(); i++){
            String tmp = expandFromCenter(s,i,i);
            if(tmp.length() > longest.length()){
                longest = tmp;
            }

            tmp = expandFromCenter(s,i,i+1);
                        if(tmp.length() > longest.length()){
                longest = tmp;
            }
        }

        return longest;
        
    }

    private String expandFromCenter(String s, int left, int right){
        while(left >= 0 && right < s.length()
            && s.charAt(left) == s.charAt(right)
        ){
            left--;
            right++;
        }

        return s.substring(left+1,right);
    }

    // b a b a d
    // 0 1 2 3 4

//   1번 인덱스 0,2 dp[0][2] = true; dp[2][0] = true; dp[1][1] = true;


    //   0 1 2 3 4
    // 0 1 1 3
    // 1 1 1 
    // 2     1
    // 3       1
    // 4         1

}
```

</details>


----

<details>
<summary><strong style="font-size:1.17em">Letter Combinations of a Phone Number</strong></summary>

https://leetcode.com/problems/letter-combinations-of-a-phone-number/description/

백트래킹

```java
class Solution {
    
    private List<String> result = new ArrayList<>();

    public List<String> letterCombinations(String digits) {

        if(digits.length() <= 0){
            return new ArrayList<>();
        }

        Map<Character, String> map = new HashMap<>();
        map.put('2',"abc"); map.put('3',"def");
        map.put('4',"ghi"); map.put('5',"jkl"); map.put('6',"mno");
        map.put('7',"pqrs"); map.put('8',"tuv"); map.put('9',"wxyz");

        // "234"
        comb(map, new StringBuilder(),digits, 0);


        return result;
    }

    private void comb(Map<Character,String> map, StringBuilder combString,String digits, int st ){
        if(digits.length() == combString.length()){
            result.add(combString.toString());
            return;
        }

        for(int i = st; i < digits.length(); i++){
            Character c = digits.charAt(st);
            String dic = map.get(c);

            for(char alpha : dic.toCharArray()){
                combString.append(alpha);
                comb(map,combString,digits,i+1);
                combString.deleteCharAt(combString.length()-1);
            }
        }
    }

    // 2 -> [a,b,c]
    // 3 -> [d,e,f]
}


```

FIFO 큐로 구현

```java
public List<String> letterCombinations(String digits) {
		LinkedList<String> ans = new LinkedList<String>();
		if(digits.isEmpty()) return ans;
		String[] mapping = new String[] {"0", "1", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
		ans.add("");
		for(int i =0; i<digits.length();i++){
			int x = Character.getNumericValue(digits.charAt(i));
			while(ans.peek().length()==i){
				String t = ans.remove();
				for(char s : mapping[x].toCharArray())
					ans.add(t+s);
			}
		}
		return ans;
	}
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">Sort Colors</strong></summary>

https://leetcode.com/problems/sort-colors/description/


선택 정렬 O(n^2), 공간복잡도 O(1)

```java
class Solution {
    public void sortColors(int[] nums) {
        int n = nums.length;

        for(int i = 0; i < n-1; i++){
            
            int minIdx = i;

            for(int j = i+1; j < n; j++){
                if(nums[minIdx] > nums[j]){
                    minIdx = j;
                }
            }

            int temp = nums[i];
            nums[i] = nums[minIdx];
            nums[minIdx] = temp;
        }


    }
}
```


Dutch National Flag 문제로 풀 수 있음 배열에 0,1,2 세 가지 숫자만 있다는 특징과 한번의 순회로 해결, 
투포인터 기법 

```java
class Solution {
    public void sortColors(int[] nums) {
        int left = 0; // 0을 위한 포인터
        int right = nums.length -1; // 2을 위한 포인터
        int current = 0; // 현재 검사중인 위치

        while(current <= right){
            if(nums[current] == 0){
                swap(nums,left, current);
                left++;
                current++;
            }else if(nums[current] == 2){
                swap(nums,current,right);
                right--;
            }else{
                current++;
            }
        }
    }

    private void swap(int[] nums, int i, int j){
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">Lowest Common Ancestor of a Binary Tree</strong></summary>

https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/description/

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        List<TreeNode> p1 = new ArrayList<>();
        List<TreeNode> q1 = new ArrayList<>();

        dfs(root, p, p1, new ArrayList<>());
        dfs(root, q, q1, new ArrayList<>());

        Map<TreeNode, Integer> map = new HashMap<>();
        for(TreeNode node : p1) {
            map.put(node, 1);
        }

        for(int i = q1.size()-1; i >= 0; i--) {
            if(map.containsKey(q1.get(i))) {
                return q1.get(i);
            }
        }
        return root;
    }

    private void dfs(TreeNode root, TreeNode target, List<TreeNode> result, List<TreeNode> arr) {
        if(root == null || result.size() != 0) {
            return;
        }

        arr.add(root);

        if(root == target) {
            result.addAll(new ArrayList<>(arr));
            return;
        }

        dfs(root.left, target, result, arr);
        dfs(root.right, target, result, arr);

        arr.remove(arr.size()-1);
    }


}

// 노드 p,q가 주어지면 최하위 공통 조상을 찾는 문제 
// 노드 자체가 조상인겸, 후손이 될 수 있습니다.

// p=5, q=1 -> 3
// 이게 왜 dfs?, tree?, binary tree?
// dfs를 순회해서 특정 노드를 찾으면 그때 거쳐갔던 노드들을 리스트에 넣고
// 리스트를 비교해서 가장 오른쪽에 있으면서 같은 노드를 반환 

```


양쪽에서 p,q를 찾으면 내가 LCA, 아니면 찾은 것만 위로 전달

```java
public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
    if (root == null || root == p || root == q) {
        return root;
    }
    
    TreeNode left = lowestCommonAncestor(root.left, p, q);
    TreeNode right = lowestCommonAncestor(root.right, p, q);
    
    if (left != null && right != null) {
        return root;
    }
    
    return left != null ? left : right;
}
```
</details>


---

<details>
<summary><strong style="font-size:1.17em">Peak Index in a Mountain Array</strong></summary>

https://leetcode.com/problems/peak-index-in-a-mountain-array/

```java
class Solution {
    public int peakIndexInMountainArray(int[] arr) {
        int left = 0;
        int right = arr.length -1;

        while(left < right){
            int mid = left + (right-left) / 2 ;

            // 증가하는 형태 
            if(arr[mid] < arr[mid + 1]){
                left = mid + 1;
            }else{
                right = mid;
            }

        }

        return left;


    }
}

// 증가했다가 감소하는 지점의 인덱스를 반환
// 시간복잡도는 O(logn)

// 이분탐색 
// [0,2,3,4,5,3,1,0]
// 4를 선택하고 만약 왼쪽 오른쪽 3 < 4 < 5 이런형태면 오른쪽으로이동
// 4< 5 > 3인 형태를 찾습니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">Insert Interval</strong></summary>

https://leetcode.com/problems/insert-interval/description/

```java
class Solution {
    public int[][] insert(int[][] intervals, int[] newInterval) {
        List<int[]> intervalList = new ArrayList<>(Arrays.asList(intervals));
        intervalList.add(newInterval);
        Collections.sort(intervalList,(a,b)->Integer.compare(a[0],b[0]));

        List<int[]> res = new ArrayList<>();
        int[] current = intervalList.get(0);

        for(int i = 1; i <intervalList.size(); i++){
            int[] interval = intervalList.get(i);

            if(current[1] >= interval[0]){
                current[1] = Math.max(current[1],interval[1]);
            }else{
                res.add(current);
                current = interval;
            }
        }

        res.add(current);
        return res.toArray(new int[res.size()][]);


    }
}
```

</details>


---

<details>
<summary><strong style="font-size:1.17em">Jump Game</strong></summary>

https://leetcode.com/problems/jump-game/description/

```java
class Solution {
    public boolean canJump(int[] nums) {
        
        if(nums.length==1){
            return true;
        }

        boolean[] dp = new boolean[nums.length];
        dp[nums.length-1] = true;

        for(int i = nums.length -2; i >= 0; i--){
            for(int j = 1; j<= nums[i] && i+j <= nums.length-1; j++){
                if(dp[i+j]){
                    dp[i] = true;
                    break;
                }
            }
        }

        return dp[0];
        
    }

    // dp[i] = i 위치에서 끝점까지 도달할 수 있는지 여부
    // 3 2 1 0 4
    //       f t

    // dp[4] = true
    // dp[3] = dp[nums[3]+ 3] = f
    // dp[2] = dp[nums[2]+ 2] = dp[3] = f
    // dp[1] = dp[nums[1]+1] = dp[3] = f
    // dp[0] = dp[nums[0] + 0]3 = dp[3] = f

    // 2 3 1 1 4
    // dp[4] = t
    // dp[3] = dp[nums[3]+ 3] = dp[4] = t
    // dp[2] = dp[nums[2]+ 2] = dp[3] = t
    
    // if: nums[x] >= nums.length-1 -> 무조건 t 배열 outof
    

}
```

O(n)방법

뒤에서부터 앞으로 오면서, 각 위치에서 last에 도달할 수 있는지 확인
도달할 수 있다면 last를 현재 위치로 업데이트

```java
class Solution {
    public boolean canJump(int[] nums) {

        if (nums.length == 1) {
            return true;
        }

        int last = nums.length - 1;
        for (int i = nums.length - 2; i >= 0; i--) {
            if (i + nums[i] >= last) {
                last = i;
            }
        }

        return last <= 0;

    }
}
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">Palindromic Substrings</strong></summary>

https://leetcode.com/problems/palindromic-substrings/description/

```java
class Solution {
    public int countSubstrings(String s) {
        
        if(s.length()==1){
            return 1;
        }

        int result = 0;
        for(int i = 0; i < s.length(); i++){
            char cur = s.charAt(i);
            result++;


            // 홀수
            int left = i-1;
            int right = i+1;
            while(left >= 0 && right <= s.length()-1){
                if(s.charAt(left)== s.charAt(right)){
                    result++;
                    left--;
                    right++;
                }else{
                    break;
                }
            }


            //짝수
            left = i;
            right = i+1;

            while(left >= 0 && right <= s.length()-1){
                if(s.charAt(left)== s.charAt(right)){
                    result++;
                    left--;
                    right++;
                }else{
                    break;
                }
            }
        }

        return result;
    }
}
```

```java
class Solution {
    public int countSubstrings(String s) {
        if(s.length() == 1){
            return 1;
        }

        int ans = 0;
        for(int i = 0; i < s.length(); i++){
            for(int j = i; j < s.length(); j++){
                if(isPalindlom(i,j,s)) ans++;
            }
        }

        return ans;
    }

    private boolean isPalindlom(int st, int en, String s){
        while(st<=en){
            if(s.charAt(st)!=s.charAt(en)){
                return false;
            }
            st++;
            en--;
        }
        return true;
    }
}
```

```java
class Solution {
    public int countSubstrings(String s) {
        int n = s.length();
        boolean[][] palindrome = new boolean[n][n];
        int ans = 0;

        for(int i=0;i<n;i++) {
            palindrome[i][i] = true;
            ans++;
        }

        for(int i=0;i<n-1;i++) {
            if(s.charAt(i) == s.charAt(i+1)) {
                palindrome[i][i+1] = true;
                ans++;
            }
        }

        for(int len=3;len<=n;len++) {
            for(int i=0;i<n-len+1;i++) {
                if(s.charAt(i) == s.charAt(i+len-1) && palindrome[i+1][i+len-2]) {
                    palindrome[i][i+len-1] = true;
                    ans++;
                }
            }
        }

        return ans;
    }
}
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">Number of Islands</strong></summary>

https://leetcode.com/problems/number-of-islands/description/

```java
class Solution {

    private int[] dx = {-1,0,1,0};
    private int[] dy = {0,1,0,-1};
    private int M;
    private int N;

    public int numIslands(char[][] grid) {
        M = grid.length;
        N = grid[0].length;

        boolean[][] visited = new boolean[M][N];
        
        int islandCnt = 0;
        for(int i = 0; i < M; i++){
            for(int j = 0; j < N; j++){
                if(grid[i][j] == '1' && !visited[i][j]){
                    dfs(i,j,grid,visited);
                    islandCnt++;
                }
            }
        }

        return islandCnt;
    }

    private void dfs(int x, int y, char[][] grid, boolean[][] visited){

        visited[x][y] = true;
        
        for(int i = 0; i < 4; i++){
            int nx = x + dx[i];
            int ny = y + dy[i];

            if(0 > nx || nx >= M || 0 > ny || ny >= N){
                continue;
            }

            if(!visited[nx][ny] && grid[nx][ny] == '1'){
                dfs(nx,ny, grid, visited);
            }


        }
        
    }
}

// 00 부터 진입을 하고, 상하좌우를 보면서 dfs를 돌리고 방문표시를 한다
// 만약에 0을 만나면 그 자리에서 즉시 다음방향으로 넘어갑니다
// 그렇게 해서 빠져나가면 섬 1개가 충족되고, 또 다른 곳에서 섬이 있을 수 있으니
// 0,1 .. 0,2 이렇게 전붇 살펴봅니다. 하지만 visit된 곳과 0인 곳은 dfs를 돌리지않습니다.

// O(n^3) = 90000 -> 27 000 000
```


</details>

---

<details>
<summary><strong style="font-size:1.17em">Kth Smallest Element in a BST</strong></summary>

https://leetcode.com/problems/kth-smallest-element-in-a-bst/description/

```java
class Solution {
    public int kthSmallest(TreeNode root, int k) {
        List<Integer> treeNodes = new ArrayList<>();
        dfs(root, treeNodes);

        return treeNodes.get(k-1);
    }

    private void dfs(TreeNode root, List<Integer> treeNodes){
        if(root == null){
            return;
        }

        dfs(root.left, treeNodes);
        treeNodes.add(root.val);
        dfs(root.right, treeNodes);
    }
}

// 왼쪽 -> 루트 -> 오른쪽 이렇게 다 리스트에 담고 k 번쨰 값을 꺼냅니다.
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">3Sum</strong></summary>

```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        Arrays.sort(nums);

        for(int i = 0; i < nums.length; i++){
            if(i > 0 && nums[i] == nums[i-1]) continue;

            List<Integer> threeNum = new ArrayList<>();
            

            int target = -nums[i];

            int left = i+1;
            int right = nums.length -1;

            while(left < right){
                if(nums[left] + nums[right] == target){
                    result.add(Arrays.asList(nums[i],nums[left],nums[right]));

                    // 중복 건너뛰기
                    while (left < right && nums[left] == nums[left+1]) left++;
                    while (left < right && nums[right] == nums[right-1]) right--;
                
                    left++;
                    right--;
                }else if(nums[left] + nums[right] > target){
                    right--;
                }else{
                    left++;
                }

            }

        }
        
        return result;
    }
}

// 인덱스가 다른 세개의 값의 합이 0이 되게 해야하고

// [-1,0,1,2,-1,-4]
// -4 -1 -1 0 1 2

// 한놈을 고정

// -4 고정 후 나머지를 4가되게.
// 정렬된 배열에서 두 수의 합이 4가되게 하는 문제로 바뀜 
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">Generate Parentheses</strong></summary>

https://leetcode.com/problems/generate-parentheses/description/

```java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> result = new ArrayList<>();

        dfs(result, n,n, new StringBuilder());

        return result;
    }

    private void dfs(List<String> result, int left, int right, StringBuilder path){
        if(left > right || left < 0 || right < 0){
            return;
        }

        if(left == 0 && right == 0){
            result.add(path.toString());
            return;
        }

        dfs(result, left-1, right, path.append("("));
        path.deleteCharAt(path.length()-1);
        dfs(result, left, right-1, path.append(")"));
        path.deleteCharAt(path.length()-1);
    }
}

// n쌍이면

// n 개의 (, )이 있다는 것
// (()) , ()() -> 완전탐색

// 스택 판단처럼 
```




</details>

---

<details>
<summary><strong style="font-size:1.17em">All Nodes Distance K in Binary Tree</strong></summary>

https://leetcode.com/problems/all-nodes-distance-k-in-binary-tree/description/

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public List<Integer> distanceK(TreeNode root, TreeNode target, int k) {
        Map<TreeNode, TreeNode> map = new HashMap<>();
        bfs(map, root);

        List<Integer> result = new ArrayList<>();
        Set<TreeNode> visited = new HashSet<>();
        solve(result, map, target,k,visited);


        return result;

    }

    private void solve(List<Integer> result, Map<TreeNode, TreeNode> map, TreeNode node, int k,Set<TreeNode> visited){

        if(node == null || visited.contains(node)) return;
        visited.add(node);

        if(k==0){
            result.add(node.val);
            return;
        }

        solve(result,map,node.left, k-1,visited);
        solve(result,map,node.right, k-1,visited);

        if(map.containsKey(node)){
            solve(result,map,map.get(node),k-1,visited);
        }
        
        


    }

    private void bfs(Map<TreeNode,TreeNode> map, TreeNode root ){
        if(root == null){
            return;
        }
        if(root.left != null){
            map.put(root.left, root);
            bfs(map, root.left);
        }

        if(root.right != null){
            map.put(root.right,root);
            bfs(map,root.right);
        }
        
        
    }








}
// bfs를 타면서 target
// target에 대해 k 거리에 있는 노드들을 반환하며, 순서는 상관없습니다
// // 먼저 target을 bfs를 찾고, hashmap에 각 노드들 번호를 저장
// 키: 노드값 값: 번호 
// 그다음 찾은 target에서 k이니깐 
// 루트기준으로 노드가 있는 방향은 |target번호-루트번호|+ k
// 아닌 방향은 k- |target번호-루트번호| 인 노드들 저장 
//     1
//    2 2
//  3 3 3 3
// 4 4444444
//   55

// 루트를 기준으로 왼쪽 노드 오른쪽 노드 번호의 합
// 
```


```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    Map<TreeNode, TreeNode> parent;

    public List<Integer> distanceK(TreeNode root, TreeNode target, int k) {
        parent = new HashMap<>();

        // 1. 모든 노드의 부모 정ㅂ조를 저장
        dfs(root, null);    

        // 2. target에서부터 k 만큼 떨어진 노드를 찾기 위한 BFS
        Queue<TreeNode> queue = new LinkedList<>();
        Set<TreeNode> visited = new HashSet<>();
        queue.add(target);
        visited.add(target);

        int dist = 0;
        while(!queue.isEmpty() && dist < k){
            int size = queue.size();
            
            for(int i = 0; i < size; i++){
            TreeNode node = queue.poll();

            if(node.left != null && !visited.contains(node.left)){
                queue.add(node.left);
                visited.add(node.left);
            }

            if(node.right != null && !visited.contains(node.right)){
                queue.add(node.right);
                visited.add(node.right);
            }

            TreeNode par = parent.get(node);
            if(par != null && !visited.contains(par)){
                queue.add(par);
                visited.add(par);
            }
            }

            dist++;


        }

        List<Integer> result = new ArrayList<>();
        for(TreeNode node : queue){
            result.add(node.val);
        }

        return result;

    }

    private void dfs(TreeNode node, TreeNode par){
        if(node == null) return;
        parent.put(node,par);
        dfs(node.left, node);
        dfs(node.right, node);
    }
}
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">Validate Binary Search Tree</strong></summary>

https://leetcode.com/problems/validate-binary-search-tree/description/

```java

class Solution {
    public boolean isValidBST(TreeNode root) {
        return validate(root, Long.MIN_VALUE, Long.MAX_VALUE);
    }

    private boolean validate(TreeNode node, long min, long max){
        if(node== null) return true;

        if(node.val <= min || node.val >=max)return false;

        return validate(node.left, min, node.val) && validate(node.right, node.val, max);
    }
}
```


</details>

---

<details>
<summary><strong style="font-size:1.17em">Search a 2D Matrix II</strong></summary>

https://leetcode.com/problems/search-a-2d-matrix-ii/description/

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int m = matrix.length;
        int n = matrix[0].length;

        if(m == 1 && n == 1 && matrix[0][0] == target){
            return true;
        }

        for(int i = 0; i < m; i++){
            int left = 0;
            int right = n-1;

            while(left <= right){
                int mid = left + (right-left)/2;
                if(matrix[i][mid] == target){
                    return true;
                }

                if(matrix[i][mid] < target){
                    left = mid+1;
                }else{
                    right = mid-1;
                }
            }
        }

        return false;
    }
}

// 각 행 오름차순, 각 열 오름차순 
// 효율적인 검색

// 각 행마다 bst
// O(nlogn)
```

```java
    public boolean searchMatrix(int[][] matrix, int target) {
        if(matrix == null || matrix.length < 1 || matrix[0].length <1) {
            return false;
        }
        int col = matrix[0].length-1;
        int row = 0;
        while(col >= 0 && row <= matrix.length-1) {
            if(target == matrix[row][col]) {
                return true;
            } else if(target < matrix[row][col]) {
                col--;
            } else if(target > matrix[row][col]) {
                row++;
            }
        }
        return false;
    }
```



</details>

---

<details>
<summary><strong style="font-size:1.17em">House Robber II</strong></summary>

https://leetcode.com/problems/house-robber-ii/description/

```java
class Solution {
    public int rob(int[] nums) {
        if(nums.length ==1 ) return nums[0];

        return Math.max(rob(nums,0, nums.length-1), rob(nums,1,nums.length));
    }   

    private int rob(int[] nums, int start, int end){
        int prefix = 0; int curMax = 0;

        for(int i = start; i < end; i++){
            int t = curMax;
            curMax = Math.max(curMax, prefix + nums[i]);
            prefix = t;
        }

        return curMax;
    }
}
```

</details>

---

<details>
<summary><strong style="font-size:1.17em"> Merge Intervals</strong></summary>

https://leetcode.com/problems/merge-intervals/

```java
class Solution {
    public int[][] merge(int[][] intervals) {
        if(intervals.length == 1){
            return intervals;
        }
        
        int n = intervals.length;
        List<int[]> res = new ArrayList<>();


        // 정렬
        Arrays.sort(intervals, (a,b) -> Integer.compare(a[0],b[0]));
        

        int[] cur = new int[2];
        int[] next = new int[2];

        cur =intervals[0];
        for(int i = 1; i < n; i++){
            next = intervals[i];

            if(cur[1]>=next[0]){
                cur = new int[]{cur[0], Math.max(cur[1],next[1])};
            }else{
                res.add(cur);
                cur = next;
            }
        }

        res.add(cur);

        return res.toArray(new int[res.size()][]);
    }
}

// 겹치는 간격은 병합=합치고 그렇게 합친 결과들을 반환
// [1,3] [2,6] [8,10] [15,18]

// [1,6] [8,10] [15,18]


// [1,4] [4,5]
// [1,5]

// O(n^2) x
// O(n)


// 오름차순 정렬 intervals[i][0] 

// [1,3] [2,6] [8,10] [15,18]
// cur -> [1,3]
// next -> [2,6]
// 겹친다는 조건? -> [a,b] [c,d] 일 때 b >=c 면 겹친다
// [1,6] : [a,d] <- cur next ->[8,10]

// [1,6] [8,10] b < c 겹치x cur->[8,10]
// 새로운 ArrayList 객체에다가 겹친걸 넣어야하기 때문에 

// 
```

</details>


----

<details>
<summary><strong style="font-size:1.17em">Maximum Binary Tree</strong></summary>

https://leetcode.com/problems/maximum-binary-tree/description/

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

    public TreeNode constructMaximumBinaryTree(int[] nums) {
            if(nums.length == 1){
                return new TreeNode(nums[0], null,null);
            }
        
            TreeNode node = makeTree(nums, 0, nums.length-1);

            return node;
    }

    private TreeNode makeTree(int[] nums, int st, int en){
        
        if(st > en){
            return null;
        }

        int maxIdx = st;
        for(int i = st; i <= en; i++){
            if(nums[i] > nums[maxIdx]){
                maxIdx = i;
            }
        }

        TreeNode left = makeTree(nums, st, maxIdx-1);
        TreeNode right = makeTree(nums, maxIdx+1, en);

        return new TreeNode(nums[maxIdx],left,right);

    }
}

// 완전 이진트리
// 루트노드는 nums 최대값
// [3,2,1,6,0,5]
// 정렬 x 최대값 찾고 그 기준으로 왼쪽 오른쪽 나누고 
// 재귀로 풀면 편할 것 같습니다.
// bfs로 하면 될

// st en 사이에 최대값이 있는 인덱스 번호 
```

</details>

---

<details>
<summary><strong style="font-size:1.17em">Coin Change</strong></summary>

https://leetcode.com/problems/coin-change/

```java
class Solution {
    public int coinChange(int[] coins, int amount) {


        int[] dp = new int[amount+1];
        Arrays.fill(dp, -1);
        dp[0] = 0;
        
        

        for(int i = 1; i <= amount; i++){
            for(int coin : coins){
                if(i >= coin && dp[i-coin] != -1){
                    dp[i] = dp[i] == -1 ? dp[i-coin] + 1 
                                        : Math.min(dp[i-coin] + 1, dp[i]);
                }
            }
        }


        return dp[amount];
    }
}

// coins에 있는 숫자를 조합해서 amount가 될때 이 개수의 최소값
// 각 요소는 여러번 쓸 수 있습니다
// 조합이 안되면 -1반환

// 12
// [5,4,1]
// 4 + 4 + 4  = 12
// 5 + 5 + 1 + 1 = 12 -> 4를 반환 x
// 브루드 포스 불가능

// dp[0] = 0
// 1부터 시작
// dp[1] -> 1,4,5 모두 확인 
// dp[2] -> dp[2-1], dp[2-4], dp[2-5]
// dp[3] -> dp[3-1], dp[3-4], dp[3-5]
// dp[4] -> 

```

</details>

---

<details>
<summary><strong style="font-size:1.17em">Course Schedule</strong></summary>


https://leetcode.com/problems/course-schedule/

```java


class Solution {


    private List<List<Integer>> graph;
    private int[] visited;

    public boolean canFinish(int numCourses, int[][] prerequisites) {
        // 그래프 초기화
        graph = new ArrayList<>();

        for(int i = 0; i < numCourses; i++){
            graph.add(new ArrayList<>());
        }

        for(int[] pre: prerequisites){
            graph.get(pre[0]).add(pre[1]);
        }

        visited = new int[numCourses];

        for(int i = 0; i < numCourses; i++){
            if(visited[i] == 0 && !dfs(i)){
                return false;
            }
        }

        return true;
    }

    private boolean dfs(int v){
        visited[v] = 1;

        for(int node: graph.get(v)){
    
            if(visited[node] == 1) return false;
            if(visited[node] == 0 && !dfs(node)) return false;
        }


        visited[v] = 2;
        return true;
    }
}
```

</details>


---


<details>
<summary><strong style="font-size:1.17em">Find Peak Element</strong></summary>

https://leetcode.com/problems/find-peak-element/

right = mid -1 인데 mid로 값을 설정하면 무한루프가 돌 수도 있으니 주의해야한다. 

```java
class Solution {
    public int findPeakElement(int[] nums) {
        int n = nums.length;
        if(n==1){
            return 0;
        }


        int left = 0;
        int right = n-1;

        while(left <= right){
            int mid = left + (right - left)/ 2;
            int element = nums[mid];
            int leftElement = mid-1 < 0 ? Integer.MIN_VALUE : nums[mid-1];
            int rightElement = mid+1 > n-1 ? Integer.MIN_VALUE : nums[mid+1];

            if(leftElement < element && element > rightElement){
                return mid;
            }else if(leftElement > element){
                right = mid -1;
            }else{
                left = mid+1;
            }
        }

        return left;


    }   

}

// peak요소를 찾아라
// peak요소는 이웃 요소들 보다 크면 되고, 여러개의 peak면 그중 하나만 인덱스를 반환 

// [1,2,1,3,5,6,4]
// [1 or 5]

// O(log n)


// 시작인덱스, 끝인덱스 [끝인덱스-시작인덱스] == 3일때 왼쪽 오른쪽 중간 비교 하기 


/// 1,4,3,4,5,6
```

</details>

---

<details>
<summary><strong style="font-size:1.17em"> Binary Tree Level Order Traversal
</strong></summary>

https://leetcode.com/problems/binary-tree-level-order-traversal/description/

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
    public List<List<Integer>> levelOrder(TreeNode root) {
        if(root == null){
            return Collections.emptyList();
        }

        List<List<Integer>> result = new ArrayList<>();

        Queue<TreeNode> treeQueue = new LinkedList<>();
        treeQueue.offer(root);

        while(!treeQueue.isEmpty()){
            List<TreeNode> curNodes = new ArrayList<>();
            List<Integer> r = new ArrayList<>();
            int size = treeQueue.size();
            for(int i = 0; i < size; i++){
                TreeNode cur = treeQueue.poll();
                if(cur != null){
                    r.add(cur.val);
                    curNodes.add(cur);
                }
            }

            if(!r.isEmpty()){
                result.add(r);
            }

            for(int i = 0; i < curNodes.size(); i++){
                if(curNodes.get(i).left != null){
                    treeQueue.offer(curNodes.get(i).left);
                
                }
                if(curNodes.get(i).right != null){
                    treeQueue.offer(curNodes.get(i).right);
                
                }
            }

        }

        return result;

    }
}

// 레벨별로 List를 담는다
// root만 주어짐 -> bfs
```

</details>