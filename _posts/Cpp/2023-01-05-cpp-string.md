---
title:  "string 클래스, 문자열 정리"
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

#### String (문자열)
---
<br>
<br>

Vector는 아직 공부하지 않았으므로 일반 Main함수에 구현한다🥲

##### Stringstream  

Stringstream은 문자열을 나누는 역할을 한다. 주어진 문자열에서 필요한 자료형에 맞는 정보를 꺼낼 때 사용한다.  
`공백`과, `\n`을 제외하고 문자열에 맞는 자료형의 정보를 빼낸다.  

+ #include < sstream > 전처리 헤더를 필수로 포함해야 한다.  
+ stream.str(string str) 은 현재 stream의 값을 문자열 str로 바꾼다.  

```cpp
#include <iostream>
#include <sstream>
#include <string>
using namespace std;

int main(void) {

	string str1 = "1D2S#10S";
	string str2 = "1111DAWV2S#10S";
	stringstream ss1(str1);
	stringstream ss2(str2);
	int num1, num2;

	while (ss1 >> num1) cout << num1 << endl;
	while (ss2 >> num2) cout << num2 << endl;
}
```

```cpp
output

1
1111
```

Stringstream은 num, 즉 정수형을 출력하고 있기 때문에 문자인 D를 만나는 순간 멈추게 된다.  

때문에 str2를 `"11 a11 DAWV 2 S# 10S";` 로 입력하게 되면 11을 출력하고 공백을 만나 개행을 하게 되지만 문자 a를 만나게 되어 더이상 정수를 출력하지 않는다.     

Stringstream은 정수 혹은 문자등을 분류한다고 생각면 쉽다.  

```cpp
int main(void) {

	string str1 = "1D2S#10S";
	string str2 = "1111DAWV2S#10S";
	stringstream ss1(str1);
	stringstream ss2(str2);
	char ch1, ch2;

	while (ss1 >> ch1) cout << ch1 << " ";
	while (ss2 >> ch2) cout << ch2 << " ";
}
```

```
output

1 D 2 S # 1 0 S 1 1 1 1 D A W V 2 S # 1 0 S
```

이번에는 str1, str2에 들어있는 모든 것들이 출력되었다. 처음 int형으로 받게 되면 숫자를 받아오지만 string은 char 형으로 이루어져 있기 때문에 모든 문자를 받아 올 수 있는것이다.  

```cpp
int main(void) {

	string str1 = "1D2S#10S";
	stringstream ss1(str1);

	cout << ss1.get() << " ";
	cout << ss1.get() << " ";
	cout << ss1.get() << " ";
	cout << ss1.get() << " ";
	cout << ss1.get() << " ";
	ss1.unget();
	cout << ss1.get() << " ";
	return 0;
}
```

```
output

49 68 50 83 35 35
```

- get() : 커서를 하나씩 옮기면서 값을 반환한다.  

- unget() : 커서를 앞으로 다시 옮긴다.  

값은 아스키 코드로 출력이 되었는데 마지막에 unget()을 사용하고 다시 get()으로 받아온 값을 출력해보면 그 전과 값이 같은 것을 확인할 수 있다.  

<br>
<br>

---

##### GetLine  

**cin 객체**  

