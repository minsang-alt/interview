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
