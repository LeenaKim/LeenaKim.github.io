---
the valayout: post
title: 백준 14889 : 스타트와 링크 (JAVA)
subtitle : 백트래킹
tags: [algorithm]
author: Leena Kim
comments : true
---



# 문제

오늘은 스타트링크에 다니는 사람들이 모여서 축구를 해보려고 한다. 축구는 평일 오후에 하고 의무 참석도 아니다. 축구를 하기 위해 모인 사람은 총 N명이고 신기하게도 N은 짝수이다. 이제 N/2명으로 이루어진 스타트 팀과 링크 팀으로 사람들을 나눠야 한다.

BOJ를 운영하는 회사 답게 사람에게 번호를 1부터 N까지로 배정했고, 아래와 같은 능력치를 조사했다. 능력치 Sij는 i번 사람과 j번 사람이 같은 팀에 속했을 때, 팀에 더해지는 능력치이다. 팀의 능력치는 팀에 속한 모든 쌍의 능력치 Sij의 합이다. Sij는 Sji와 다를 수도 있으며, i번 사람과 j번 사람이 같은 팀에 속했을 때, 팀에 더해지는 능력치는 Sij와 Sji이다.

N=4이고, S가 아래와 같은 경우를 살펴보자.

| i\j  | 1    | 2    | 3    | 4    |
| :--- | :--- | :--- | :--- | :--- |
| 1    |      | 1    | 2    | 3    |
| 2    | 4    |      | 5    | 6    |
| 3    | 7    | 1    |      | 2    |
| 4    | 3    | 4    | 5    |      |

예를 들어, 1, 2번이 스타트 팀, 3, 4번이 링크 팀에 속한 경우에 두 팀의 능력치는 아래와 같다.

- 스타트 팀: S12 + S21 = 1 + 4 = 5
- 링크 팀: S34 + S43 = 2 + 5 = 7

1, 3번이 스타트 팀, 2, 4번이 링크 팀에 속하면, 두 팀의 능력치는 아래와 같다.

- 스타트 팀: S13 + S31 = 2 + 7 = 9
- 링크 팀: S24 + S42 = 6 + 4 = 10

축구를 재미있게 하기 위해서 스타트 팀의 능력치와 링크 팀의 능력치의 차이를 최소로 하려고 한다. 위의 예제와 같은 경우에는 1, 4번이 스타트 팀, 2, 3번 팀이 링크 팀에 속하면 스타트 팀의 능력치는 6, 링크 팀의 능력치는 6이 되어서 차이가 0이 되고 이 값이 최소이다.

## 입력

첫째 줄에 N(4 ≤ N ≤ 20, N은 짝수)이 주어진다. 둘째 줄부터 N개의 줄에 S가 주어진다. 각 줄은 N개의 수로 이루어져 있고, i번 줄의 j번째 수는 Sij 이다. Sii는 항상 0이고, 나머지 Sij는 1보다 크거나 같고, 100보다 작거나 같은 정수이다.

## 출력

첫째 줄에 스타트 팀과 링크 팀의 능력치의 차이의 최솟값을 출력한다.

<br>

# 코드

이 문제는 지금까지 풀어온 백트래킹 문제들을 순차적으로 풀었으면 로직을 짜는건 어렵지 않다. 

하지만 관건은 시간을 어떻게 줄일것이냐였다.

![14889](/assets/img/post_img/algorithm/14889.png)

도대체 시간초과로 몇번이나 틀린건지... 

내 방법의 문제점을 진단하고 같은 실수를 반복하지 않기 위해 이 문제는 글로 남기려 한다.

<br>

## 처음 시도 

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;

public class Main {

	public static int N;
	public static int[][] S;
	public static int[] mem;
	public static int[] start;
	public static int[] linkArr;
	public static ArrayList<Integer> link = new ArrayList<>();
	public static int MIN = Integer.MAX_VALUE;
	
