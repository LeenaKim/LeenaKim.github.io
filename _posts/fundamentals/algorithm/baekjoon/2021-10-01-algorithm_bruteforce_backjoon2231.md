---
the valayout: post
title: 백준 2231 분해합 (JAVA)
subtitle : Brute Force 
tags: [algorithm]
author: Leena Kim
comments : true
---



# 문제

어떤 자연수 N이 있을 때, 그 자연수 N의 분해합은 N과 N을 이루는 각 자리수의 합을 의미한다. 어떤 자연수 M의 분해합이 N인 경우, M을 N의 생성자라 한다. 예를 들어, 245의 분해합은 256(=245+2+4+5)이 된다. 따라서 245는 256의 생성자가 된다. 물론, 어떤 자연수의 경우에는 생성자가 없을 수도 있다. 반대로, 생성자가 여러 개인 자연수도 있을 수 있다.

자연수 N이 주어졌을 때, N의 가장 작은 생성자를 구해내는 프로그램을 작성하시오.

첫째 줄에 자연수 N(1 ≤ N ≤ 1,000,000)이 주어진다.

첫째 줄에 답을 출력한다. 생성자가 없는 경우에는 0을 출력한다.

<br>

# 코드

```java
public class BruteForce2231 {
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		
		String nStr = br.readLine();
		int n = Integer.parseInt(nStr);
		int result = 0;
		
		for(int i = (n - (nStr.length() * 9)); i < n; i++) {
			int m = 0;
			m += i;
			for(int j = 0; j < Integer.toString(i).length(); j++) {
				m += Character.getNumericValue(Integer.toString(i).charAt(j));
			}
			System.out.println("bruteNumStr : " + Integer.toString(i));
			System.out.println("m : " + m);
			 
			if(m == n) {
				result = i;
				break;
			}
		}
		
		System.out.println(result);
		
	}
}

```

<br>

# 생각할 점

## 무식한걸 더 무식하게

그나마 brute force는 정답이 나올때까지 무식하게 푸는 방법이라, 풀기 쉬웠다.

하지만 이 무식한 방법마저 나는 더 무식하게 풀곤 한다.

수학을 이용해 10씩 나눈 나머지를 자릿수로 표현하면 식이 훨씬 간단해지는데, String을 이용하면 자릿수 문제를 해결할 수 있을것이라는 생각이 먼저 떠올라 코드 안에서 여러번 형변환을 했다. 

두 번째 어이없는 건, 문제에서 굳이 '최소값'을 찾으랬다고 어차피 작은수부터 for문을 돌리며 찾는데 굳이 min 변수를 세워놓고, 모든 가능한 생성자를 찾고 그중에 최소값을 찾으려 했다는 점이다.

어차피 작은 수부터 돌아가기 때문에, 첫 번째로 찾는 생성자가 곧 최소값인데.

처음 내 코드는, min 변수를 N의 최대값인 1000000으로 놓고, 생성자를 찾을때마다 min과 비교하여 작으면 min 변수를 재선언하는것이었다.

답을 출력할때도, min 변수가 초기값인 10000000으로 그대로 남아있다면 생성자가 없다는 뜻이므로 0을 출력하고, 그 외엔 min 변수를 그대로 출력하는 방식을 택했다.

그런데, 어차피 result의 초기값을 0으로 설정하고, 생성자가 있으면 result에 대입하는데, 생성자가 없으면 당연히 0이 아니겠는가?

대체 왜 자꾸 불필요한 프로세스를 굳이 굳이 추가하려 드는지. 



## 수식은 언제쯤 활용할지

N의 생성자가 될 수 있는 범위가 N - (N.length * 9) 에서 N 까지라는건 분명 설계를 할때부터 생각하고 있었다.

하지만 막상 코드를 짜면서 이를 코드에 녹여낼 수가 없었다.

처음 내 코드는 결국 while 무한루프를 돌다가 생성자를 찾아내면 break로 빠져나오는 식이었고,

입력으로 들어오는 N이 1000000 까지 올 수 있기때문에 무한루프를 돌리면 시간제한 2초를 당연히 넘어가버렸다.

brute force가 아무리 무식하게 모든 경우의 수를 시도해보는 방법이라 해도, 최소한의 수식을 활용한다면 훨씬 더 효율적으로 풀 수 있다는 점 명심하자. 