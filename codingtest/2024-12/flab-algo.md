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