
# 이진변환반복하기

url : https://school.programmers.co.kr/learn/courses/30/lessons/70129


```
class Solution {
    public int[] solution(String s) {
        int[] answer = new int[2];
         
        int zero = 0;
        int cnt = 0;
        
        while(true){
            if("1".equals(s)){
                break;
            }
            String newStr = "";
            char[] splitStr = s.toCharArray();
            for(int i=0;i<splitStr.length;i++) {
            	if(splitStr[i] == '0') {
            		zero++;
            	}else {
            		newStr += splitStr[i]+"";
            	}
            	
            }
            s = Integer.toBinaryString(newStr.length());
            cnt++;
                
        }
        
        answer[0] = cnt;
        answer[1] = zero;
        
        
        return answer;
    }
}
```
