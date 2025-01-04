<details>
<summary><strong style="font-size:1.17em">Maximum Units on a Truck</strong></summary>

https://leetcode.com/problems/maximum-units-on-a-truck/description/

O(nlogn)으로 풀 수 있는 문제입니다. 정렬 + 그리디로 풀 수 있습니다.

```java
class Solution {
    public int maximumUnits(int[][] boxTypes, int truckSize) {
        Arrays.sort(boxTypes, (a,b)-> b[1]-a[1]); // 이거 오버플로우 날 수 있음 : Integer.compare(b[1], a[1])

        int result = 0;

        for(int i=0; i < boxTypes.length; i++){
            int size = boxTypes[i][0];
            int cost = boxTypes[i][1];

            if(truckSize < size){
                result += cost*(truckSize);
                break;
            }

            result += cost*size;
            truckSize-=size;
        }

        return result;
    }

//    50+ 27 +  14
}
```


</details>