![image](https://user-images.githubusercontent.com/106606698/197340890-fa419ab6-af14-44cf-99c7-fe9df106c4fd.png)
(https://velog.io/@jxlhe46/C-getline-%ED%95%A8%EC%88%98)  

+ < iostream > 헤더파일에 포함된 입력 스트림 객체이다.  
+ 공백, 탭, 엔터같은 화이트 스페이스 문자<sup>[1](#footnote_1)</sup>를 무시하고 입력 받지만, 이 문자들은 버퍼에 그대로 남아있다.  

```cpp
#include <iostream>
using namespace std;

int main() {

	int n;
	cin >> n;
	cout << n << '\n';

	string str;
	cin >> str;
	cout << str << '\n';

	return 0;
}
```

```
입력: 1
출력: 1
입력: Hello World!
출력: Hello
```

실행결과에서 알 수 있듯이 cin은 공백 이전까지만 입력을 받기 때문에 공백을 포함해서 입력을 받을 수 없다.  
이를 해결하기 위해 getline함수를 사용할 수 있다.  

**getline 함수**  

getline 함수는 `istream`에 속한 cin.getline 함수와 `string`에 속한 getline 함수 두 가지가 있다.  

>istream 라이브러리의 cin.getline()  

- 문자 배열이며 마지막 글자가 ‘\0’(terminator)인 c-string을 입력 받는데 사용한다.    
- n-1개의 문자 개수만큼 읽어와 str에 저장한다. (n번째 문자는 NULL(‘\0’)로 바꾼다.)  
- 세 번째 인자인 delim은 별도로 지정해주지 않으면 엔터(‘\n’)로 인식한다.  
- delim을 지정해주면 그 제한자(delim)문자 직전까지 읽어서 str에 저장한다.  

```cpp
cin.getline(char* str, streamsize n);
cin.getline(char* str, streamsize n, char dlim);
```

```cpp
#include <iostream>

using namespace std;

int main() {

	char a[100];

	cin.getline(a, 100);

	cout << a;

	return 0;
}
```

```
입력 : Hello World
출력 : Hello World
```

getline에서 제한자를 지정하지 않았기 때문에 Enter직전의 문자까지를 출력해준다.  

```cpp
#include <iostream>

using namespace std;

int main() {

	char a[100];

	cin.getline(a, 100, '@');

	cout << a;

	return 0;
}
```

```
입력 : Hello World ~~!! @Wellcome
출력 : Hello World ~~!!
```

@를 제한자로 설정했기 때문에 @ 직전의 문자까지 출력한다.  

>string 라이브러리의 getline()  

- 최대 문자 수를 입력하지 않아도 된다.  
- 원하는 구분자(delimiter)를 만날 때 까지 모든 문자열을 입력 받아 하나의 string 객체에 저장한다.  

```cpp
#include <iostream>
#include <string>

using namespace std; //필수! 없으면 string 선언 안됐다고 됨

int main()
{
   string str;
    
   getline(cin,str); // 표준입력방식으로 str에 문자열 끝까지 저장
}
```

```
입력 : Hello World
출력 : Hello World
```

```cpp
#include <iostream>
#include <string>

using namespace std; //필수! 없으면 string 선언 안됐다고 됨

int main()
{
   string str;
    
   getline(cin,str,'@'); // 표준입력방식으로 str에 's'까지 저장
}
```

```
입력 : Hello World \n sdfjk @sdkfjdkl
출력 : Hello World \n sdfjk 
```

개행을 하더라도 @ 직전의 문자까지 저장해서 출력해준다.  

**주의 점**  

```cpp
#include <iostream>
#include <string>

using namespace std;

int main()
{
    int n;
    string str;
    cin >> n;
    getline(cin, str);
    cout << str;
}
```  

아래는 위의 코드를 실행했을 시의 사진이다.  

![image](https://user-images.githubusercontent.com/106606698/197345779-2bc78907-5ef2-4e4e-a786-25b87335d850.png)  

위 코드처럼 입력을 하면 n을 입력받고 str을 입력받지 않은 뒤 바로 다음 코드로 넘어가게 된다. 
그 이유는 버퍼에 정수 값을 입력한 뒤 누른 엔터(\n)가 그대로 남아있어 getline에 들어가기 때문이다.  
이때, cin.ignore() 라는 함수를 사용하면 해결할 수 있다.  

```cpp
#include <iostream>
#include <string>

using namespace std;

int main()
{
    int n;
    string str;
    cin >> n;
	cin.ignore();
    getline(cin, str);
    cout << str;
}
```  

![image](https://user-images.githubusercontent.com/106606698/197345984-e55f83b8-d268-403d-b6e2-aa0f7d87a4ba.png)  

cin.ignore()가 입력 버퍼의 모든 내용을 제거해주기 때문에 getline()이 정상적으로 동작할 수 있다.  

>cin.get()  
 
- 표준 입력 버퍼에서 문자를 하나만 가져온다.  
- 문자 하나만 입력이 가능하며 공백과 개행도 입력으로 포함한다.  

```cpp
#include <iostream>

using namespace std;

int main()
{
    char ch1, ch2;
    ch1 = cin.get();
    ch2 = cin.get();
    cout << ch1 << "  " <<ch2 << endl;

    return 0;
}
```

![image](https://user-images.githubusercontent.com/106606698/197346301-6cf92e31-04e5-4eeb-ab42-5104f7c1bda2.png)

![image](https://user-images.githubusercontent.com/106606698/197346310-3e37051d-9db3-42c4-9d8f-7d1e2cdc6e3d.png)

a b를 입력했을 때 a만 출력된 것은 공백도 입력으로 간주하기 때문이다.  

<br>
<br>

---

##### Find, Substr  

find 함수는 찾고있는 문자의 자릿수를 반환해준다.  

```cpp
int main() {
	string s = "This is a string";
	string n;
	
	cout << s.find("s");

	return 0;
}
```

```
output

3
```

```cpp
#include <iostream>

using namespace std;

int main()
{
    string str = "abcSefghijklmnopqrStuvwxyz";

    cout << str.find('s', 1);

    return 0;
}
```

```
output

3
```

`cout << str.find('s', 17);` >> putput : 18


```
size_type find(const basic_string& str, size_type pos = 0) const;      // (1)
size_type find(const CharT* s, size_type pos, size_type count) const;  // (2)
size_type find(const CharT* s, size_type pos = 0) const;               // (3)
size_type find(CharT ch, size_type pos = 0) const;                     // (4)
template <class T>
size_type find(const T& t, size_type pos = 0) const;  // (5)
```

탐색은 pos 부터 시작한다.

1. 문자열에서 str 의 위치를 리턴한다.  

2. s 가 가리키는 문자 부터 count 개 만큼을 취한 부분 문자열을 원 문자열에서 찾는다. 참고로 s 에 중간에 NULL 이 있어도 괜찮다.  

3. s 가 가리키는 문자열을 원 문자열에서 검색한다. 이 때 s 는 널 종료 문자열로 간주된다.  

4. 원 문자열에서 문자 ch 의 위치를 찾는다.  

5. t 를 string_view 객체인 sv 로 변환한 뒤에(std::basic_string_view< CharT, Traits > sv = t;), sv 를 원 문자열에서 찾는다. 이 때 T 는 string_view 로 변환 가능한 타입이어야 한다.  

> 인자들  

- str - 찾고자 하는 문자열  

- pos - 검색을 시작할 위치  

- count - 찾고자 하는 문자열의 길이  

- s - 찾고자 하는 문자열을 가리키는 포인터  

- ch - 찾고자 하는 문자  

- t - 찾고자 하는 string_view 로 변환 가능한 객체  

```cpp
#include <iostream>
#include <string>

void print(std::string::size_type n, std::string const &s) {
  if (n == std::string::npos) {
    std::cout << "not found\n";
  } else {
    std::cout << "found: " << s.substr(n) << '\n';
  }
}

int main() {
  std::string::size_type n;
  std::string const s = "This is a string";

  // s 의 처음 부터 찾는다.
  n = s.find("is");
  print(n, s);

  // s 의 5번째 문자부터 찾는다.
  n = s.find("is", 5);
  print(n, s);

  // 단일 문자 (a) 를 찾는다.
  n = s.find('a');
  print(n, s);

  // 단일 문자 (q) 를 찾는다.
  n = s.find('q');
  print(n, s);
}
```

```
output

found: is is a string
found: is a string
found: a string
not found
```

> 참고자료    

- strstr : 문자열에서 원하는 부분 문자열을 리턴한다.  

- strchr : 문자열에서 특정 문자의 위치를 찾는다.  

- rfind : 문자열에서 특정 문자열이 마지막으로 나타나는 위치를 찾는다.  

- find_first_of : 주어진 문자들 중 가장 먼저 나타나는 문자의 위치를 찾는다.  

- find_first_not_of : 주어진 문자가 아닌 문자가 가장 먼저 나타나는 문자의 위치를 찾는다.  

- find_last_of : 주어진 문자들 중 가장 끝에 나타나는 문자의 위치를 찾는다.  

- find_last_not_of : 뒤에서 부터 주어진 문자에 포함되지 않는 문자의 위치를 찾는다.  

- search : 특정 범위의 원소를 찾는다.  


substr은 문자열의 부분 문자열을 리턴하는 string 메소드로서  

`basic_string substr(size_type pos = 0, size_type count = npos) const;`   
다음과 같다. pos는 첫 번째 문자의 위치이고, count 길이만큼 문자열을 리턴한다.  

```cpp
#include<iostream>
#include<string>

using namespace std;

int main()
{
    string str = "abcdefghi";
    cout << str.substr(2, 5);
}
```

```
output

cdefg
``` 

2번째 문자부터 시작해 5의 길이만큼 문자열을 리턴해준다.  
`size_type find(const basic_string& str, size_type pos = 0) const; `  
str은 찾고자 하는 문자열이고 pos는 검색을 시작할 위치이다.  

find와 substr을 이용하는 장점은 delimeter(구분자)가 두종류 이상이더라도 다음과 같이 처리가 가능하다.  

```cpp
#include<iostream>
#include<string>
#include<vector>
#include<sstream>
#include<algorithm>

using namespace std;

// 구분자 배열, split할 문자열, 배열크기, previous
int findMany(string delArr[], string targetStr, int numdel, int previous){

    int *curs = new int[numdel];

    int min = 987654321;
    for(int i=0; i<numdel; i++){
        curs[i] = targetStr.find(delArr[i], previous);
        if(curs[i] == string::npos){
            curs[i] = 987654321;
        }
        if(curs[i] < min){
            min = curs[i];
        }
    }
    if(min == 987654321){
        return string::npos;
    }
    return min;
}

int main()
{
    string str="java/c,c++,python";
    int previous =0;
    int current=0;
    vector<string> x;
    x.clear();
   
    string findchs[2] = {",", "/"};
    //find는 찾을게 없으면 npos를 리턴함
    while((current = findMany(findchs, str, 2, previous))!=string::npos){
        string substring=str.substr(previous,current-previous);
        x.push_back(substring);
        previous = current+1;
    }
    x.push_back(str.substr(previous,current-previous));
    
    for(int i=0;i<x.size();i++){
        cout<<x[i]<<endl;
    }
    
    
    return 0;
}
```
(https://prod.velog.io/@kjpark4321/%EC%BD%94%ED%85%8C-%EB%8C%80%EB%B9%84-c-%EB%AC%B8%EC%9E%90%EC%97%B4-%EC%B2%98%EB%A6%AC)  

<br>
<br>

---

##### 연습하기    

> 공백을 포함한 문자열을 출력하고, 해당 문자열을 `,`를 기준으로 한 줄씩 출력하기  

```cpp
#include <iostream>
#include<vector>
#include <string>
using namespace std;

int main()
{
	string str;
	getline(cin, str);
	vector<string> x;
	x.clear();

	cout << str <<"\n\n\n";

	int current = 0;
	int previous = 0;

	string ch[10000];
		
	//												못 찾으면 npos 리턴
	while ((current = str.find(',', previous)) != string::npos)
	{
		string substring = str.substr(previous, current - previous);
		x.push_back(substring);
		previous = current + 1;
	};
	x.push_back(str.substr(previous, current - previous));

	for (int i = 0; i < x.size(); i++) {
		cout << x[i] << endl;
	};

	return 0;
}
```

```
Input : Hello World, My name is suwan, welcome to my Blog

Output:
Hello World, My name is suwan, welcome to my Blog


Hello World
 My name is suwan
 welcome to my Blog
```

반복문의 조건은 `,` 를 찾지 못하면 반복문을 탈출하게 되어있다.  
current에 previous부터 시작해서 `,`를 찾는다. 처음 반복문을 돌 때는 previous가 0이므로 문자열의 처음부터 쉼표를 찾게 된다.  쉼표를 찾는다면, substr을 사용해 previous. 즉 0번째 문자열부터 시작해서 current(쉼표의 위치 - previous)개의 문자를 배열의 맨 뒤에 넣어준다.  
그리고 난 뒤, previous에 current + 1 한 값을 넣어준다. current는 쉼표의 위치인데 여기에 1을 더해줌으로써 한 번 체크했던 쉼표는 제외하고 그 다음 쉼표를 찾도록 한 것이다.  

더이상 쉼표를 찾지 못해 npos가 리턴되면 반복문을 탈출하게 된다.  
마지막 쉼표 뒤의 문장을 출력하기 위해서 substr을 통해 마지막 문장 또한 배열의 맨 뒤에 넣어준다.  

`str.substr(previous, current - previous)` 이때 previous는 마지막 쉼표 + 1의 자리이고 currnet는 문자열의 맨 마지막 위치이다. 쉼표를 찾지 못했기 때문에 마지막 위치에서 멈췄고 해당 위치를 current에 넣어줬기 때문이다.
current에서 previous를 빼면 마지막 쉼표 다음 문자부터 맨 끝 문자열 까지의 개수가 나온다.  

그 다음 반복문을 통해 배열을 모두 출력하면 된다.  
 
<br>
<br>
<br>
<br>

---

**주석**  

---

<a name="footnote_1">1</a>: 컴퓨터에서 콘솔이나 프린터로 찍었을 떄 공백을 표현하는 문자들을 의미한다.
