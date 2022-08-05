
# 스타수열

https://school.programmers.co.kr/learn/courses/30/lessons/70130


1. array에 교집합으로 사용할 수 있을만한 key값을 찾기 위해 각 숫자가 호출된 횟수를 저장합니다.
keyset을 순회하면서 스타 수열의 최댓값을 찾습니다.

2. a[]를 돌면서 앞과 뒤에 교집합인 값이 있는지, 숫자가 같지는 않은지 확인하고 스타 수열 조건에 해당할 경우 스타수열의 길이인 star값을 2 올립니다.
start값과 answer를 비교해서 최대 값을 저장합니다.


3. answer를 반환합니다.



```
public class programmers_스타수열 {

	public static void main(String[] args) {
		
		System.out.println(solution(new int[] {0})); //0
		System.out.println(solution(new int[] {5,2,3,3,5,3})); // 4
		System.out.println(solution(new int[] {0,3,3,0,7,2,0,2,2,0})); // 8

	}

	public static int solution(int[] a) {
		int answer = 0;
		int[] count = new int[a.length + 1]; // a길이 미만의 수
		for (int i = 0; i < a.length; i++) {
			count[a[i]]++;
		}
		for (int i = 0; i < count.length; i++) {
			if (count[i] * 2 <= answer)
				continue;
			int star = 0;
			for (int j = 0; j < a.length - 1; j++) {
				if ((a[j] == i || a[j + 1] == i) && (a[j] != a[j + 1])) {
					star += 2;
					j++;
				}
			}
			answer = Math.max(answer, star); // 스타 수열 최대값 
		} 
		return answer; 
		
	}
}

```
