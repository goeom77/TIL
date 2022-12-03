# C++ 기초

복습: No
작성일시: 2022년 12월 3일 오후 3:40

## ✨입출력

```cpp
#include <iostream>

using namespace std; // namespace 소스코드 사용

int main()
{
	cout << "Hello C++ World" << endl;
	//std::cout << "Hello C++ World" << std::endl; 소스코드를 사용하지 않으면
	return 0;
}
```

1. `cout << ' ' << endl;`   : '  '를 출력하시오
2. `;` : 한 행의 종료
3. `return 0;` : 프로그램 종료
4. `cin >> number` : 정수형 변수 number 선언
5. `const int kNowYear = 2022` : const로 할당한 상수는 프로그램 종료 전 변경 불가능
// google 권장 앞에 k붙이기

```cpp
#include <iostream>

using namespace std; // namespace 소스코드 사용

int main()
{
	int number = 0; // 정수형 변수 number 선언;
	// int 적지 않으면 선언되지 않은 식별자입니다. 경고!
	cin >> number; // 사용자 입력
	
	cout << '입력한 숫자는' << number << '입니다' << 'endl;

	return 0;
}
```

## ✨자료형

1. char : 문자형 변수, 하나의 문자만 저장, `‘C’` : 한개의 쿼테이션 사용
2. int : 정수형 변수
3. double : 실수형 변수, 소수점을 다룰 때 float는 한계가 있어 double사용
4. bool : true / false
5. string : 문자열 변수, `"Hello World"` : 더블 쿼테이션 사용

## ✨조건문

1. if ~ else
    
    ```cpp
    #include <iosream>
    
    using namespace std;
    
    int main()
    {
    	int x = 10;
    	int y = 2;
    	if (x > y)
    		cout << "x는 y보다 큽니다 << endl;
    	else
    		cout << "x는 y보다 작습니다 << endl;
    
    	return 0;
    }
    ```
    
2. for
    
    ```cpp
    #include <iostream>
    
    using namespace std;
    
    int main()
    {
    	int sum1 = 0;
    	
    	for (int i = 0; i < 5; i++) // 0 + 1 + 2 + 3 + 4
    	{
    		sum1 += i;
    	}
    	cout << "합산결과는" << sum1 << "입니다" << endl; // 10
    
    	return 0;
    }
    ```
    

## ✨배열

💡 쓰는 이유

1. 코드가 길어지고 전체 프로젝트 규모가 커질 때 효율적 사용
2. 비슷한 유형의 데이터는 따로 선언하여 사용하는 것보다 배열에 담아 꺼내 쓰기

```cpp
#include <iostream>

using namespace std;

int main()
{
	const int kArraySize = 3; // 배열의 크기 정해놓기

	int founding[kArraySize]; // 크기가 3인 배열 선언
	founding[0] = 1;
	founding[1] = 2;
	founding[2] = 3;

	cout << "첫번째 :" << founding[0] <<endl; //펏번째 :1
	cout << "두번째 :" << founding[1] <<endl; //두번째 :2
	cout << "세번째 :" << founding[2] <<endl; //세번째 :3

	return 0;
}
```

## ✨함수

```cpp
#include <iostream>

using namespace std;

void Minus(const int x, const int y)
{
	cout << " x - y = " << x-y << endl;
}

int Plus(const int x, const int y)
{
	return x + y; // return 값이 없으면 오류 발생
// return 값이 없는 경우 pass할수 있는 방법은? for문에서 if로 막아줘야되나?
}

int main()
{
	Minus(10,5);

	cout << " x + y = " << Plus(2,6) << endl;

	return 0;
}
```

cf ) 

한줄 주석 : `//`

여러줄 주석 : `/* */`

## ✨네임스페이스

💡 특징

1. 같은 이름의 변수나 함수가 있는 경우를 해결
2. 원리는 변수나 함수를 해당 영역에서만 유효하도록 제한

```cpp
#include <iostream>

using namespace std;

namespace silla
{
	int year = 935;

	void CentralArea()
	{
		cout << "경상도" << endl;
	}
}

using namespace silla;

int main()
{
	cout << "신라 중심지 : ";
	silla::CentralArea(); // 신라 중심지 : 경상도
	cout << "신라 멸망연도 :" << silla::year << endl; // 신라 멸망연도 : 935

	return 0;
}
```

## ✨include 함수 배우기

💡 외부 라이브러리 사용하기

```cpp
#include <iostream>
#include <vector>

using namespace std;

int main()
{
	vector<int> exam;
	exam.push_back(10); //차후 배우기
	...
	return 0;
}
```

## ✨ 스코핑룰

💡 변수의 범위 이해하기

```cpp
#include <iostream>

using namespace std;

int x = 10;

int Func1()
{
	int y = x + 10; //밖의 x를 그대로 사용
	return y; // y = 20
}
int Func2()
{
	int x = 100;
	return x; // x = 100
}
int main()
{
	cout << "y= " << Func1() << endl; // y = 20
	cout << "x= " << Func2() << endl; // x = 100
	cout << "x= " << x << endl; // x = 10

	return 0;
}
```