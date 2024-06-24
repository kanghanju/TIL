## LIS(Longest Increasing Subsequence) 최장 증가 부분 수열 
#### 공부 날짜: 2024/06/24

<br><br>
### LIS(Longest Increasing Subsequence)란?
> 말 그대로 가장 길게 증가하는 '부분 수열'로 **어떤 수열에서 만들 수 있는 부분 수열 중에서 가장 길면서 오름차순을 유지하는 수열**을 LIS라고 한다. 

**부분 집합이 아님**

<br>

### LIS를 구현하는 방법 두 가지 
#### 1. DP를 활용한 LIS 구현 
> 시간 복잡도 : O(n^2)

- 원소와 이전 원소들을 비교하며 원소들 중에서 i번째 원소보다 작은 원소들 중 DP 값이 가장 큰 값에 +1을 하며 dp[i] 값을 구한다.
- 입력 값의 크기가 작을 경우에 유용하다. 

```java
public class LIS_DP {

    public static void main(String[] args) {
        int[] arr = {3,2,4,1,6};
        int[] dp = new int[arr.length];
        dp[0] = 1; //LIS의 첫 번째 원소는 항상!!! 1이다.
        
        for (int i = 1; i < arr.length; i++) {
            //첫 원소부터 i 원소 전까지 비교
            for(int j = 0; j < i; j++) {
                if(arr[j] < arr[i]) {
                    dp[i] = Math.max(dp[i],dp[j] + 1);
                }
                //증가 부분 수열의 길이는 1부터 시작하므로 0인 값을 1로 변경해준다.
                if(dp[i] == 0) {
                    dp[i] = 1;
                }
            }
        }
    }
}
```

<br>

#### 2. 이분 탐색을 활용한 LIS 구현 
> 시간 복잡도 : O(nlogn)

- 입력 값의 크기가 클 경우 이분 탐색을 활용하면 시간 복잡도를 줄일 수 있다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class LIS_Binarysearch {

    추후 추가 예정 
}

```

<br>

#### 참고자료 
[자료1](https://hstory0208.tistory.com/entry/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-LIS%EC%B5%9C%EC%9E%A5-%EC%A6%9D%EA%B0%80-%EB%B6%80%EB%B6%84-%EC%88%98%EC%97%B4%EC%9D%B4%EB%9E%80)

[자료2](https://ng-log.tistory.com/entry/%EC%B5%9C%EC%9E%A5-%EC%A6%9D%EA%B0%80-%EB%B6%80%EB%B6%84-%EC%88%98%EC%97%B4LIS-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-JAVA)
