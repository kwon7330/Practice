# C++ 객체 지향 프로그레밍

## 절차 지향 프로그레밍 
절차 지향 프로그래밍은 **~하다** 중점의 프로그레밍, 함수들이 각기 자신들의 기능을 절차에 의해 호출
유지보수가 어렵다는 단점이 있다.

## C++ 은 객체 지향 프로그레밍 + 일반화 프로그레밍
### 객체 지향 프로그레밍 (OOP) 
객체 지향 프로그레밍은 **주어** 중점의 프로그레밍으로 프로그렘을 구성하는 객체 간의 의사소통이다.
용량이크고, 속도가 떨어진다는 단점이 있다.

### 객체
객체는 **인스턴스** + **클래스**로 실세계에 존재하는 사물 또는 상황을 코드로 반영한 것이다.


## 추상화
공통적인 요소를 추출하는 과정

## 클래스의 4대속성
- 은닉화, 
- 캡슐화 
- 상속성 
- 다형성

## 일반화 프로그래밍
일반화 프로그래밍은 자료형과 상관없이 지속적으로 사용가능한 프로그래밍을 설계하는 것을 말한다.


## 은닉화
은닉화는 데이터의 보호를 위해 클래스가 가진 문법이다.


### 접근제어 지시자 
사용의 범위를 결졍해주는 지시자 문법으로 public,protected,private 가있다.

- public : 외부에서 접근가능
- private : 외부에서 접근불가능
- protected : 상속된 객체만 접근가능


### access method 
멤버 변수의 접근 또는 값 변경을 위한 수단이다.


```
struct tagInfo
{
public: // 구조체 내부, 외부 접근을 모두 허용한다.
	int m_iHp; // 멤버 변수
private: // 구조체 외부 접근을 허용하지 않는다.

public:
	void Render(); // 멤버 함수
	
}

void tagInfo::Render()
{
	iHp = 100;	//내부접근
	cout << iHp << endl; // 내부 접근
}


class CObj
{
private:
    int         m_iHp;            // 멤버 변수

public:     // access method : 멤버 변수의 접근 또는 값 변경을 위한 수단
    int         Get_Hp()         { return m_iHp; } // 외부에서 멤버 변수인 m_iHp의 값을 읽기 위한 access method이다.
    void        Set_Hp(int _iHp) { m_iHp = _iHp; } // 외부에서 멤버 변수인 m_iHp의 값을 쓰기 위한 access mehtod이다.

    void        Render();
};

void CObj::Render()
{
    //m_iHp = _iNumber;           // 내부 접근
    cout << m_iHp << endl;      // 내부 접근
}


```

## 생성자
객체 생성 시, 자동으로 생성되는 함수들로 default생성자 default복사생성자 default 대입연산자 default 소멸자가 있다.

1. default 생성자는 생성자가 명시적으로 구현되어 있지 않은 경우 '컴파일러' 에 의해 자동생성되며 매개변수가 void 형식으로 되어있다.
2. default 복자 생성자는 객체를 복사하여 생성하고자 할때, 명시적으로 구현되어있지 않다면 '컴파일러'에 의해 자동으로 생성된다.
3. default 대입 연산자는 객체와 특정 값의 대입을 수행하도록 자동적으로 생성되는데 필요시 직접 구현하여 특정기능을 사용 할 수 있도록 만든다. 
4. defautl 소멸자는 소멸자가 명시적으로 구현되어 있지 않은 경우 '컴파일러' 에 의해 자동으로 생성된다.

객체 생성시에는 반드시 생성자가 호출되어야하고 생성자는 멤버 변수를 초기화 하는 수단으로 사용된다.

## 객체생성과소멸 과정

메모리할당 -> 생성자 호출 -> 소멸자 호출 -> 메모리 반환


```
class CObj
{
public:
   CObj(); // 생성자 구현
   ~CObj(); // 소멸자 구현

public:
    void Render() { cout << m_iA << endl; }

private:
    int m_iA;
};

CObj::CObj()
{
    cout << "생성자 호출" << endl;
    m_iA = 100;			// 대입을 통한 초기화 문법
}

CObj::~CObj()
{
    cout << "소멸자 호출" << endl;
}


int main()
{
    CObj obj;
    obj.Render();

    //생성자 호출 100 소멸자 호출 순으로 출력되게된다.


    return 0;
}
```

## 용어정리

### 객체 배열
객체 배열은 객체를 담는 배열을 뜻한다.
### 객체 배열 포인터
객체 배열을 가리키는 포인터 변수를 말한다.
### 객체 포인터 배열
객체를 가리키는 포인터를 담는 배열을 뜻한다.

## explict
프로그레머가 명령하지 않은 기능을 막아주게 하는 명령어이다.

