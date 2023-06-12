# 정렬 알고리즘(Sort)

---

# ****정렬 알고리즘 별 시간 복잡도****

| 정렬 알고리즘 | 시간 복잡도 |
| --- | --- |
| Bubble Sort (버블 정렬) | O(n^2) |
| Selection Sort (선택 정렬) | O(n^2) |
| Insertion Sort (삽입 정렬) | O(n^2) |
| Shell Sort(셸 정렬) | O(n^1.5) |
| Quick Sort (퀵 정렬) | 평균 : O(nlogn) / 최악 : O(n^2) |
| Merge Sort (병합 정렬) | O(nlogn) |

---

## 1. Bubble Sort(버블 정렬)

- 순서대로 근접한 두 수를 비교해서 오른쪽 수가 왼쪽 수보다 더 작으면 교환
- 이 작업을 한 번 수행 할때마다 맨 끝자리에 가장 큰 수가 가게 됨
- 이 작업을 최대 n - 1 번 반복하면 정렬 완료 -> 시간복잡도 : O(n^2)

```java
private static void bubble(int[] arr) {
		for(int i=0;i<arr.length; i++) {
	        for(int j=0;j<arr.length-i-1;j++) {
	            if(arr[j]>arr[j+1]) {
	                swap(arr,j,j+1);
	            }
	        }
	    }	
	}
	
	public static void swap(int[] arr, int m ,int n) {
		int temp=arr[m];
        arr[m]=arr[n];
        arr[n]=temp;
	}
```

---

## 2.Selection Sort(선택 정렬)

- 정렬할 리스트에서 최소값을 찾는다.
- 최소값을 맨 앞자리의 값과 교환
- 맨 앞자리 제외한 나머지 값들 중 최소값을 찾아 다음 자리값과 교환
- 이 작업을 최대 n - 1 번 반복하면 정렬 완료 -> 시간복잡도 : O(n^2)

```java
private static void selection(int[] arr) {
		for(int i=0;i<arr.length-1; i++) {
					int min=i;
	        for(int j=i+1;j<arr.length;j++) {
	            if(arr[j]<arr[i]) {
	                min = j;
	            }
	        }
				 swap(arr,min,i);
	    }	
	}
	
	public static void swap(int[] arr, int m ,int n) {
		int temp=arr[m];
        arr[m]=arr[n];
        arr[n]=temp;
	}
```

---

## 3.Insertion Sort (삽입 정렬)

- 타겟이 되는 데이터를 이전 위치에 있는 데이터와 비교 (첫 번째 타겟은 두 번째 데이터부터 시작)
- 만약 이전 위치에 있던 데이터보다 작다면 위치를 서로 교환
- 타겟에 대한 정렬이 끝나면 다시 타겟을 설정
- 이 작업을 최대 n - 1 번 반복하면 정렬 완료 -> 시간복잡도 : O(n^2)

     → 삽입될 위치를 찾을때 이진탐색으로 탐색하면 시간복잡도를 줄일 수 있음

```java
private static void insertion(int[] arr) {
    for(int i=1;i<arr.length;i++) {
			int tmp=arr[i];
			for(int j=i-1;j>=0;j--) {
				if(arr[j]>tmp) {
					arr[j+1]=arr[j];
				}else {
					break;
				}
			}
			arr[j+1]=tmp;
		}
```

---

## 4.Shell Sort(셸 정렬)

- 정렬할 배열의 요소를 그룹으로 나눠 각 그룹별로 삽입 정렬 수행
- 그 그룹을 합치면서 정렬을 반복하여 요소의 이동 횟수를 줄인다.
- 위의 과정을 그룹의 개수가 1이 될 때까지 반복한다.

```java
static void intervalSort(int[] arr) {
		// i : interval 4 2 1 순으로
		for(int i=arr.length/2;i>0;i/=2) {
			for(int k=1;k<arr.length;k++) {
				int j;
				int tmp=arr[k];//arr[4]
				for(j=k-1;j>=0;j-=i) {
					if(arr[j]>tmp) {
						arr[j+i]=arr[j];
					}else {
						break;
					}
				}
			}
		}
	}
```

단점 - 멀리 떨어진 요소를 교환하므로 안정적이지 않음

---

## 5.Quick Sort(퀵 정렬)

### 퀵 정렬 개념

- 하나의 리스트를 피벗을 기준으로 두 개의 비균등한 크기로 분할하고 분할된 부분 리스트를 정렬한 다음, 두 개의 정렬된 부분 리스트를 합하여 전체가 정렬된 리스트가 되게 하는 방법이다.
- 퀵 정렬은 3단계로 이루어져있다.
    
    1단계. 분할(Divide) : 입력 배열을 피벗을 기준으로 비균등하게 2개의 부분 배열(피벗을 중심으로 왼쪽 = 피벗보다 작은 요소들, 오른쪽 = 피벗보다 큰 요소들)로 분할한다.
    
    2단계. 정복(Conquer) : 부분 배열을 정렬한다. 부분 배열의 크기가 충분히 작지 않으면 순환 호출을 이용하여 다시 분할 정복 방법을 적용한다.
    
    3단계. 결합(Combine) : 정렬된 부분 배열들을 하나의 배열에 합병한다.
    
