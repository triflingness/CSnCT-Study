## 순환(recursion) 
  - 어떤 알고리즘이나 함수가 자기 자신을 호출하여 문제를 해결하는 프러그래밍 기법
  -> 하노이탑, 거듭제곱, 팩토리얼, 피보나치 수열

 ### 반복 :  for, while 등 반복 구조를 사용하여 반복시키는 문장(일정 횟수 동안 반복, 조건 만족까지 반복
```c
int factorial(int n) {
	if(n<=1) return(1);
	else return (n*factorial(n-1));
}
 ```
### 순환 : 자신을 다 호출하여 작업 수행
```c
int factorial_iter(int n)
{
	int k, v=1;
	for(k=n; k>0;k11)
		v=v*k;
	return(v);
}
```
### 분할 정복 : 작은 동일한 문제들을 분해하여 해결하는 방법 

### 순환의 개념을 사용하면 유리한 경우 
  -팩토리얼 함수 계산, 피보나치 수열, 이항 계수 계산, 각종 이진 트리 알고리즘, 이진 탐색, 하노이탑 문제
  
#### <반복 거듭제곱> 
```c
double slow_power(double x, int n) {
	int i;
	double r =1.0;
	for(i=0; i<n; i++)
		r = r*x;
	return(r);
}
```
#### <순환 거듭제곱>
```c
double power(double x, int n)
{
	if(n==0) return 1;
	else if ((n%2)==0)
	return power(x*x, n/2)
	else return x*power(x*x, (n-1)/2);
}
```

### 순환 알고리즘의 시간 복잡도: O(n)
  - 쉽지만 수행 시간과 기억 공간의 사용에 있어서는 비요율 적인 경우가 많다.
