# Best Time to Buy and Sell Stock II

[https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/528/week-1/](https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/528/week-1/)
~~~
dp로 

1. 물건을 산 경우(buy) : Math.max(buy, not buy-price[x]);
	=> 물건을 사는 경우 제일 싸게 하도록 진행
2. 물건을 사지 않은 경우(not buy) : Math.max(not buy, buy+price[x]);
    => 가지고 있는 물건이 있다면 팔 경우 이윤이 남도록 진행
~~~

```java
class Solution {
    public int maxProfit(int[] prices) {
    	
    	int buy = Integer.MIN_VALUE;
    	int notbuy = 0;
    	for (int x : prices) {
			buy = Math.max(buy, notbuy-x);
			notbuy = Math.max(notbuy, buy + x);
		}
    	
    	return notbuy;
	}
}
```