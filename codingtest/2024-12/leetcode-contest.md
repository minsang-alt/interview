
---

<details>
<summary><strong style="font-size:1.17em">Button with Longest Push Time</strong></summary>

https://leetcode.com/contest/weekly-contest-428/problems/button-with-longest-push-time/description/


```java
class Solution {
    public int buttonWithLongestTime(int[][] events) {

        if(events.length==1){
            return events[0][0];
        }

        // 순회하여 차이값 저장 
        int[] timeGap = new int[events.length];
        timeGap[0] = events[0][1];
        for(int i = 1; i < events.length; i++){
            timeGap[i] = events[i][1]-events[i-1][1];
        }

        // 뒤 부터 순회하며 가장 오랜걸린시간이 나오면 인덱스 업데이트
        int smallIndex = -1;
        int maxTimeGap = -1;
        for(int i = events.length -1; i>=0; i--){
            int idx = events[i][0];
            if(maxTimeGap == timeGap[i] && smallIndex > idx){
                smallIndex = idx;
            }else if(maxTimeGap < timeGap[i]){
                maxTimeGap = timeGap[i];
                smallIndex = idx;
            }
        }

        return smallIndex;
        
    }
    // 오름차순 시간
    // 버튼을 누르는데 가장 오랜 걸린 시간의 인덱스 반환
    // 동일한 차이 시간이면 가장 작은 인덱스 반환 
}

```

</details>

---

<details>
<summary><strong style="font-size:1.17em">Minimum Remove to Make Valid Parentheses</strong></summary>

https://leetcode.com/problems/minimum-remove-to-make-valid-parentheses/

O(N)이지만 느림 
```java
class Solution {
    public String minRemoveToMakeValid(String s) {
        // left -> right
        int leftNum = 0;
        int rightNum = 0;

        StringBuilder sb = new StringBuilder();
        for(char c : s.toCharArray()){
            if(c=='('){
                leftNum++;
            }else if(c==')' && leftNum < rightNum +1){
                continue;
            }else if(c==')'){
                rightNum++;
            }

            sb.append(c);
        }

        s = sb.toString();
        System.out.println(s);


        // right -> left  
        sb = new StringBuilder();
        leftNum = 0;
        rightNum = 0;

        for (int i = s.length() - 1; i >= 0; i--) {
            char c = s.charAt(i);
            if (c == ')') {
                rightNum++;
            } else if (c == '(' && leftNum + 1 > rightNum) {
                continue;
            } else if (c == '(') {
                leftNum++;
            }
            sb.insert(0, c);  
        }

        return sb.toString();

    }
}

```

인덱스와 스택으로 해결하는 방법

```java
public String minRemoveToMakeValid(String s) {
  StringBuilder sb = new StringBuilder(s);
  Stack<Integer> st = new Stack();
  for (int i = 0; i < sb.length(); ++i) {
    if (sb.charAt(i) == '(') st.add(i + 1);
    if (sb.charAt(i) == ')') {
      if (!st.empty() && st.peek() >= 0) st.pop();
      else st.add(-(i + 1));
    }
  }
  while (!st.empty())
    sb.deleteCharAt(Math.abs(st.pop()) - 1);
  return sb.toString();
}
```

</details>