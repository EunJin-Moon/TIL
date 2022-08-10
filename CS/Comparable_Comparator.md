Comparable과 Comparator는 모두 인터페이스(interface)라는 것  


즉, Comparable 혹은 Comparator을 사용하고자 한다면 인터페이스 내에 선언된 메소드를 '반드시 구현'해야한다는 것



#  Interface Comparable

- 정의  
    - 정렬 수행 시 기본적으로 적용되는 정렬 기준이 되는 메서드를 정의하는 인터페이스
    - package: java.lang.Comparable
    - Java에서 제공되는 정렬이 가능한 클래스들은 모두 Comparable 인터페이스를 구현하고 있으며, 정렬 시에 이에 맞게 정렬이 수행

- 구현 방법
  - 정렬할 객체에 Comparable interface를 implements 후, compareTo() 메서드를 오버라이드하여 구현
  - compareTo() 메서드 작성법  
     - 현재 객체 < 파라미터로 넘어온 객체: 음수 리턴  
     - 현재 객체 == 파라미터로 넘어온 객체: 0 리턴  
     - 현재 객체 > 파라미터로 넘어온 객체: 양수 리턴  
     - 음수 또는 0이면 객체의 자리가 그대로 유지되며, 양수인 경우에는 두 객체의 자리가 바뀐다.  
      
- 사용 방법
    Arrays.sort(array)  
    Collections.sort(list)  
    참고 Arrays.sort()와 Collections.sort()의 차이

* Arrays.sort()
   - 배열 정렬의 경우  
    Ex) byte[], char[], double[], int[], Object[], T[] 등 * Object Array에서는 TimSort(Merge Sort + Insertion Sort)를 사용  
        Object Array: 새로 정의한 클래스에 대한 배열 * Primitive Array에서는 Dual Pivot QuickSort(Quick Sort + Insertion Sort)를 사용  
        Primitive Array: 기본 자료형에 대한 배열  
        
        
* Collections.sort() 
   - List Collection 정렬의 경우  
    Ex) ArrayList, LinkedList, Vector 등 * 내부적으로 Arrays.sort()를 사용
    
```
class Point implements Comparable<Point> {
    int x, y;

    @Override
    public int compareTo(Point p) {
        if(this.x > p.x) {
            return 1; // x에 대해서는 오름차순
        }
        else if(this.x == p.x) {
            if(this.y < p.y) { // y에 대해서는 내림차순
                return 1;
            }
        }
        return -1;
    }
}
```


# Interface Comparator

- 정의
  - 정렬 가능한 클래스(Comparable 인터페이스를 구현한 클래스)들의 기본 정렬 기준과 다르게 정렬 하고 싶을 때 사용하는 인터페이스
  - package: java.util.Comparator
      - 주로 익명 클래스로 사용
      - 본적인 정렬 방법인 오름차순 정렬을 내림차순으로 정렬할때 사용
 
 - 구현 방법
     - 정렬할 객체에 Comparable interface를 implements 후, compareTo() 메서드를 오버라이드하여 구현
     - compareTo() 메서드 작성법  
        - 현재 객체 < 파라미터로 넘어온 객체: 음수 리턴  
        - 현재 객체 == 파라미터로 넘어온 객체: 0 리턴  
        - 현재 객체 > 파라미터로 넘어온 객체: 양수 리턴  
        - 음수 또는 0이면 객체의 자리가 그대로 유지되며, 양수인 경우에는 두 객체의 자리가 바뀐다.  
- 사용 방법
    - Arrays.sort(array, myComparator)
    - Collections.sort(list, myComparator)
    - Arrays.sort(), Collections.sort() 메서드는 두 번째 인자로 Comparator interface를 받을 수 있다.




```
class MyComparator implements Comparator<Point> {
  @Override
  public int compare(Point p1, Point p2) {
    if (p1.x > p2.x) {
      return 1; // x에 대해서는 오름차순
    }
    else if (p1.x == p2.x) {
      if (p1.y < p2.y) { // y에 대해서는 내림차순
        return 1;
      }
    }
    return -1;
  }
}
```



* 익명 클래스

```
Comparator<Point> myComparator = new Comparator<Point>() {
  @Override
  public int compare(Point p1, Point p2) { 위와 동일 }
};
```
