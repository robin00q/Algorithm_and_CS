# 종만북 12.1 DARPA Grand Challenge

[https://algospot.com/judge/problem/read/DARPA](https://algospot.com/judge/problem/read/DARPA)
~~~
최적화 문제 : n대의 카메라를 모두 배치하면서 카메라 간의 최소 간격이 최대치 인 것을 반환하라.

결정 문제 : n대의 카메라 개수가 주어질 때 적절히 배치하면 특정 간격 이상이 되도록 할 수 있는가? (boolean)
~~~

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;
import java.util.StringTokenizer;

public class Main {
	public static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	public static Scanner sc = new Scanner(System.in);
	public static StringTokenizer st;
	
	public static List<Double> locations;
	
	public static void main(String[] args) throws NumberFormatException, IOException {

		int iterator = sc.nextInt();

		while ((--iterator) >= 0) {
			solve();
		}
	}

	public static void solve() throws IOException {
		
		int cameras = sc.nextInt();
		int m = sc.nextInt();
		List<Double> locations = new ArrayList<Double>();
		
		for(int i = 0 ; i < m ; i++) {
			double input = sc.nextDouble();
			locations.add(input);
		}
		
		double answer = optimize(locations, cameras);
		
		System.out.println(Math.round(answer*100)/100.0);
	}

	private static double optimize(List<Double> locations, int cameras) {
		double lo = 0;
		double hi = 241;
		
		for(int it = 0 ; it < 100 ; it++) {
			double mid = (lo + hi) / 2.0;
			if(decision(locations, cameras, mid)) {
				lo = mid;
			} else {
				hi = mid;
			}
		}
		
		return lo;
		
	}

	private static boolean decision(List<Double> locations, int cameras, double gap) {
		
		double limit = -1;
		int installed = 0;
		for(int i = 0 ; i < locations.size() ; i++) {
			if(limit <= locations.get(i)) {
				installed++;
				limit = locations.get(i) + gap;
			}
		}
		
		if(installed >= cameras) {
			return true;
		}
		
		return false;
	}
	
}

```