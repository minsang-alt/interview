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

### 1분 자기소개

```text
1. 저는 기록을 통한 학습과 팀원 간 지식 공유를 매우 중요하게 생각합니다. 이를 통해 빠르게 변화하는 환경에서도 팀이 함께 성장할 수 있도록 기여할 수 있습니다

```

### 리더형인가요 팔로워형인가요?

```text
저는 팔로워형에 가깝다고 생각합니다.
이유는 필요할 경우 저는 주어진 역할에 집중하여 맡은 일을 성실하게 수행하고, 팀의 목표 달성을 위해 리더에게 지시를 기다리는 대신에 필요한 일을 스스로 찾아서 처리하는 편입니다.

예시로는 예전에 한 프로젝트를 진행했을 때 였는데요. 프로젝트 리딩하는 분이 프로젝트 마감 달 동안은 기능구현에 집중하자고 하였고, 모두 다 동의한 상태였습니다.
하지만, 프로젝트 발표일이 약 10일이 남은 상태에서도 팀원들이 명확한 일정 계획 없이 기능을 개발하고 있었습니다. 
계산을 해보니 실제로 기능 개발을 할 수 있는 기간은 7,8일 정도였고 나머지는 예상치 못한 버그 수정과 발표 준비에 할애해야 했습니다.

하지만 백엔드 역할을 맡은 저는 맡은 부분은 모두 해결했지만 프론트엔드 팀에서 어디까지 구현이 끝났는지 Jira에서도 티켓을 발행하지 않아 미지수 상태였고 마감까지 원하는 목표에 도달할 수 있을지
매우 불확실한 상태였습니다.

그래서 리더겸 프론트엔드 팀장에게 이 상황을 인지시키고 정확한 진행상황을 파악하기 위해 프론트엔드 팀과 회의를 소집했습니다. 

회의에서 저는 프론트엔드 팀원들이 각자의 역량을 평가하고, / 남은 각각의 기능들에 대해 / 얼마만큼의 시간이 걸릴것 같은지 객관적으로 판단하려고 노력했습니다.
그리고나서 남은 기능들의 우선순위를 재정립했습니다. 시간 소모가 크면서 중요도가 낮은 기능은 과감히 제외하고, 통합 및 배포 과정에서 발생할 수 있는 오류에 대비해 충분한 시간을 배정했습니다.  

이러한 접근 방식을 통해 저희 팀은 발표날에 완성도 있는 프로젝트를 제출했고 발표대비도 철저히 하여 우수상을 받게 되었습니다.
```

참고로 리더형은 의견을 모으고 결정할 줄 알아야한다. 

### 우리회사 왜 지원했나요? (지원동기) == 라인에 지원한 동기는 무엇인가요

```text


```

### 회사에 대해 궁금한 점 있나요?

```text
- 일본쪽에 서비스 하시려고 하는 걸로 알고있는데 어떤 계획이나 릴리즈 시점이나 혹시 그런게 있을까요?
- 그리고 말하기 조심스러운데 유튜브 뮤직이 되게 압도적인데 어떤 계획이 있으실까 궁금했습니다.
- 최근 NoSQL 데이터베이스에 대해 공부하고 있어서 그런데요, 회사에서는 MongoDB를 어떤 용도로 주로 활용하고 계신지 궁금합니다. 
```

### 동시에 여러 가지 일이 맡겨진 경우 어떻게 하겠는가?

```text

```

### 10년 뒤의 본인의 모습

```text

```

### 자율성이 높은 환경에서 일할 때의 장단점은 무엇이라고 생각하십니까? 개인적인 경험이 있다면 공유해 주세요

```text

```

### 자율적인 조직과 시스템화된 조직 차이점 == 시스템기반으로 돌아가는 조직과 구성원의 자율적역량이 최대한 발휘되는 조직간의 장단

```text
일단 이 둘의 차이점은 
자율적인 조직은 구성원들간 합의된 원칙 하에서 성과에 집중하여 일할 수 있도록 합니다. 그래서 스스로 경쟁하고, 자발적으로 새로운 시도를 해야 합니다.

시스템 기반으로 돌아가는 조직은 정해진 규칙과 절차에 따라 업무를 수행하며, 효율성과 일관성을 중시합니다. 
이러한 조직에서는 역할과 책임이 명확하게 분담되어 있어 업무 프로세스가 체계적으로 운영됩니다. 따라서 업무의 예측 가능성이 높고, 오류나 실수가 최소화될 수 있습니다.   

따라서 제 생각은 조직의 핵심 코어는 표준화하여 효율성과 일관성을 확보합니다.이를 통해 기본적인 운영은 안정적으로 유지하면서도 오류를 최소화할 수 있습니다.
그리고 구성원들에게 목표 달성을 위한 방법과 수단에 대한 자율성을 부여합니다. 각자의 전문성과 창의성을 활용하여 혁신적인 아이디어를 도출할 수 있도록 합니다.

또한,조직의 비전과 목표를 명확하게 제시하고, 이를 구성원들과 공유합니다. 이를 통해 구성원들이 자율적으로 움직이면서도 조직의 방향성과 일치하도록 유도합니다.
```

### 자유로운 조직에서 리더와 구성원이 각각 해야할 일이 무엇일까요?

```text
리더는 오늘 무엇을 했느냐에 대한 관리보다는 성과를 내기 위해 어떤 노력을 하고 있는지를 확인해야합니다. -> 전자는 업무 나열식 대답, 후자는 기존에 하지않았던 새로운 방식
또한, 구성원들의 고민방향을 좀 더 생산적으로 될 수 있도록 도와주어야합니다.

구성원은 각자 할 일을 관리하고 성과를 내기 위해서는 역량이 있어야 합니다. 그리고 성과를 증명해내야 합니다.  
```

### 팀 내에서 자율성을 높이면서도 전체적인 방향성을 잃지 않게 하려면 어떻게 해야 할까요?

```text
팀의 목표와 비전이 있어야하며 구성원들은 이를 숙지하고 본인의 역량에 따라 이를 실현시키기 위해 성과를 내야 합니다.  
```

### 본인의 단점이 뭐라고 생각하나요?

```text
관심분야나 제게 필요하다고 느끼는 것 이외에 것은 전혀 신경을 안씁니다. 그래서 남들과 대화를 할 때 개발이외 분야에서는 조금 공감대를 느끼기 힘듭니다.

인스타를 둘러보거나 다른 분야의 친구들과 만나 요즘 관심있는 게 뭔지 파악하려고 노력하고 있습니다.  
```

### 영어점수가 낮은거같은데 해외사람들이랑 일해야할텐데 가능할까요?

```text
언어의 장벽 때문에 대화의 이해도를 떨어뜨릴 수 있기 때문에 
계속해서 질문하고 반박하면서 회의나 토론을 많이 해서 좋은 결론에 도달할 수 있도록 노력하고자 합니다. 
```

### 마지막 어필

```text
저는 단순한 기술 구현이 아니라 LINE Music이 추구하는 음악의 진보와 긍정적 영향력 확대에 함께 기여하고 싶습니다. 
새로운 기술을 통해 더 많은 사람들이 음악을 쉽게 접하고, 음악을 통해 긍정적인 변화를 이끌어낼 수 있는 서비스 개발에 일조하고 싶습니다. 
저에게 이 기회를 주신다면 LINE Music의 성공을 위해 최선을 다하겠습니다. 
```