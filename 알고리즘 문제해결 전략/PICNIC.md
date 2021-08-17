# PICNIC

## 입력
```
3
2 1
0 1
4 6
0 1 1 2 2 3 3 0 0 2 1 3
6 10
0 1 0 2 1 2 1 3 1 4 2 3 2 4 3 4 3 5 4 5

```
## 소스코드
```java
import java.io.InputStreamReader;
import java.io.BufferedReader;
import java.io.IOException;
 
public class Main {
	private static boolean[][] areFriends;
	private static int n;
	public static void main(String args[]) throws IOException{
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringBuilder sb = new StringBuilder();
		
		boolean[] taken;
		int testCase = Integer.parseInt(br.readLine());
		String result = "";
		for(int j=0; j < testCase; j++) {
			String[] line = br.readLine().split(" ");
			n = Integer.parseInt(line[0]);
			int friendCount = Integer.parseInt(line[1]);
			areFriends = new boolean[10][10];
			for(int i=0; i< friendCount; i++) {
				line = br.readLine().split(" ");
				int a = Integer.parseInt(line[0]);
				int b = Integer.parseInt(line[1]);
				
				areFriends[a][b] = areFriends[b][a] = true;
			}
			boolean[] data = new boolean[10];
			result += (j +1 == testCase) ? countPairings(data) : countPairings(data) + "\n";
		}
		System.out.println(result);
	}
	public static int countPairings(boolean[] taken) {
		int firstFree = -1;
		int n = taken.length;
		for(int i=0; i<n;i++) {
			if(!taken[i]) {
				firstFree = i;
				break;
			}
		}
		if(firstFree ==-1) return 1;
		int ret = 0;
		
		for(int pairWith = firstFree+1; pairWith < n; pairWith++) {
			if(!taken[pairWith] && areFriends[firstFree][pairWith]) {
				taken[firstFree] = taken[pairWith] = true;
				ret += countPairings(taken);
				taken[firstFree] = taken[pairWith] = false;
			}
		}
		return ret;
	}
}
```
