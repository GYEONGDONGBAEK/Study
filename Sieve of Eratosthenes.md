# [Algorithm] 에라토스테네스의 체

---

에라토스테네스의 체는 소수를 구하는 알고리즘으로 유명하다. 소수가 되는 수의 배수를 지우면 남은 건 소수가 된다는 알고리즘이다.

### 방법

1. 2부터 소수를 구하고자 하는 구간의 모든 수를 나열한다. 그림에서 회색 사각형으로 두른 수들이 여기에 해당한다.
2. 2는 소수이므로 오른쪽에 2를 쓴다. (빨간색)
3. 자기 자신을 제외한 2의 배수를 모두 지운다.
4. 남아있는 수 가운데 3은 소수이므로 오른쪽에 3을 쓴다. (초록색)
5. 자기 자신을 제외한 3의 배수를 모두 지운다.
6. 남아있는 수 가운데 5는 소수이므로 오른쪽에 5를 쓴다. (파란색)
7. 자기 자신을 제외한 5의 배수를 모두 지운다.
8. 남아있는 수 가운데 7은 소수이므로 오른쪽에 7을 쓴다. (노란색)
9. 자기 자신을 제외한 7의 배수를 모두 지운다.
10. 위의 과정을 반복하면 구하는 구간의 모든 소수가 남는다. (보라색)

![에라토스테네스의 체.gif](%5BAlgorithm%5D%20%E1%84%8B%E1%85%A6%E1%84%85%E1%85%A1%E1%84%90%E1%85%A9%E1%84%89%E1%85%B3%E1%84%90%E1%85%A6%E1%84%82%E1%85%A6%E1%84%89%E1%85%B3%E1%84%8B%E1%85%B4%20%E1%84%8E%E1%85%A6%20d764773d85544a1abb51fd2af7831003/%25EC%2597%2590%25EB%259D%25BC%25ED%2586%25A0%25EC%258A%25A4%25ED%2585%258C%25EB%2584%25A4%25EC%258A%25A4%25EC%259D%2598_%25EC%25B2%25B4.gif)

---

### Java로 구현

```java
public class Eratos {
	public static void main(String[] args) {
		// ArrayList로 구현
		ArrayList<Boolean> primeList;

		// 사용자로부터의 콘솔 입력
		Scanner scan = new Scanner(System.in);
		int n = scan.nextInt();

		// n <= 1 일 때 종료
		if(n <= 1) return;

		// n+1만큼 할당
		primeList = new ArrayList<Boolean>(n+1);
		// 0번째와 1번째를 소수 아님으로 처리
		primeList.add(false);
		primeList.add(false);
		// 2~ n까지 소수로 설정
		for(int i=2; i<=n; i++ )
			primeList.add(i, true);

		// 2부터  ~ i*i <= n
		// 각각의 배수들을 지워간다.
		for(int i=2; (i*i)<=n; i++){
			if(primeList.get(i)){
				for(int j = i*i; j<=n; j+=i) primeList.set(j, false);
				//i*i 미만은 이미 처리되었으므로 j의 시작값은 i*i로 최적화할 수 있다.
			}
		}
		StringBuffer sb = new StringBuffer();
		sb.append("{");
		for(int i=0; i<=n; i++){
			if(primeList.get(i) == true){
				sb.append(i);
				sb.append(",");
			}
		}
		sb.setCharAt(sb.length()-1, '}');

		System.out.println(sb.toString());

	}
}
```