# Search in Rotated Sorted Array

[https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/530/week-3/](https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/530/week-3/)
~~~
순환하는 배열에서 원하는 값을 찾기

이분탐색을 사용

어떤 원소와 맨 앞의원소를 비교해 현재 중간값에서 좌, 우로 이동할 지 결정
~~~

```java
class Solution {
	public int search(int[] nums, int target) {
		int n = nums.length;
		if (n == 0) {
			return -1;
		}

		int l = 0;
		int r = n - 1;
		
		int first = nums[0];

		while (l <= r) {
			int mid = l + (r - l) / 2;
			int value = nums[mid];
			
			if(value == target) {
				return mid;
			}
			
			boolean iamBig = value >= first;
			boolean targetBig = target >= first;
			
			if(iamBig == targetBig) {
				if(value >= target) {
					r = mid - 1;
				} else {
					l = mid + 1;
				}
			} else {
				if(targetBig) {
					r = mid - 1;
				} else {
					l = mid + 1;
				}
			}

		}
		
		return -1;
	}

}
```