<details>
<summary><strong style="font-size:1.17em">Range Sum of BST</strong></summary>

https://leetcode.com/problems/range-sum-of-bst/description/

```java
class Solution {
    public int rangeSumBST(TreeNode root, int low, int high) {
        if(root == null) return 0;
        if(root.val < low) return rangeSumBST(root.right,low,high);
        if(root.val > high) return rangeSumBST(root.left,low,high);

        return root.val + rangeSumBST(root.left,low,high) + rangeSumBST(root.right,low,high);
    }
}
```

```java
class Solution {
    public int rangeSumBST(TreeNode root, int low, int high) {
        if(root == null) return 0;
        int sum = 0;
        if(root.val >= low && root.val <=high) sum+= root.val;

        return sum + rangeSumBST(root.left, low, high) + rangeSumBST(root.right,low,high);
    }
}
```




</details>


---

<details>
<summary><strong style="font-size:1.17em">Asteroid Collision</strong></summary>

https://leetcode.com/problems/asteroid-collision/description/

```java
class Solution {
    public int[] asteroidCollision(int[] asteroids) {
        Deque<Integer> st = new LinkedList<>();

        for(int num : asteroids){
            if(st.size() > 0){
                int n = st.peek();
                if((n>0 && num >0) || (n < 0 && num <0) || (num >0 && n <0)){
                    st.push(num);
                }else{
                    collite(st,num,n);
                }

            }else{
                st.push(num);
            }
        }

        int size = st.size();
        //System.out.println("size: " + size);
        int[] result = new int[size];
        for(int i = size-1; i >=0; i--){
            result[i] = st.pop();
        }

        return result;
    }


    private void collite(Deque<Integer> st, int num, int nInSt){

        if((nInSt>0 && num >0) || (nInSt < 0 && num <0)){
            st.push(num);
            return;
        }
        if(nInSt < 0 && num >0){
            st.push(num);
            return;
        }
        if(Math.abs(num) > Math.abs(nInSt)){
            st.pop();
            if(st.size() <= 0){
                st.push(num);
                return;
            }
            collite(st, num, st.peek());
        }else if(Math.abs(num) == Math.abs(nInSt)){
            st.pop();
        }

    }
}

// 두 소행성이 만나면 
// -> <- 크기 같을 때는 둘 다 폭발 다르면 작은쪽이 폭발 
// 방향이 같으면 절대 안만남 -> -> 
// 연속적으로 일어남 
// 스택 ? 
```


</details>

---

<details>
<summary><strong style="font-size:1.17em">Minimum Add to Make Parentheses Valid</strong></summary>

https://leetcode.com/problems/minimum-add-to-make-parentheses-valid/description/

O(n)으로 스택을 사용해서 풂
```java
class Solution {
    public int minAddToMakeValid(String s) {
        Deque<Character> st = new LinkedList<>();
        for(char c: s.toCharArray()){
            if(!st.isEmpty()){
                if(st.peek() == '(' && c ==')'){
                    st.pop();
                }else{
                    st.push(c);
                }
            }else{
                st.push(c);
            }
        }

        return st.size();
    }
}
```



</details>

---

<details>
<summary><strong style="font-size:1.17em">Count Binary Substrings</strong></summary>

https://leetcode.com/problems/count-binary-substrings/description/

```java
class Solution {
    public int countBinarySubstrings(String s) {
        int cur = 1;
        int prev = 0;
        int result = 0;

        for(int i = 1; i < s.length(); i++){
            if(s.charAt(i)== s.charAt(i-1)){
                // 이전 문자열과 같을 경우 현재 그룹개수를 늘림
                cur++;
            }else{
                // 문자가 바뀌면 이제 새로운 그룹으로 진입이니 그전에 이전그룹과 비교
                result += Math.min(prev,cur);
                // 현재그룹은 이제 이전그룹이 됨
                prev = cur;
                // 이제 바뀐 문자열개수 = 1로 다시초기화하고 시작
                cur = 1;
            }

        }

        // 문자열이 끝나면 이제 이전그룹과 지금까지 업데이트한 그룹 비교
        return result + Math.min(prev, cur);
    }

}  

// 연속된 이전 그룹과 연속된 현재 그룹의 개수 중 최소값이 지금까지 만들수있는 최대 만족시킬수있는 개수 
// 만족이란, 0011처럼 그룹이되있꼬, 0,1개수가 같은 것

```

</details>