```
class CObj
{
public:
    CObj(int _iA) { m_iA = _iA; } 
    ~CObj() {}

public:
    void Render() { cout << m_iA << endl; }

private:
    int m_iA;
};


int main()
{
    CObj obj = 100; // obj(100) 과 같은 결과 (묵시적 캐스팅)
    obj.Render();
   
    return 0;
}
```

이때 컴파일러가 defualt 대입 연산자를 호출하여 맴버 변수에 100을 대입하게 된다.
이는 프로그레머가 의도한것이 아니기 떄문에 이를 해결하기 위해서 explict를 붙여서
프로그레머가 명령하지 않은 기능을 막는다.

## 전방선언
전반선언은 자료형의 유무를 먼저 알려주는 문법으로 해당 클래스의 멤버함수 호출 권환을 주지 않는다.
1. 상호 참조 대상인 클래스의 객체가 아닌 포인터 형식으로 멤버 변수를 선언.
2. cpp 파일에 참조 대상 클래스의 헤더 파일을 포함하여 함수를 호출.
3. 상호 참조하는 클래스 중 한 클래스만 전방 선언 문법을 사용해도 된다.

### CBoy.h
```
class CBoy
{
public:
    CBoy()

public:
    void Render();
    void Output();

private:
    CGirl& m_pGirl;

```
### CBoy.CPP
```
CBoy::CBoy()
{
	m_pGirl = new CGirl;
}

void CBoy::Render()
{
	cout << "hello boy" << endl;
}

void CBoy::Output()
{
	cout << "CGirl : ";
	m_pGirl->Print();

}
```
### CGirl.h
 
 ```
 class CGirl
{
public:
	CGirl();
	~CGirl();
public:
	void	Initialize();
	void	Print();
	void	Draw();
	void	Release();

private:
	CBoy*		m_pBoy;
};
 ```
### CGirl.CPP
 ```
 CGirl::CGirl()
{
	
}

CGirl::~CGirl()
{
	Release();
}

void CGirl::Initialize()
{
	m_pBoy = new CBoy;
}

void CGirl::Print()
{
	cout << "Girl 클래스 함수입니다" << endl;
}

void CGirl::Draw()
{
	cout << "Boy : ";
	m_pBoy->Render();
}

void CGirl::Release()
{
	if (m_pBoy)
	{
		delete m_pBoy;
		m_pBoy = nullptr;
	}
}
 ```
CBoy 클래스는 CGirl 객체를 참조하는데, CGirl 클래스의 정의를 알 수 없고,
CGirl 클래스도 마찬가지로 CBoy 객체를 참조하는데 CBoy의 정의를 알 수 없다.
따라서 무한루프가 걸리게된다.
전방선언을 사용하면 CBoy와 CGirl이 서로의 정의를 알지 못하는 상황에서, 각각의 클래스가 선언만 되어 있고, 
컴파일러는 서로의 정의를 필요로 하지 않기 때문에 무한루프 문제를 해결 할 수 있게된다.


## 레퍼런스
C++의 자료형으로 포인터를 대체하기 위한 문법으로 변수에게 별명을 짓는 것으로 이해 할 수 있다.

### 포인터를 사용한 간접 참조
```
int main()
{
    int iData = 0;
    int* p = &iData; // 간접 참조
    *p = 10;
    cout << iData << endl;
   
    return 0;
}
```
### 레퍼런스를 사용한 직접 참조
```
int main()
{
    int iData = 0;
    int& ref = iData; //레퍼런스는 선언과 동시에 lvalue로 초기화해한다.

    ref = 200;

    cout << sizeof(ref) << endl; // 레퍼런스는 크기가 없다.
    cout << ref << endl;
   
    return 0;
}
```

### 레퍼런스의 한계
1. 레퍼런스 자료형은 l-Value만 참조가 가능하다.
    - 만약 const를 사용하여 읽기 전용으로만 참조를 한다면 r-value도 참조 가능하다.
    - r-value 레퍼런스를 사용하면 r-value도 참조 가능하다.

2. 레퍼런스는 선언과 동시에 반드시 참조 대상을 지정해 초기화를 해야한다.

3. 레퍼런스는 오직 하나의 데이터만 참조 가능하다.

4. 레퍼런스는 동적할당이 불가능하다.

```
int main()
{
	int	iTest(100);
	
	int& r = iTest;
	
	r = 200;
	
	int	iSrc(4000);
	
	r = iSrc; 
	// 여전히 iTest를 참조하고있지만 값을 iSrc에 담겨져있는 4000으로 변경
	
	cout << iTest << endl; 
	cout << r << endl;
	
	r = 5000;
	
	cout << iTest << endl;
	cout << iSrc << endl;

  
    return 0;
}
```

## extern
extern은 다른 파일에 해당 전역 변수의 유무를 알려주는 문법이다.
자료형과 변수 이름이 완벽히 일치해야하고, 
extern으로 선언하는 시점에 메모리 크기를 갖지 않고, 초기화나 값 변경이 불가능하다.

