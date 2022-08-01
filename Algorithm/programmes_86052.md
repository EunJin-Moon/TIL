# 프로그래머스 : 빛의 경로 사이클

https://school.programmers.co.kr/learn/courses/30/lessons/86052

1) 회전하는 방향으로 생각
    위->왼->아래->오른
2) 3차원 배열
  각 정점이 모든방향을 갔나 확인


```
import java.util.*;
class Solution {
    static int [][] dir = {{-1,0},{0,-1},{1,0},{0,1}};
	static boolean visited[][][];
	static int R,C;
    public int[] solution(String[] grid) {
	        ArrayList<Integer>list = new ArrayList<Integer>();
	        
	        R = grid.length;
	        C = grid[0].length();
	        visited = new boolean[R][C][4];
	        
	        for(int i = 0 ; i < R; i++) {
	        	for(int j = 0 ; j < C ; j++) {
	        		for(int d = 0 ; d < 4 ; d++) {
	        			if(!visited[i][j][d]) {
	        				list.add(solve(grid, i, j, d));
	        			}
	        		}
	        	}
	        }
	        
	        Collections.sort(list);
	        int[] answer = new int[list.size()];
	        for(int i = 0 ;i<list.size();i++) {
	        	int cnt = list.get(i);
	        	answer[i] = cnt;
	        }
	        
	        return answer;
	}
	private static int solve(String[]grid, int x, int y, int d) {
		int cnt = 0;
		
		while(true) {
			if(visited[x][y][d]) {
				break;
			}
			cnt++;
			visited[x][y][d] = true;
			
			if(grid[x].charAt(y) == 'L') {
				d = d == 0 ? 3 : d-1;
			}else if(grid[x].charAt(y) == 'R') {
				d = d == 3 ? 0 : d+1;
			}
			x = (x + dir[d][0] + R)%R;
			y = (y + dir[d][1] + C)%C;
			
		}
		
		return cnt;
		
	}
}

```
