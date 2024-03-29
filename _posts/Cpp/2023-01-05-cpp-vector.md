---
title:  "Vector"
excerpt: ""

categories:
  - cpp
tags:
  - [Cpp, C++]

toc: true
toc_sticky: true
 
date: 2023-01-05
last_modified_at: 2023-01-05
---

#### Vetor
---
<br>
<br>

##### vector의 사용  

- < vector > 헤더파일을 추가해야 한다.  
- vector의 선언은 `vector<[자료형]> [변수이름]` 이다.  

<br>
<br>

##### vector의 생성자와 연산자.    

- vector< int > a;  
	- 비어있는 vector a를 생성한다.    
	- int a[];  

- vector< int > a(5);  
	- 기본값이(0)으로 초기화 된 5개의 원소를 가지는 vector a를 생성한다.  
	- int a[5] = {0, 0, 0, 0, 0};  

- vector< int > a(5,2);  
	- 2로 초기화 된 5개의 원소를 가지는 vector a를 생성한다.    
	- int a[5] = {2, 2, 2, 2, 2};  

- vector< int > a1(5,2);  
vector< int > a2(a1);  
	- a2는 a1 vector를 복사해서 생성된다.  
	- int a2[5] = {2, 2, 2, 2, 2};

- vector< int > a1; , vector< int > a2; 가 있고, 내부에 인자들이 있다고 했을 때 연산자를 통해 대소 비교가 가능하다.  

<br>
<br>

##### vector의 멤버 함수.    

- a.assign(5,2);  
	- 2의 값으로 5개의 원소를 할당한다.  

- a.at(idx);  
	- idx번 째 원소를 참조한다.  
	- a[idx]보다 속도가 느리지만, 범위를 점검하므로 안전하다.  
    
- a[idx];  
	- idx번 째 원소를 참조한다.  
	- 범위를 점검하지 않으므로 속도가 a.at(idx)보다 빠르다.  
- a.front();  
	- 첫 번재 원소를 참조한다.  

- a.back();  
	- 마지막 원소를 참조한다.  

- a.clear();  
	- 모든 원소를 제거한다.  
	- **원소만 제거하고 메모리는 남아있다.**   
	- size만 줄어들고 capacity는 그대로 남아있다.  

- a.push_back(7);  
	- 마지막 원소 뒤에 원소 7을 삽입한다.  

- a.pop_back();  
	- 마지막 원소를 제거한다.  

- a.begin();  
	- 첫 번째 원소를 가리킨다. (iterator와 사용)  

- a.end();  
	- 마지막의 **다음**을 가리킨다. (iterator와 사용)  

- a.rbegin();  
	- reverse begin을 가리킨다.(배열 순서를 뒤집고, 첫 번째 원소를 가리킨다.)  
	- iterator와 사용  