	// 자신을 제외한 다른 팀원간의 능력치 합을 구하는 함수 
	public static int getSum(int[] arr) {
		int sum = 0;
		for(int i = 0; i < arr.length; i++) {
			for(int j = 0; j < arr.length; j++) {
				if(i != j) {
					sum += S[arr[i]][arr[j]];
				}
			}
		}
		return sum;
	}
	public static void dfs(int depth) {
		// 두명씩 짝이 지어졌을때 
		// S[i][j] + S[j][i] 와 S[l][h] + S[h][l] 비교 
		if(depth == N/2) {
			link.removeAll(link);
			// start가 아닌 나머지는 link
			for(int i = 0; i < N; i++) {
				for(int j = 0; j < start.length; j++) {
					if(i == start[j]) break;
					if(i != start[j] && j == start.length - 1) {
						link.add(i);
					}
				}
			}
			// 두 팀의 능력치 합을 계산 
			
			int startSum = getSum(start);
			int size = 0;
			for(int temp : link) {
				linkArr[size++] = temp;
			}
			int linkSum = getSum(linkArr);
			MIN = Math.min(Math.abs(startSum - linkSum), MIN);
			return;
		}
		// 두 팀으로 어떻게 나눌것인가 
		for(int i = 0; i < N; i++) {
			// 아직 멤버로 발탁되지 않았으면 
			if(mem[i] >= 0) {
				// 해당 멤버를 풀에서 없앤다 
				mem[i]--;
				start[depth] = i; // 스타트가 아닌 나머지는 링크 
				dfs(depth + 1);
				
				// 재귀가 끝나면 다시 멤버를 복귀시킨다
				mem[i]++;
			}
		}
	}

	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		N = Integer.parseInt(br.readLine());
		S = new int[N][N];
		mem = new int[N];
		start = new int[N/2];
		linkArr = new int[N/2];
		String[] Sstr = new String[N];
		for(int i = 0; i < N; i++) {
			Sstr[i] = br.readLine();
		}
		for(int i = 0; i < N; i++) {
			String[] str = Sstr[i].split(" ");
			for(int j = 0; j < N; j++) {
				S[i][j] = Integer.parseInt(str[j]);
			}
		}
		
		dfs(0);
		System.out.println(MIN);
	}
}

