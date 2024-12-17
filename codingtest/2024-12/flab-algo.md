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