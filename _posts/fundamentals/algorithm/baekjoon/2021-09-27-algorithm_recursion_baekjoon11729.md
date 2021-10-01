---
the valayout: post
title: 백준 11729 하노이의 탑 (JAVA)
subtitle : 재귀함수 
tags: [algorithm]
author: Leena Kim
comments : true
---



# 문제

세 개의 장대가 있고 첫 번째 장대에는 반경이 서로 다른 n개의 원판이 쌓여 있다. 각 원판은 반경이 큰 순서대로 쌓여있다. 이제 수도승들이 다음 규칙에 따라 첫 번째 장대에서 세 번째 장대로 옮기려 한다.

한 번에 한 개의 원판만을 다른 탑으로 옮길 수 있다.
쌓아 놓은 원판은 항상 위의 것이 아래의 것보다 작아야 한다.
이 작업을 수행하는데 필요한 이동 순서를 출력하는 프로그램을 작성하라. 단, 이동 횟수는 최소가 되어야 한다.

첫째 줄에 첫 번째 장대에 쌓인 원판의 개수 N (1 ≤ N ≤ 20)이 주어진다.
첫째 줄에 옮긴 횟수 K를 출력한다.

두 번째 줄부터 수행 과정을 출력한다. 두 번째 줄부터 K개의 줄에 걸쳐 두 정수 A B를 빈칸을 사이에 두고 출력하는데, 이는 A번째 탑의 가장 위에 있는 원판을 B번째 탑의 가장 위로 옮긴다는 뜻이다.
 

# 나의 코드

```java
public class Recursion11729 {
	
	// 원판의 움직임 출력 
	static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
	
	public static void move(int n, String from, String to) throws IOException {
		bw.write(from + " " + to + "\n");
	}
	public static void hanoi(int n, String from, String to, String via) throws IOException {
		if(n == 1) {
			move(n, from, to);
		} else {
			hanoi(n-1, from, via, to);  // n-1개를 먼저 1에서 2로 이동 
			move(n, from, to); 			// 가장 무거운걸 3으로 이동 
			hanoi(n-1, via, to, from);  // 2로 옮겨놨던 n-1개를 3으로 이
		}
	}
	
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		int n = Integer.parseInt(br.readLine());
		
		System.out.println((int)Math.pow(2, n)-1); // 원판을 움직이는 회수 
		hanoi(n, "1", "3", "2");
		bw.close();
		
	}
}
```



# 생각할 점

## 물리적으로 생각하지 말자.

왜 나는 '물리적으로' 원판을 직접 장대에 옮길 생각을 했을까?

하노이의 탑 뿐만아니라 모든 알고리즘 문제에서, 자꾸만 쓸데없는 자료구조를 동원해가며 시각적으로 나타내려하는건 나의 취약점이다.

처음에 난 정말 1, 2, 3 세 개의 장대를 배열이든 뭐든 시각적으로 만들어내려했고, 옮기는 히스토리조차 ArrayList에 모두 담아 한꺼번에 출력하려 했다.

'장대가 세 개가 있고, 원판이 움직이며, 움직인 히스토리를 보여야하는구나' 라고 문제를 보는 순간부터 난 이미 이 모든 개체들을 만들어내려고 하고있었다.

그러다가 도저히 안될 것 같아, 구글링을 하며 힌트를 얻고 코드를 짰다. 

원판이고 장대고 나발이고, 다 필요가 없었다. 규칙만 알면 끊임없이 호출하면 되었으며, 옮긴 히스토리는 내가 일일히 다 기록하려했던 생각 자체가 무색할만큼 너무나 간단하게 출력이 가능했다.

문제를 너무 단순하게만 접근해도 문제지만, 문제를 볼때마다 복잡하게 푸는것은 더 문제다. 



## 수식으로 세워보자.

원판을 움직이는 회수는 공식이 있었다.

이 공식은 결코 대단한 것이 아니며, 규칙을 먼저 찾아내었다면 반복된 예제를 그려보며 충분히 도출할 수 있는 식이었다.

무식하게 무조건 cnt 변수를 ++ 할 생각부터 하지 말고, 수식을 통한 일반화로 더 효율적으로 풀도록 노력하자. 