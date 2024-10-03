## 코딩 테스트

**미완성 코드**

```java
package com.flab.book_challenge;


import java.util.HashMap;
import java.util.Map;

public class Main {

    public static void main(String[] args) {
        Solution sol = new Solution();

        // 테스트 케이스
        System.out.println(sol.solution(new int[]{2, 3, 1, 4}, 3));  // 예상 출력: 3
        System.out.println(sol.solution(new int[]{1, 2, 3, 4}, 5));  // 예상 출력: 4
        System.out.println(sol.solution(new int[]{1, 2, 3, 4}, 20));  // 예상 출력: 4
    }

    static class Solution {
        public int solution(int[] play_list, int listen_time) {
            int n = play_list.length;

            int maxSongs = 0;
            int uniqueSongs = 0;
            Map<Integer, Integer> songCount = new HashMap<>();

            // 초기 윈도우 설정
            for (int i = 0; i < listen_time && i < n * 2; i++) {
                if (songCount.getOrDefault(i % n, 0) == 0) {
                    uniqueSongs++;
                }
                songCount.put(i % n, songCount.getOrDefault(i % n, 0) + 1);

            }

            maxSongs = uniqueSongs;

            // 슬라이딩 윈도우
            for (int i = listen_time; i < n * 2; i++) {
                // 윈도우의 시작 부분 제거
                int removeIndex = i - listen_time;
                songCount.put(removeIndex % n, songCount.get(removeIndex % n) - 1);
                if (songCount.get(removeIndex % n) == 0) {
                    uniqueSongs--;
                }

                // 윈도우의 끝에 새로운 부분 추가
                if (songCount.getOrDefault(i % n, 0) == 0) {
                    uniqueSongs++;
                }
                songCount.put(i % n, songCount.getOrDefault(i % n, 0) + 1);

                maxSongs = Math.max(maxSongs, uniqueSongs);

                // 모든 곡을 들었다면 종료
                if (maxSongs == n) {
                    break;
                }
            }

            return maxSongs;
        }


    }
}
```

완벽한 코드
```java

package com.example.javaspring.codingTest;

import java.util.Arrays;
import java.util.HashSet;
import java.util.Set;

public class Main {

    public static void main(String[] args) {
        Solution sol = new Solution();

        // 테스트 케이스
        System.out.println(sol.solution(new int[]{2, 3, 1, 4}, 3));  // 예상 출력: 3
        System.out.println(sol.solution(new int[]{1, 2, 3, 4}, 5));  // 예상 출력: 4
        System.out.println(sol.solution(new int[]{1, 2, 3, 4}, 20));  // 예상 출력: 4
        System.out.println(sol.solution(new int[]{2, 2, 4, 4}, 5));  // 예상 출력: 3 7~12 0,2,4,8,12,14
        System.out.println(sol.solution(new int[]{2, 1, 3, 2, 1}, 2));  // 예상 출력: 2
    }

    static class Solution {
        public int solution(int[] play_list, int listen_time) {
            int n = play_list.length;
            int totalTime = Arrays.stream(play_list).sum();

            // 전체 재생 시간이 듣는 시간보다 짧으면 모든 곡을 들을 수 있음
            if (totalTime <= listen_time) {
                return n;
            }

            // 누적 재생 시간 계산
            int[] cumulativeTime = new int[n * 2 + 1];
            for (int i = 0; i < n * 2; i++) {
                cumulativeTime[i + 1] = cumulativeTime[i] + play_list[i % n];
            }

            int maxUnique = 0;

            // 모든 가능한 시작 지점에 대해 검사
            for (int start = 0; start < totalTime; start++) {
                int end = start + listen_time;
                int startSong = findSong(cumulativeTime, start);
                int endSong = findSong(cumulativeTime, end);

                // unique한 곡의 수 계산
                Set<Integer> uniqueSongs = new HashSet<>();
                for (int i = startSong; i < endSong; i++) {
                    uniqueSongs.add(i % n);
                }
                // endSong이 정확히 곡의 시작점이 아니라면 마지막 곡도 포함
                if (cumulativeTime[endSong] != end) {
                    uniqueSongs.add(endSong % n);
                }

                maxUnique = Math.max(maxUnique, uniqueSongs.size());

                if (maxUnique == n) {
                    break; // 모든 곡을 들었다면 종료
                }
            }

            return maxUnique;
        }

        // 주어진 시간에 해당하는 곡의 인덱스를 찾는 메소드
        private int findSong(int[] cumulativeTime, int time) {
            int left = 0, right = cumulativeTime.length - 1;
            while (left < right) {
                int mid = left + (right - left) / 2;
                if (cumulativeTime[mid] > time) {
                    right = mid;
                }
                else {
                    left = mid + 1;
                }
            }
            return left - 1;
        }
    }

}
```

### 코딩테스트에서 어려웠던 점 있나요?

### 잘 풀었다고 생각하시나요?

### 문제를 처음 접했을 때 어떤 접근 방식을 선택했나요?

### 문제를 어떻게 분석하고, 어떤 핵심 조건을 파악했나요?

### 이 알고리즘이나 데이터 구조를 선택한 이유는 무엇인가요?

### 시간 복잡도와 공간 복잡도를 어떻게 고려했나요?

### 이 코드를 어떻게 개선할 수 있을까요?

### 시간이 더 있었다면 어떤 부분을 더 수정했을까요?

## 우리회사 왜 지원했나요?

```text
대규모 음악 파일과 메타데이터 실시간 스트리밍 데이터를 어떻게 처리할 수 있을까 궁금해서 지원했습니다
  
```

## 회사에 대해 궁금한 점 있나요?

```text
- 최근 NoSQL 데이터베이스에 대해 공부하고 있어서 그런데요, 회사에서는 MongoDB를 어떤 용도로 주로 활용하고 계신지 궁금합니다. 
```