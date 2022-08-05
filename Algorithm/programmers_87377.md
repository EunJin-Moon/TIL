#교점에 별 만들기

https://school.programmers.co.kr/learn/courses/30/lessons/87377


Level 2문제..

1) for 문을 돌면서 두 직선들의 교점을 구하고, 구한 교점들을 hashset에 넣어줍니다.
  1-1) (AD-BC)==0 이면, 두 직선은 평행

  1-2) 두 교점이 정수인지 아닌지 판별하여, 구한 교점 x, y가 모두 정수인 것만 HashSet<Point> 에 넣어줍니다.

  1-3) 구한 교점으로 x의 최댓값과, 최솟값, y의 최댓값과 최솟값을 구합니다.


2) 구한 maxx, maxy, minx, miny로 구한 교점들을 넣을 판의 height와 width를 구합니다.

3) answer= new String[height] 로 판을 만들어주고, 일단 점으로 채워줍니다.

4) set에 넣어뒀던 교점들을 순회하며 answer판에 "*" 별을 넣어줍니다.


```
import java.util.*;
public class programmers_교점에별만들기 {

	public static void main(String[] args) {
		
						
		System.out.println(Arrays.toString(solution(new int[][] {{2, -1, 4}, {-2, -1, 4}, {0, -1, 1}, {5, -8, -12}, {5, 8, 12}}	)));	
//		["....*....", ".........", ".........", "*.......*", ".........", ".........", ".........", ".........", "*.......*"]
		System.out.println(Arrays.toString(solution(new int[][] {{0, 1, -1}, {1, 0, -1}, {1, 0, 1}}	)));	
		//["*.*"]
		
		System.out.println(Arrays.toString(solution(new int[][] {{1, -1, 0}, {2, -1, 0}} )));	
		//["*"]
		
		System.out.println(Arrays.toString(solution(new int[][] {{1, -1, 0}, {2, -1, 0}, {4, -1, 0}})));	
//		["*"]
		
	}

	public static class Point{
	    long x;
	    long y;
	    public Point(long x, long y){
	        this.x = x;
	        this.y = y;
	    }
	}

	public static String[] solution(int[][] line) {
		String[] answer;

		long minX = Long.MAX_VALUE, maxX = Long.MIN_VALUE;
		long minY = Long.MAX_VALUE, maxY = Long.MIN_VALUE;

		// x = (bf-ed)/ad-bc
		// y = (ec-af)/ad-bc
		HashSet<Point> set = new HashSet<>();
		long x = 0, y = 0;
		for (int i = 0; i < line.length - 1; i++) {
			long a = line[i][0];
			long b = line[i][1];
			long e = line[i][2];
			for (int j = 0; j < line.length; j++) {
				long c = line[j][0];
				long d = line[j][1];
				long f = line[j][2];

				long adbc = a * d - b * c;
				if (adbc == 0)
					continue; // 비교대상 직선과 평행함

				long bfed = b * f - e * d;
				if (bfed % adbc != 0)
					continue; // x가 정수가 아님

				long ecaf = e * c - a * f;
				if (ecaf % adbc != 0)
					continue; // y가 정수가 아님

				x = bfed / adbc;
				y = ecaf / adbc;
				set.add(new Point(x, y));
				
				minX = Math.min(minX, x);
				minY = Math.min(minY, y);
				maxX = Math.max(maxX, x);
				maxY = Math.max(maxY, y);
			}
		}
//		System.out.println(minX+":"+minY+":"+maxX+":"+maxY);
		long height = maxY - minY + 1;
		long width = maxX - minX + 1;
		answer = new String[(int) height];
		StringBuilder sb = new StringBuilder();
		for (int i = 0; i < width; i++) {
			sb.append(".");
		}
		Arrays.fill(answer, sb.toString());
		long nx, ny;
		for (Point p : set) {
			nx = p.x - minX;
			ny = maxY - p.y;
//			System.out.println(p.x + ":" + p.y + " = "+nx + ":"+ny);
			answer[(int) ny] = answer[(int) ny].substring(0, (int) nx) + "*" + answer[(int) ny].substring((int) nx + 1);

		}

		return answer;
	}


}
```
