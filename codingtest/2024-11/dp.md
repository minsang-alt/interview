## 오늘은 DP를 공부 했지요

DP를 사용하기 위한 두 가지 중요한 조건입니다:

### 중복되는 부분 문제(Overlapping Subproblems)

큰 문제가 작은 문제들로 쪼개질 수 있고
이 작은 문제들이 여러 번 재사용된다는 뜻
예: 피보나치에서 F(3)은 F(5), F(4) 계산할 때 모두 필요함

### 최적 부분 구조(Optimal Substructure)

작은 문제들의 최적해를 조합해서
큰 문제의 최적해를 만들 수 있다는 뜻
예: F(5) = F(4) + F(3) 처럼 작은 문제들의 답을 합치면 큰 문제의 답이 됨

### DP 문제의 첫 번째 특징

```text
최소값 찾기

"~하는데 필요한 최소 비용은?"
예: 계단 오르는 최소 비용


최대값 찾기

"~로 얻을 수 있는 최대 이익은?"
예: 도둑이 훔칠 수 있는 최대 금액


방법의 수 세기

"~를 하는 방법이 몇 가지야?"
예: 타일을 채우는 방법의 수


최대 길이 찾기

"가장 긴 ~는 무엇일까?"
예: 가장 긴 증가하는 부분 수열


도달 가능성 확인

"특정 지점에 도달할 수 있을까?"
예: 점프해서 끝점까지 갈 수 있나?



쉽게 말해서, DP는 주로:

"최대/최소"를 찾거나
"몇 가지 방법이 있는지" 세거나
"가능한지 아닌지" 확인하는 문제에 사용됩니다!

이런 유형의 문제를 보면 "아, DP를 써야 하나?" 하고 생각해보면 좋습니다 
```

### 그리디인지 DP인지 어떻게 알까?

```text
DP 문제에서 흔히 나타나는 두 번째 특징은 미래의 "결정"이 이전 결정에 달려 있다는 것입니다. 
한 단계에서 어떤 일을 하기로 결정하면 이후 단계에서 어떤 일을 하는 능력에 영향을 미칠 수 있습니다. 
이러한 특성으로 인해 그리디 알고리즘이 DP 문제에 유효하지 않게 됩니다. 이전 결정의 결과를 고려해야 합니다. 
물론 이 특성은 첫 번째 특성만큼 잘 정의되어 있지 않으며 이를 식별하는 가장 좋은 방법은 몇 가지 예를 살펴보는 것입니다.
```

---

## 문제 1  ✅

https://leetcode.com/problems/climbing-stairs/description/

## 문제 2  ✅

https://leetcode.com/problems/min-cost-climbing-stairs/description

## 문제 3  ✅

https://leetcode.com/problems/n-th-tribonacci-number/?envType=study-plan-v2&envId=dynamic-programming

## 문제 4  ✅

https://leetcode.com/problems/house-robber/description/?envType=study-plan-v2&envId=dynamic-programming

## 문제 5  ✅

https://leetcode.com/problems/delete-and-earn/description/?envType=study-plan-v2&envId=dynamic-programming

## 문제 6  ✅

https://leetcode.com/problems/unique-paths/description/?envType=study-plan-v2&envId=dynamic-programming

## 문제 7  ✅

https://leetcode.com/problems/minimum-path-sum/description/?envType=study-plan-v2&envId=dynamic-programming

## 문제 8  ✅

https://leetcode.com/problems/unique-paths-ii/description/?envType=study-plan-v2&envId=dynamic-programming

## 문제 9  ✅

https://leetcode.com/problems/triangle/description/?envType=study-plan-v2&envId=dynamic-programming

## 문제 10  ✅

https://leetcode.com/problems/minimum-falling-path-sum/description/?envType=study-plan-v2&envId=dynamic-programming

## 문제 11  ✅

https://leetcode.com/problems/maximal-square/description/?envType=study-plan-v2&envId=dynamic-programming

## 문제 12  ✅

https://leetcode.com/problems/longest-palindromic-substring/description/?envType=study-plan-v2&envId=dynamic-programming

## 문제 13  ✅

https://leetcode.com/problems/word-break/


---

## LCS (Longest Common Subsequence) 

LCS 푸는 방법: https://velog.io/@emplam27/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C-%EC%95%8C%EC%95%84%EB%B3%B4%EB%8A%94-LCS-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-Longest-Common-Substring%EC%99%80-Longest-Common-Subsequence

## 문제 14  ✅

https://leetcode.com/problems/longest-common-subsequence/

## 문제 15  ✅

https://leetcode.com/problems/longest-palindromic-subsequence/

## 문제 16  ✅

https://leetcode.com/problems/edit-distance/description/