## main.cpp
```
#include "CObj.h"

int g_iNumber = 100; // 전역변수 선언


int main()
{
    CObj obj;
    obj.Render(); // 맴버 함수 호출

    return 0;
}

```

### CObj.h

```

#pragma once

extern int g_iNumber; // extren 키워드를 사용해서 main의 전역변수를 가져왔다.
					  // 이 때 자료형과 변수명은 완벽히 일치해야한다.

class CObj
{
public:
	void Render() { cout << "COJ :" << g_iNumber; } // 값을 출력

};


```

출력값 : COJ :100

## 이니셜라이저

### 대입을 통한 멤버 변수 초기화
```
class CObj
{

public:
	CObj(int _iA) { m_iA = _iA; }

private : 
	int m_iA;
};
```
### 이니셜라이저를 통한 멤버 변수 초기화
```
class CObj
{

public:
	CObj(int _iA) : m_iA(_iA) {}

private : 
	int m_iA;
};
```
### 대입을 통한 초기화 vs 이니셜라이저
대입 초기화
	- 1. 멤버 변수는 기본 생성자에 의해 초기화되고
	- 2. 생성자 본문에서 대입 연산을 통해 두 번째로 값이 할된다. 
이 과정에서 불필요한 추가 작업이 발생하게 된다.

이니셜라이저
	- 멤버 변수를 생성자의 본문으로 들어가기 전에 이미 초기값을 할당한다.

## const와 클래스

### const와 멤버 변수
클래스 안 멤버변수에 const로 선언을 하였을 때 그값을 변경하는것은 불가능하다.
하지만 이니셜라이저를 통해 생성과 동시에 초기화를 하면 const가 붙은 멤버 변수여도 값 변경이 가능하다.

### const와 멤버 함수
public: 으로 되어있는 멤버 함수 뒤 에 const키워드를 붙이면 함수 자체가 읽기 전용이 된다고 생각 하겠지만,
**멤버 변수** 를 제외하고는 모두 쓰기가 가능하다.

또한 const안에서 멤버함수를 호출하면 오류가 나는데, 그 멤버 함수가 멤버변수를 쓰는 기능의 함수 일 수 있기 때문이다.
만약 멤버함수가 같은 **const멤버 함수**라면 호출이 가능하다.


```
int g_iTemp = 0;

class CObj
{
public:
	CObj() : m_iA(100), m_iB(200){}
	CObj(int _iA, int _iB) : m_iA(_iA), m_iB(_iB) {}

public:

	void		Render() const { cout << "hello korea" << endl; } // const 멤버 함수
	void		Print()	const { cout << "hello jusin" << endl; }
	void		Draw()	const;	


private:
	const int		m_iA; // const 멤버 변수
	int				m_iB;
};

void	CObj::Draw()	const
{
	//int		iData = 100; // 지역변수
	//
	//iData = 200;					// 쓰기
	//cout << iData << endl;		// 읽기

	// 전역변수
	// g_iTemp = 30000;				// 쓰기
	// cout << g_iTemp << endl;		// 읽기


	// static변수
	// static int	iStatic = 500;
	// iStatic = 600;				// 쓰기
	// cout << iStatic << endl;		// 읽기


	// 포인터 변수
	// int* p = new int(10);
	// 	
	// *p = 20;						// 쓰기
	// cout << *p << endl;			// 읽기


	// 멤버 변수
	//m_iB = 500;					// 쓰기(멤버 변수 쓰기만 불가능)	
	//cout << m_iB << endl;			// 읽기

	// const멤버 함수
	Print();
}
```

## Static과 전역변수

### Static 변수
데이터 영역에 할당 되며, staic 변수는 정적 변수로 내부(함수) 에서만 접근 가능한 정적변수이다.

### 전역변수
데이터 영역에 할당 되며, 전역변수는 외부에서 접근 가능한 정적변수이다.

### 데이터 영역 메모리의 특성
데이터 영역에 할당되는 메모리들은 초기화 되지 않으면 BSS로 가서 0으로 초기화 되는 특성이 있다.


## 클래스 변수
클래스 변수는 동일 데이터 타입 인 다른 객체끼리 공유할 수 있는 변수를 말한다.

### 초기화 방법
```
class CObj
{
public:
	CObj(int _iB) : m_iB(_iB) {} // 멤버 변수 초기화

public:
    static int     m_iA;  // 클래스 변수
private:
    int             m_iB; // 멤버 변수
}
int CObj::m_iA = 200; // 클레스 변수 초기화
```

### 클래스 변수 vs 멤버 변수

