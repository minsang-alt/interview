
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