```

<br>

**시간을 잡아먹는 포인트**

- 쓸데없는 변수들

  - start, link, linkArr : 문제에 팀을 두개로 쪼갠다고 나와있지만, 이를 반드시 구현할 필요는 없다. 이미 mem 변수로 값이 -1인 인덱스는 스타트팀, 0인 인덱스는 링크인데 이걸 굳이 새 변수에 담으로써 메모리와 시간을 그만큼 잡아먹는다. link의 경우는 스타트가 아닌 인덱스를 골라 담기위해서 선언했는데, linkArr 배열에 담을경우 인덱스값을 알아야하기때문에 그냥 인덱스에 구애받지 않고 바로 add 함수를 쓰기위해 선언했다. 이 또한 그냥 size++ 방법을 이용해 바로 배열에 담았으면 필요 없는 변수였다. 

  ```java
  start = new int[N/2];
  linkArr = new int[N/2];
  public static ArrayList<Integer> link = new ArrayList<>();
  ```

  

- Main 함수

  - 라인별로 입력을 받기위해 반복문을 N번만큼 더 탐. N이 20까지 들어올 수 있으니 최악의 경우 20번을 한번 더 도는 것. 어차피 밑에서 데이터별로 다시 2중반복문을 돌기 때문에 이 때 받으면 시간이 절약됨 .

  ```java
  String[] Sstr = new String[N];
  for(int i = 0; i < N; i++) {
    Sstr[i] = br.readLine();
  }
  ```

  - StringTokenizer을 활용하지 못함. split으로 하나씩 쪼개면 배열에 담기때문에 시간이 더 걸린다.

  ```java
  for(int i = 0; i < N; i++) {
    String[] str = Sstr[i].split(" ");
    for(int j = 0; j < N; j++) {
      S[i][j] = Integer.parseInt(str[j]);
    }
  }
  ```



- getSum 함수

  - 앞서 변수부터 선언을 비효율적으로 했으니 start가 아닌 인덱스를 발라내는 불필요한 작업이 들어갔다. 그나마 시간을 줄여보겠다고 자기 자신인 팀원은 반복문을 탈출하는 로직을 짰지만, 짜나 마나한 코드였다. 어차피 `S[i][i]` 는 0이기때문에 0을 더하게 두는게 가독성이 좋다. 

  ```java
  link.removeAll(link);
  // start가 아닌 나머지는 link
  for(int i = 0; i < N; i++) {
    for(int j = 0; j < start.length; j++) {
      if(i == start[j]) break;
      if(i != start[j] && j == start.length - 1) {
        link.add(i);
      }
    }
  }
  ```

  - 변수를 잘못 선언하여 ArrayList 를 배열로 변환하는 작업때문에 N번만큼 반복문을 또 돌게되었고, 스타트 팀과 링크 팀의 점수 합을 구하느라 getSum 함수를 두 번 호출하여 이중반복문을 두 번이나 타게 되었다. 

  ```java
  int startSum = getSum(start);
  int size = 0;
  for(int temp : link) {
    linkArr[size++] = temp;
  }
  int linkSum = getSum(linkArr);
  ```

  - 굳이 스타트와 링크팀을 배열로 나누느라 start[depth] = i 라는 불필요한 작업이 들어가게 되었다.

  ```java
  // 두 팀으로 어떻게 나눌것인가 
  for(int i = 0; i < N; i++) {
    // 아직 멤버로 발탁되지 않았으면 
    if(mem[i] >= 0) {
      // 해당 멤버를 풀에서 없앤다 
      mem[i]--;
      start[depth] = i; // 스타트가 아닌 나머지는 링크 
      dfs(depth + 1);
  
      // 재귀가 끝나면 다시 멤버를 복귀시킨다
      mem[i]++;
    }
  }
  ```



<br>

## 최종 코드

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.StringTokenizer;

public class Main {

	public static int N;
	public static int[][] S;
	public static boolean[] visited;
	public static int MIN = Integer.MAX_VALUE;
	
	// 자신을 제외한 다른 팀원간의 능력치 합을 구하는 함수 
	public static void diff() {
		// 두 팀의 능력치 합을 계산 
		int startSum = 0, linkSum = 0;
		for(int i = 0; i < visited.length; i++) {
			for(int j = 0; j < visited.length; j++) {
				if(!visited[i] && !visited[j]) {
					startSum += S[i][j];
				} else if(visited[i] && visited[j]) {
					linkSum += S[i][j];
				}
			}
		}
		int val = Math.abs(startSum - linkSum);
		// 두 팀의 점수차가 0이면 가장 낮은 최솟값이기때문에 바로 종료 
		if(val == 0) {
			System.out.println(val);
			System.exit(0);
		}
		MIN = Math.min(val, MIN);
					
	}
	// from : 팀 내에서는 1과 2가 스타트팀이나, 2와 1이 스타트임이나 상관없으므로 탐색 시간을 줄이기위해 이미 채택한 팀원은 제외하고 탐색 
	public static void dfs(int from, int depth) {
		// 두명씩 짝이 지어졌을때 
		// S[i][j] + S[j][i] 와 S[l][h] + S[h][l] 비교 
		if(depth == N/2) {
			diff();
			return;
		}
		// 두 팀으로 어떻게 나눌것인가 
		for(int i = from; i < N; i++) {
			// 아직 멤버로 발탁되지 않았으면 
			if(!visited[i]) {
				// 해당 멤버를 풀에서 없앤다 
				visited[i] = true;
				dfs(i + 1, depth + 1);
				
				// 재귀가 끝나면 다시 멤버를 복귀시킨다
				visited[i] = false;
			}
		}
	}

	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		N = Integer.parseInt(br.readLine());
		S = new int[N][N];
		visited = new boolean[N];

		for(int i = 0; i < N; i++) {
			StringTokenizer st = new StringTokenizer(br.readLine(), " ");
			for(int j = 0; j < N; j++) {
				S[i][j] = Integer.parseInt(st.nextToken());
			}
		}
		
		dfs(0, 0);
		System.out.println(MIN);
	}
}

```

위에서 언급한 모든 시간을 잡아먹는 부분을 하나씩 고쳐나가며 결국 이와 같은 최종 코드가 완성되었다. 그래도 시간초과의 장벽을 넘을 수 없어 최솟값이 바로 0으로 나왔을 때 바로 프로그램을 빠져나가는 로직까지 추가해야 통과하게 되었다.

로직을 짜는건 어렵지 않았으나, 내 문제는 항상 걸리는 시간을 잘 고려하지 못한다는 것이다. 눈에 보이는대로 구현하려하지 말고, 최적화된 로직으로 다듬는 법을 터득해야 한다. 