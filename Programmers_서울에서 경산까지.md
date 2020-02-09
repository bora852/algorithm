```java
import java.util.Arrays;

class Solution {
    public int solution(int K, int[][] travel) {
        int answer = 0;
        
        //도시 수,  3 이상 100 이하
        //시간, K는 0보다 크고 100,000
        int[][] dp = new int[101][100001];
        dp[0][travel[0][0]] = travel[0][1];
        dp[0][travel[0][2]] = travel[0][3];
        
        //travel
        //[도보 이동 시간, 도보 이동 모금액, 자전거 이동 시간, 자전거 이동 모금액]
        for(int i = 1; i < travel.length; i++) {
        	for(int j = 0; j <= K; j++) {
        		if(dp[i - 1][j] == 0) continue;
        		if( (j + travel[i][0]) <= K 
    				&& (dp[i][j + travel[i][0]]) < (dp[i - 1][j] + travel[i][1]) ) {
        			dp[i][j + travel[i][0]] = dp[i - 1][j] + travel[i][1];
        			answer = Math.max(answer, dp[i][j + travel[i][0]]);
        		}
        		if(j + travel[i][2] <= K
    				&& dp[i][j + travel[i][2]] < dp[i - 1][j] + travel[i][3]) {
        			dp[i][j + travel[i][2]] = dp[i - 1][j] + travel[i][3];
        			answer = Math.max(answer, dp[i][j + travel[i][2]]);
        		}
        	}
        }
        
        return answer;
    }
}

public class Programmers {
	public static void main(String[] args) {
		Solution sol = new Solution();
		System.out.println(sol.solution(1660, new int[][]{{500, 200, 200, 100}, {800, 370, 300, 120}, {700, 250, 300, 90}}));
	}
}
```