- a.rend();  
	- reverse end를 가리킨다. (배열 순서를 뒤집고, 마지막의 다음을 가리킨다.
	- iterator와 사용  

- a.reserve(n);  
	- n개의 원소를 저장할 위치를 예약한다. (미리 동적할당 해놓는다.)  

- a.resize(n);  
	- 크기를 n으로 변경한다.  
	- 더 커졌을 경우 default 값인 0으로 초기화 한다.  

- a.resize(n, 3);  
	- 크기를 n으로 변경한다.  
	- 더 커졌을 경우 인자의 값을 3으로 초기화한다.  

- a.size();  
	- 원소의 개수를 리턴한다.  

- a.capacity();  
	- 할당된 공간의 크기를 리턴한다.  
	- 공간 할당의 기준은, 점점 커지면 capacity를 할당하게 된다.   

- a2.swap(a1);  
	- a1과 a2의 원소와 capacity를 바꿔준다. (모든걸 스왑한다)  
	- a1의 capacity를 없앨 때(할당한 메모리를 프로그램이 끝나기 전에 없애고 싶을 때) 사용하기도 한다.  
	- a2를 capacity가 0인 임시 객체로 만들어서 스왑해준다.  
	- vector< int >().swap(a1);  

- a.insert(2, 3, 4);  
	- 2번째 위치에 3개의 4값을 삽입한다. (다음 칸의 숫자들은 뒤로 밀린다)  

- a.erase(iter);  
	- iter 가 가리키는 원소를 제거한다.    
	- size만 줄어들고 capacity(할당된 메모리)는 그대로 남는다.  
	- erase는 파라미터 하나를 받을때와 두개를 받을 때가 다르다.  

- a.empty()  
	- vector가 비어있으면 return true  
	- 비어있다의 기준은 size가 0인 것. capacity와 관계 없다.  

<br>
<br>

##### vector의 size와 capacity의 관계  

![image](https://user-images.githubusercontent.com/106606698/198256654-4d4726ab-d005-4f2c-bfe8-7f665be2f45c.png)

- a.size();  
	- 원소의 개수를 리턴한다.  

- a.capacity();  
	- 할당된 공간의 크기를 리턴한다.  
	- 공간 할당의 기준은 점점 커지면 capacity를 할당하게 된다.  
	- string 클래스로 vector를 만들었을 때.

---  
원소 개수 1 → capacity 1  
원소 개수 2 → capacity 2  
원소 개수 3 → capacity 4  
원소 개수 4 → capacity 4  
원소 개수 5 → capacity 8  
원소 개수 6 → capacity 8  
원소 개수 7 → capacity 8  
원소 개수 8 → capacity 8
원소 개수 9 → capacity 16    

---

참고한 블로그의 예시 코드이다.[https://blockdmask.tistory.com/70]  

```c
#include <iostream>
#include <vector>

using namespace std;

int main(void)
{
	vector<int> a;

	cout << "< a[i], a.size(), a.capacity() >" << endl;
	for (int i = 0; i <= 64; i++)
	{
		a.push_back(i + 1);
		cout << "< " << a[i] << ", " << a.size() << ", " << a.capacity() << " >" << endl;
	};

	return 0;	
}
```

```
Output

< a[i], a.size(), a.capacity() >
< 1, 1, 1 >
< 2, 2, 2 >
< 3, 3, 3 >
< 4, 4, 4 >
< 5, 5, 6 >
< 6, 6, 6 >
< 7, 7, 9 >
< 8, 8, 9 >
< 9, 9, 9 >
< 10, 10, 13 >
< 11, 11, 13 >
< 12, 12, 13 >
< 13, 13, 13 >
< 14, 14, 19 >
< 15, 15, 19 >
< 16, 16, 19 >
< 17, 17, 19 >
< 18, 18, 19 >
< 19, 19, 19 >
< 20, 20, 28 >
< 21, 21, 28 >
< 22, 22, 28 >
< 23, 23, 28 >
< 24, 24, 28 >
< 25, 25, 28 >
< 26, 26, 28 >
< 27, 27, 28 >
< 28, 28, 28 >
< 29, 29, 42 >
< 30, 30, 42 >
< 31, 31, 42 >
< 32, 32, 42 >
< 33, 33, 42 >
< 34, 34, 42 >
< 35, 35, 42 >
< 36, 36, 42 >
< 37, 37, 42 >
< 38, 38, 42 >
< 39, 39, 42 >
< 40, 40, 42 >
< 41, 41, 42 >
< 42, 42, 42 >
< 43, 43, 63 >
< 44, 44, 63 >
< 45, 45, 63 >
< 46, 46, 63 >
< 47, 47, 63 >
< 48, 48, 63 >
< 49, 49, 63 >
< 50, 50, 63 >
< 51, 51, 63 >
< 52, 52, 63 >
< 53, 53, 63 >
< 54, 54, 63 >
< 55, 55, 63 >
< 56, 56, 63 >
< 57, 57, 63 >
< 58, 58, 63 >
< 59, 59, 63 >
< 60, 60, 63 >
< 61, 61, 63 >
< 62, 62, 63 >
< 63, 63, 63 >
< 64, 64, 94 >
< 65, 65, 94 >
```  

- **기존 메모리의 *2 로 증가하게 된다.**   
- 이런 식으로 메모리 할당을 하는 이유는 **puch_back**이 일어날 때마다 동적할당을 하면 비효율적이다. 때문에 미리 정해둔 만큼 동적할당을 한 번에 하는 것!  
- 원소의 개수가 증가하면서, 메모리를 증가해서 따로 할당하게 되면 기존위치에 메모리를 이어서 할당하는 게 아니라 새롭게 메모리를 할당해 원소들을 전부 복사하는 형태이다. 때문에 기존에는 복사에 대한 비용이 많이 들었으나 현재는 복사가 아닌 이동의 형태라서 메모리 증가에 대한 비용이 늘지 않았다.  
 
size는 할당된 메모리 안에 요소가 들어있는 것의 개수.  
capacity는 vector의 요소(element)들을 담을 수 있는 메모리가 할당되어있는 공간의 용량이다.  
size는 실제 유효한 요소(element)들의 개수이다.  
 
새로운 원소를 추가할 때(push_back), capacity가 size보다 크다면 새로운 원소를 추가하거나 지울 수 있다.  
capacity가 size와 크기가 같다면 capacity가 증가한 새로운 연속된 공간을 할당하고 기존의 모든 요소들을 복사한다.(기존 정보는 지움!) 즉 capacity > size인 상황을 만들고 맨 뒤에 요소를 복사해 놓고, ++size 하는 과정이 일어나는 것이다.  

<br>
<br>

##### reseve와 resize의 차이점  

reserve는 capacity를 프로그래머가 원하는 크기로 할당해준다.  
**~~추후 추가작성~~**  

resize는 지정한 수 만큼 요소를 만들어준다. capacity가 작으면 재할당이 일어난다.  
여기서 주의할 점은 증가되는 size만큼 복사생성자가 호출된다는 점이다.(**C++11, 최근 버전에는 생성자가 호출!**)  

<br>
<br>

##### vector의 멤버 형식  

- iterator : 반복자 형식  
 
- reverse_iterator : 역 반복자 형식  
 
- value_type : 원소의 형식  
 
- size_type : 원소 개수의 형식  

<br>
<br>

##### algorithm 헤더

>replace 함수  

벡터의 값을 변경할 때 사용했던 함수이다.  

```cpp
//		벡터의 시작,   벡터의 끝,  10의 값을 모두 90으로 변경
replace(temp.begin(), temp.end(), 10, 90);
```

구간을 지정하고 배열을 돌아 값을 찿고, 해당 값을 모두 설정한 값으로 변경해준다.  
시간복잡도가 큰 것 같다,,  

>정렬 함수  

- 오름차순  
`sort(score.begin(), score.end());`  
 
- 내림차순(r을 붙인다)   
`sort(score.rbegin(), score.rend());`  

<br>
<br>

##### 예제  

```cpp
#include <iostream>
#include <vector>

using namespace std;

int main(void)
{
	//기본값이 1로 초기화 된 5개의 원소를 가지는 vector a
	vector<int> a(5, 1); 

	cout << "<벡터 선언>" << endl;
	for (int i = 0; i < a.size(); i++)
	{
		cout << a[i] << " ";
	}
	cout << endl;

	a.assign(5, 2);

	cout << "a 벡터에 <assign()>" << endl;
	for (int i = 0; i < a.size(); i++)
	{
		cout << a[i] << " ";
	}

	cout << endl;
	cout << endl;

	//vector b에 1~10 차례대로 push_back하기
	vector<int> b;
	for (int i = 0; i < 10; i++)
	{
		b.push_back(i);
	}
	cout << "vector<int> b에 <push_baack>" << endl;
	for (int i = 0; i < b.size(); i++)
	{
		cout << b[i] << " ";
	};
	cout << endl;
	cout << endl;

	cout << "<b.at(1)>" << endl;
	cout << b.at(1) << endl;
	cout << "<b[1]>" << endl;
	cout << b[1] << endl;
	cout << "<b.front()>" << endl;
	cout << b.front() << endl;
	cout << "<b.back()>" << endl;
	cout << b.back() << endl;
	cout << "<b.pop_back()>" << endl;
	b.pop_back();
	for (int i = 0; i < b.size(); i++)
	{
		cout << b[i] << " ";
	};
	cout << endl;
	cout << endl;


	cout << "<a.swap(b)> a와 b 스왑" << endl;
	a.swap(b);
	cout << "b : ";
	for (int i = 0; i < b.size(); i++)
	{
		cout << b[i] << " ";
	};
	cout << endl;
	cout << "a : ";
	for (int i = 0; i < a.size(); i++)
	{
		cout << a[i] << " ";
	};
	cout << endl;
	cout << endl;
	
	cout << "b의 size : " << b.size() << ", b의 capacity : " << b.capacity() << endl;
	cout << "b.clear" << endl;
	b.clear();
	cout << "b의 size : " << b.size() << ", b의 capacity : " << b.capacity() << endl;

	return 0;
}
```

```
Output

<벡터 선언>
1 1 1 1 1
a 벡터에 <assign()>
2 2 2 2 2

vector<int> b에 <push_baack>
0 1 2 3 4 5 6 7 8 9

<b.at(1)>
1
<b[1]>
1
<b.front()>
0
<b.back()>
9
<b.pop_back()>
0 1 2 3 4 5 6 7 8

<a.swap(b)> a와 b 스왑
b : 2 2 2 2 2
a : 0 1 2 3 4 5 6 7 8

b의 size : 5, b의 capacity : 5
b.clear
b의 size : 0, b의 capacity : 5
```

<br>
<br>

##### 반복자 Iterator  

[출처 : https://dnf-lover.tistory.com/entry/c-%EB%AC%B8%EB%B2%95-%EB%B0%98%EB%B3%B5%EC%9E%90-IteratorVector%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%98%EC%97%AC-%EC%98%88%EC%A0%9C]

1. 선언  

`vector<int>::iterator iter;`  

2. 초기화  

`iter = v.begin();  //vector 반복자 iter는 v의 시작점`  

3. 예시  

```cpp
#include <iostream>
#include <vector>

using namespace std;

int main(void)
{
	vector<int> v;

	for (int i = 0; i < 7; i++) {
		v.push_back(10 * i);
	}

	vector<int>::iterator iter;
	// vector 반복자 iter는 v의 시작점을 가리킴
	iter = v.begin();

	cout << &iter << endl;
	cout << *iter << endl;
	// 임의 접근
	cout << iter[1] << endl;

	iter += 2; // += 연산 사용
	cout << &iter << endl;
	cout << *iter << endl;

	// 반복
	for (iter = v.begin(); iter != v.end(); iter++) {
		cout << *iter << endl;
	}


	return 0;
}
```

```
Output

004FFE24
0
10
004FFE24
20
0
10
20
30
40
50
60
```