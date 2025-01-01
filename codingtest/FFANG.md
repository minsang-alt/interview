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