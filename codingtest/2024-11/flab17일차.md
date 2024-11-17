## Valid Anagram

https://leetcode.com/problems/valid-anagram/
- 24분
- Easy
- solved

```java
import java.util.*;
class Solution {
    public boolean isAnagram(String s, String t) {
        // s와 t가 같은 구성요소인지 물어보는 문제 
        // 즉 t의 요소로 s가 만들어져야 한다.

        // 제한도, 무조건 소문자, 5만 이하의 글자 



        // 길이 부터 같은 지 판단 
        if(s.length()!=t.length()){
            return false;
        }

        // 같으면 
        // s를 먼저 해시테이블에 저장 키:값(개수)
        Map<Character, Integer> map = new HashMap<>();
        for(char c: s.toCharArray()){
            map.put(c,map.getOrDefault(c,0)+1);
        }


        // t를 읽으며 있는 지 판단 
        for(char c : t.toCharArray()){
            if(!map.containsKey(c) || map.get(c) == 0){
                return false;
            }

            map.put(c,map.get(c)-1);
        }

        return true;

        // 시간 복잡도

    }
}
```

## Rotting Oranges

https://leetcode.com/problems/rotting-oranges/

- Fail


```java
class Solution {
    public int orangesRotting(int[][] grid) {
        // bfs 
        // 썩은 오렌지 위치 큐에 넣기 
        // 셸 상태를 저장하기 위해 방문표시 

        // 처음엔 신선한 오렌지 개수 세기
        // 썩은건 큐에 

        int N = grid.length;
        int M = grid[0].length;
        int[][] visited = grid;

        Queue<int[]> q = new LinkedList<>();
        int countFreshOrange = 0;

        for(int i = 0; i < N; i++){
            for(int j = 0; j < M; j++){
                if(visited[i][j] == 2){
                    q.offer(new int[]{i,j});
                }
                if(visited[i][j] == 1){
                    countFreshOrange++;
                }
            }
        }

        if(countFreshOrange==0)return 0;
        if(q.isEmpty()) return -1;

        int minutes = -1;
        int[][] dirs = {{1,0},{-1,0},{0,-1},{0,1}};
        while(!q.isEmpty()){
            int size = q.size();
            while(size-- > 0){
                int[] cell = q.poll();
                int x = cell[0];
                int y = cell[1];
                for(int[] dir : dirs){
                    int i = x + dir[0];
                    int j = y + dir[1];
                    if(i >=0 && i < N && j >= 0 && j < M && visited[i][j] ==1){
                        visited[i][j] = 2;
                        countFreshOrange--;
                        q.offer(new int[]{i,j});
                    }
                }

            }
            minutes++;
        }

        if(countFreshOrange==0)return minutes;
        return -1;
    }
}
```