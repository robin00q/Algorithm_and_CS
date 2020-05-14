# Check If It Is a Straight Line

[https://leetcode.com/explore/challenge/card/may-leetcoding-challenge/535/week-2-may-8th-may-14th](https://leetcode.com/explore/challenge/card/may-leetcoding-challenge/535/week-2-may-8th-may-14th)

~~~
기울기를 확인하여 직선인지 확인
~~~

```java
class Solution {
	public boolean checkStraightLine(int[][] coordinates) {
		int fX = coordinates[0][0];
		int fY = coordinates[0][1];
		
		int sX = coordinates[1][0];
		int sY = coordinates[1][1];
		
		double initIncline = ((double)(fX - sX) / (double)(fY - sY));

		for (int i = 2; i < coordinates.length; i++) {
			int x = coordinates[i][0];
			int y = coordinates[i][1];
			
			double inclineOthers = ((double)(fX - x) / (double)(fY - y));
            
			if(Math.abs(initIncline) != Math.abs(inclineOthers)) {
				return false;
			}
		}

		return true;
	}
}
```