- 순환 호출이 한번 진행될 때마다 최소한 하나의 원소(피벗)는 최종적으로 위치가 정해지므로, 이 알고리즘은 반드시 끝난다는 것을 보장할 수 있다.

---

### 퀵 정렬 동작 원리

- 리스트 가운데서 하나의 원소를 고른다. 이렇게 고른 원소를 피벗 이라고 한다.
- 피벗 앞에는 피벗보다 값이 작은 모든 원소들이 오고, 피벗 뒤에는 피벗보다 값이 큰 모든 원소들이 오도록 피벗을 기준으로 리스트를 둘로 나눈다. 이렇게 리스트를 둘로 나누는 것을 분할이라고 한다. 분할을 마친 뒤에 피벗은 더 이상 움직이지 않는다.
- 분할된 두 개의 작은 리스트에 대해 재귀적으로 이 과정을 반복한다. 재귀는 리스트의 크기가 0이나 1이 될 때까지 반복된다.
- n개의 데이터를 정렬할 때, 최악의 경우에는 O(n^2)번의 비교를 수행하고, 평균적으로 O(n log n)번의 비교를 수행한다.

```java
static void quickSort(int[] arr,int left, int right) {
		int pl=left;
		int pr=right;
		int pivot=arr[(pl+pr)/2];
		printProcess(arr,pl,pr,pivot);
		do {
			while(arr[pl]<pivot) pl++;
			while(arr[pr]>pivot) pr--;
			if(pl<=pr) {
				swap(arr,pl++,pr--);
			}
			
		}while(pl<=pr);
		if(left<pr) quickSort(arr,left,pr); //재귀호출
		if(pl<right) quickSort(arr,pl,right);
	}

	private static void swap(int[] arr, int i, int j) {
		int tmp=arr[i];
		arr[i]=arr[j];
		arr[j]=tmp;
		
	}
```

### 퀵 정렬의 시간 단축 방법

- Quick Sort는 pivot이 어떻게 정해지느냐에 따라 시간복잡도가 달라짐
- n개의 pivot이 모두 가장 작은 수 혹은 가장 큰 수로 뽑혔을 때 가장 오랙 걸리고 이 때의 시간 복잡도가 O(n^2)
- 따라서 pivot을 정하는 방식이 중요할 수 있음
- 위에서 구현한 코드는 중앙의 pivot을 무작위로 정했었는데 이 방법이 아닌 처음, 중간, 끝 값 중 2번째로 큰 값으로 pivot을 정하는 방법, 3개의 구간을 나눠 중간값을 구하고 그 값의 중간값을 pivot을 정하는 방법 등이 있음

---

## 6.Merge Sort (병합 정렬)

- n개의 입력이 들어오면, n개의 그룹으로 나누고, 2개씩 그룹을 합치면서 동시에 정렬
- 1개의 그룹이 남을때 까지 반복하면 정렬 완료
- 시간복잡도 : O(nlogn)

```java
static void partition(int[] arr, int left, int right) {
		if(left==right) return; //분할 하다보면(2로 나누다보면) left==right순간이 생긴다
		int mid=(left+right)/2;
		partition(arr,left,mid); //전반부 분할
		partition(arr,mid+1,right); //후반부 분할
		merge(arr, left, right); //2개로 나눈 배열을 병합하는 메서드
		
	}

	static void merge(int[] arr, int left, int right) {
		int tmp[]=new int[arr.length]; //임시 저장소
		int index=0; //tmp 에서 사용할 인덱스
		int pc=(left+right)/2;
		int pl=left;
		int pr=pc+1;
		index=left;
		while(pl<=pc && pr<=right) {
			tmp[index++]=(arr[pl] < arr[pr])? arr[pl++]: arr[pr++];
		}
		//남은 배열이 있을 경우 tmp로 옮긴다.
		if(pl>pc) { //왼쪽 배열을 tmpp로 다 옮겼다면 오른쪽 배열 남은 요소를 tmp로 옮긴다
			for(int i=pr;i<=right;i++) {
				tmp[index++]=arr[i];
			}
		}else { //반대의 경우, 왼쪽에 배열 남은요소 옮기기
			for(int i=pl;i<=pc;i++) {
				tmp[index++]=arr[i];
			}
		}
		for(int i=left;i<=right;i++) {
			arr[i]=tmp[i];
		}
		
	}
```