클래스 변수는 동일한 타입의 여러 객체를 선언했을때 모두 동일한 값이 공유된다.
반면, 멤버 변수는 각 객체 마다 따로 멤버 변수 가지고 있어서 독립적으로 사용한다.

## static 맴버 함수
static 멤버함수는 static 멤버 변수와 함수만 사용가능하고, 멤버 변수는 사용이 불가능하다.

```
class CObj
{
public:
	CObj();
	~CObj();

public:
	void Render() { cout << m_iA << endl; }
	static void Draw() { cout << m_iB << endl; }
	static void Print()
	{
		Render(); // 멤버 함수 호출 불가능
		m_iA = 10; // 멤버 변수 쓰기 불가능
		cout << m_iA << endl;  // 멤버 변수 읽기 불가능

		m_iB = 0; // 클래스 변수는 사용이 가능하다.
		cout << m_iB << endl;
		Draw(); // static 함수 사용가능.
	}

private:
	int m_iA;
	static int m_iB;
};
```

### Private 생성자 소멸자
```
class CObj
{
private:
	CObj(int _iA) : m_iA(_iA) {}
	~CObj() {}

public:
	void Render() { cout << m_iA << endl; }
	void Set_A(int m_iA) { this->m_iA = m_iA; }
	CObj* Get_This() { return this; } // 객체의 고유 주소를 반환
	static CObj* Create()
	{
		CObj* pObj = new CObj(100);
		return pObj;
	}
	void Destroy() { delete this; }

private:
	int m_iA;
};
```
위 상황을 보면 생성자와 소멸자를 private: 로하여 외부에서 마음대로 객체를 생성하지 않게 막고있다.
이때 static 멤버 함수를 통해 외부에서 객체를 생성하고, 그객체의주소를 반환시킨다.
	-**싱글턴 패턴**도 한번 참고해보자.

## this 포인터
this 포인터는 생성된 객체의 고유 주소(상수 포인터)이다.
위의 코드에서 private로 되어있는 소멸자를 대신하여 외부에서 객체를 제거할때 사용한다.

## 복사 생성자
복사 생성자는 객체를 복사할때 데이터 메모리 블록 자체를 통째로 복사를 통해 관리하여 사용 할수 있게한다.
명시적으로 정의하지 않으면 컴파일러가 default 복사 생성자를 호출하여 **앝은 복사**를 하게된다. 동적할당된 메모리를
다룬다면 복사생성자를 직접 구현하여 **깊은 복사**를 해야한다.

### 복사 생성자가 호출되는 경우
#### 매개 변수로 전달하여 객체를 생성하는 경우
```
class CObj
{
public:
	CObj(int _iA) : m_iA(_iA) { cout << "int형 생성자 호출" << endl; }

	CObj(const CObj& rhs)
		: m_iA(rhs.m_iA) { cout << "복사 생성자 호출" << endl; }

public:
	void	Render() { cout << m_iA << endl; }

private:
	int		m_iA;
};

int main()
{
    
	CObj Temp(100);
	Temp.Render();

	CObj Sour(Temp); 이전의 만든 객체를 파라미터에 대입하여 객체를 복사한다.
						
	Sour.Render();

    return 0;
}
```

#### 함수의 매개변수가 객체 타입인 경우
```
class CObj
{
public:
	CObj(int _iA) : m_iA(_iA) { cout << "int형 생성자 호출" << endl; }

	CObj(const CObj& rhs)
		: m_iA(rhs.m_iA) { cout << "복사 생성자 호출" << endl; }

public:
	void	Render() { cout << m_iA << endl; }

	void	Draw(CObj Param)	// call by value : 값 복사에 의한 호출
	{							
		Param.Render();
	}

private:
	int		m_iA;
};


int main()
{
    
	CObj Temp(100);
	Temp.Render();
	
	CObj Dest(200); //Dest객체를 200으로 초기화하고
	Temp.Draw(Dest); // 함수의 매개변수가 객체 타입인 함수에 복사할 객체를 넣었을 떄 값에 의해 호출된다.
	
    return 0;
}
```


#### 함수의 반환 타입이 객체 타입인경우
값으로 반환되는 객체는 호출된 함수에서 새로운 객체를 만들어야하기 때문에 복사생성자를 호출한다. 이때 Temp의 값이 새로운 객체로 복사된다.
```
class CObj
{
public:
	CObj(int _iA) : m_iA(_iA) { cout << "int형 생성자 호출" << endl; }

	CObj(const CObj& rhs)
		: m_iA(rhs.m_iA) { cout << "복사 생성자 호출" << endl; }

public:
	void	Render() { cout << m_iA << endl; }

	CObj	Get_Obj() { return *this; }	// 3. 함수의 반환 타입이 객체 타입인 경우 


private:
	int		m_iA;
};


int main()
{
    
	CObj Temp(100);
	
    Temp.Get_Obj().Render();	

    return 0;
}
```


