# 힙 정렬이란?
> "힙(Heap)을 이용해 데이터를 정렬하면 어떨까?"

## 힙이란??

### 힙은 '부모의 값이 자식의 값보다 항상 크다'는 조건을 만족하는 *완전이진트리이다.

*완전이진트리 : 트리의 한 종류. 

- '**완전**'은 부모는 자식을 왼쪽부터 추가하는 모양을 유지한다는 뜻
- '**이진**'은 부모가 가질 수 있는 자식의 개수는 최대 2개라는 의미
- **트리는** 가지가 뻗어나가는 것처럼 데이터가 서로 연결되어 있다는 것.


- 최대 힙 : 부모 노드의 키 값이 자식 노드의 키 값보다 항상 크거나 같은 크기의 관계
- 최소 힙 : 부모 노드의 키 값이 자식 노드의 키 값보다 항상 작거나 같은 크기의 관계



## 힙 정렬 수행 방법

1. 정렬한 원소들을 입력하여 최대 힙을 구성
2. 힙에 대하여 삭제 연산을 수행하여 얻은 원소를 마지막 자리에 배치
3. 나머지 원소에 대해서 다시 최대 힙으로 재구성. 원소의 개수만큼 2~3을 반복 수행

## 수행 과정

- 정렬되지 않은 69, 10, 30, 2, 16, 8, 31, 22의 자료들을 힙 정렬 방법으로 정렬하기

[https://t1.daumcdn.net/cfile/tistory/1106654D4D6FB5C610](https://t1.daumcdn.net/cfile/tistory/1106654D4D6FB5C610)

1. 초기 상태 → 노드가 8개인 완전 이진 트리를 만들고 최대 힙으로 구성한다.

[https://t1.daumcdn.net/cfile/tistory/205FA64C4D6FB5DA51](https://t1.daumcdn.net/cfile/tistory/205FA64C4D6FB5DA51)

2. 힙에 삭제 연산을 수행하여 루트 노드의 원소 69를 구해서 배열의 마지막 자리에 저장하고 나머지 원소들에 대해서 최대 힙으로 재구성한다.

[https://t1.daumcdn.net/cfile/tistory/1579554D4D6FB6C128](https://t1.daumcdn.net/cfile/tistory/1579554D4D6FB6C128)

3. 힙에 삭제 연산을 수행하여 루트 노드의 원소 31을 구해서 배열의 비어있는 마지막 자리에 저장하고 나머지 원소들에 대해서 최대 힙으로 재구성한다... * 반복

[https://t1.daumcdn.net/cfile/tistory/143BEB504D6FB6732F](https://t1.daumcdn.net/cfile/tistory/143BEB504D6FB6732F)

[https://t1.daumcdn.net/cfile/tistory/1860F94F4D6FB66518](https://t1.daumcdn.net/cfile/tistory/1860F94F4D6FB66518)

4. 힙에 삭제 연산을 수행하여 루트 노드의 원소 2를 구해서 배열의 비어있는 마지막 자리에 저장하고 나머지 원소들에 대해서 최대 힙으로 재구성한다.

## 배열의 마지막부터 큰 값 대입하기

1. 변수 i의 값을 n - 1로 초기화한다
2. a[0]과 a[i]를 바꾼다.
3. a[0], a[1], ... , a[i - 1]을 힙으로 만든다.
4. i의 값을 1씩 줄여 0이 되면 끝이다. 그렇지 않으면 2로 돌아간다. 

## 부모와 자식의 인덱스 사이 관계식

1. 부모는 a[(i - 1) / 2]
2. 왼쪽 자식은 a[i * 2 + 1]
3. 오른쪽 자식은 a[i * 2+ 2]

# 시간복잡도는 O(n log n)

힙 정렬은 **선택 정렬**을 응용한 알고리즘. 

힙 정렬은 첫 요소를 꺼내는 것으로 가장 큰 값이 구해지므로 첫 요소를 꺼낸 다음 나머지 요소를 다시 힙으로 만들어야 그 다음에 꺼낼 첫 요소도 가장 큰 값을 유지한다. 따라서 가장 큰 요소를 선택할 때의 시간 복잡도는 한 번에 선택할 수 있어 O(1)로 줄어든다. 그 대신 힙 정렬에서 다시 힙으로 만드는 작업의 시간 복잡도는 O(log n)이다.(← 한 번 자식 노드로 내려갈 때마다 노드의 갯수가 2배씩 증가하기 때문에)

따라서, 힙 정렬은 힙으로 만드는 작업을 요소의 개수만큼 반복하므로 시간 복잡도는 O(n log n)이다. 

코드 예제)

```java
package sort.heap;

import java.util.Scanner;

public class HeapSort {

	public static void main(String[] args) {

		Scanner sc = new Scanner(System.in);
		
		System.out.println("힙 정렬");
		System.out.print("요솟수 : ");
		int nx = sc.nextInt(); // 요솟수
		int[] x = new int[nx];
		
		for(int i=0; i < nx; i++) {
			System.out.print("x["+i+"]: ");
			x[i] = sc.nextInt();
		}
		
		heapSort(x, nx); // 배열x를 힙 정렬 합니다
		
		System.out.println("오름차순으로 정렬했습니다");
		for (int i=0; i<nx; i++)
			System.out.println("x["+ i + "]="+ x[i]);
		
		sc.close();
	}

	// 요소가 n개인 배열 a를 힙 정렬하는 메소드
	private static void heapSort(int[] a, int n) {
		// 1. 배열을 힙으로 만들기
		for (int i=(n-1)/2; i >= 0; i--) //a[i]~a[n-1]를 힙으로 만들기 i는 루트
			downHeap(a, i, n-1);
			
		//2. 힙정렬 반복 수행
		for (int i= n-1; i > 0; i--) {
			swap(a, 0, i); // 가장 큰 요소(루트인 a[0])와 아직 정렬되지 않은 부분의 마지막 요소를 교환
			downHeap(a, 0, i-1);  // a[0] ~ a[i-1]을 힙으로 만듭니다
		}
	}

	// a[left] ~ a[right]를 힙으로 만듭니다 - a[left] 이외에는 모두 힙 상태라고 가정하고 a[left]를 아랫부분의 알맞은 위치로 옮겨 힙상태로 만든다
	private static void downHeap(int[] a, int left, int right) {
		int temp = a[left];	// 루트
		int child;			// 큰 값을 가진 노드
		int parent;			// 부모
		
		for (parent = left; parent < (right + 1) / 2; parent = child) {
			int cl = parent * 2 + 1;	// 왼쪽 자식
			int cr = cl + 1;			// 오른쪽 자식
			child = (cr <= right && a[cr] > a[cl]) ? cr : cl;	// 큰 값을 가진 노드를 자식에 대입
			if (temp >= a[child])
				break;
			a[parent] = a[child];
		}
		a[parent] = temp;
	}

	// 배열 요소 a[idx1]과 a[idx2]의 값을 바꿉니다
	private static void swap(int[] a, int idx1, int idx2) {
		int t = a[idx1];
		a[idx1] = a[idx2];
		a[idx2] = t;
		
	}

}
```

 출처1 ([https://zamzagi.tistory.com/entry/힙-정렬Heap-Sort](https://zamzagi.tistory.com/entry/%ED%9E%99-%EC%A0%95%EB%A0%ACHeap-Sort))   
 출처2 Do it! 자료구조와 함께 배우는 알고리즘 입문 자바편   
 출처3 나동빈님 블로그(https://blog.naver.com/ndb796/221228342808)
