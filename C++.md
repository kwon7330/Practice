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
이는 프로그레머가 의도한것이 아니기 문에 이를 해결하기 위해서 explict를 붙여서
프로그레머가 명령하지 않은 기능을 막는다.

## 전방선언
전반선언은 자료형의 유무를 먼저 알려주는 문법으로 해당 클래스의 멤버함수 호출 권환을 주지 않는다.
1. 상호 참조 대상인 클래스의 객체가 아닌 포인터 형식으로 멤버 변수를 선언.
2. cpp 파일에 참조 대상 클래스의 헤더 파일을 포함하여 함수를 호출.
3. 상호 참조하는 클래스 중 한 클래스만 전방 선언 문법을 사용해도 된다.

#### CBoy.h
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
#### CBoy.CPP
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
#### CGirl.h
 
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
#### CGirl.CPP
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

#### main.cpp
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

#### CObj.h

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
	Temp.Draw(Dest); // 함수의 매개변수가 객체 타입인 함수에 복사할 객체를 넣었을  값에 의해 호출된다.
	
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

## 얕은 복사 VS 깊은 복사



### 얕은 복사
```
class CObj {
public:
    explicit CObj(int _iA) : m_iA(_iA)
    {
        m_pData = new int(_iA);  // 동적할당
        cout << "생성자 호출" << endl;
    }

    // 얕은 복사 생성자
    CObj(const CObj& rhs) : m_iA(rhs.m_iA) 
    {
        m_pData = rhs.m_pData;
        cout << "앝은 복사 생성자 호출 " << endl; 
    }


    ~CObj() { delete m_pData; cout << "소멸자 호출" << endl; }  // 동적으로 할당된 메모리 해제

    void Render() { cout << m_iA << ", " << *m_pData << endl; }

private:
    int m_iA;
    int* m_pData;  // 동적 메모리 할당
};

int main() {
    CObj obj1(10);
    CObj obj2 (obj1);  // 복사 생성자 호출
  
    obj2.Render();  

    return 0;
}

```

위와 같은 상황에 얕은 복사를 사용하면 소멸자가 호출될 때 문제가 생긴다. 
얕은 복사를 하게되면 두객체에서 m_pData가 동일한 메모리를 가리키게되는데 이때 소멸자가 호출하게되면 복사 객체의 소멸자에서
m_pData를 삭제해버리기 문에 원본 객체에서 소멸자가 호출 되었을때 삭제해야할 메모리가 없게된다.

위 문제는 깊은 복사로 해결할 수 있다.

### 깊은 복사
	-멤버 변수로 포인터가 있다.
	-생성자 안에서 어떤 메모리건 포인터에 주소를 참조시킨다.(동적할당이 일반적인 예)
	-heap 메모리 주소를 소멸자에서 소멸 시키는 경우

```
class CObj {
public:
    explicit CObj(int _iA) : m_iA(_iA)
    {
        m_pData = new int(_iA);  // 동적할당
        cout << "생성자 호출" << endl;
    }


     //깊은 복사 생성자
    CObj(const CObj& rhs) : m_iA(rhs.m_iA) 
    {
        m_pData = new int(*(rhs).m_pData);  // 새로운 메모리 할당 후 값 복사
        cout << "깊은 복사 생성자 호출" << endl;
    }

    ~CObj() { delete m_pData; cout << "소멸자 호출" << endl; }  // 동적으로 할당된 메모리 해제

    void Render() { cout << m_iA << ", " << *m_pData << endl; }

private:
    int m_iA;
    int* m_pData;  // 동적 메모리 할당
};

int main() {
    CObj obj1(10);
    CObj obj2 (obj1);  // 깊은 복사 생성자 호출
  
    obj2.Render();  

    return 0;
}
```

깊은 복사를 통해 새로운 메모리를 할당한 후 값을 복사하게되면 메모리를 반납할 때 서로 다른 주소를 반환 할 수 있게된다.


## friend
friend키워드는 다른 클래스에서 private: 접근자에도 접근 할 수있도록 허용해주는 키워드이다.

#### CObj.h
```
#include "COther.h" 
class CObj
{
    friend class COther;           // COther 클래스는 CObj 클래스의 private 멤버에 접근 가능
    friend void COther::Render();  // COther::Render() 함수는 CObj의 private 멤버에 접근 가능

public:
    CObj(int _iA) : m_iA(_iA) {}
    ~CObj() {}

private:
    int m_iA;
};
```

#### COther.h
```
class CObj; // CObj 클래스 선언

class COther
{
public:
    void Render();  // Render 함수 선언
};
```

```
#include "pch.h"
#include "COther.h"
#include "CObj.h"
void COther::Render()
{
    CObj* pObj = new CObj(100);

    pObj->m_iA = 500;  // CObj의 private 멤버에 접근하여 값 수정

    cout << pObj->m_iA << endl;  // CObj의 private 멤버를 출력

    cout << "Other" << endl;
}

```


## 상속
상속이란 공통적인 메소드를 하위 계층에서 제공 받아 사용 할 수 있도록 문법 이다.
서로 다른 자료형에 해당하는 자식 클래스들을 공통된 부모 자료형으로 묶어서 관리할 수 있다.

### 부모 클래스
상위 계층의 클래스로 일반화 되어 있는 클래스이다. 공통적이고, 일반적인 부분이 많은 클래스이다.

### 자식 클래스
하위 계층의 클래스로 구체화 되어 있는 클래스이다.

##### 자식 클래스가 있는 파일에서 지켜야 할 규칙
	1. 반드시 부모 클래스의 헤더 파일을 포함해야 한다.
	2. 자료형 옆에 상속이라는 문법을 적용
	```
	#include "CObj.h"
	class CPlayer : public CObj // CPlayer는 CObj 라는 부모 객체로 부터 상속을 받았다.
	{
	public:

	};

	```
### 상속의 조건
	1. is-a : 자식 is a 부모 : 자식은 부모이다.
	2. has-a : 자식 has a 부모 : 자식이 부모의 메소드를 소유하고 있다.
	
### 자식 객체 생성과 소멸
	1. 메모리할당
	2. 부모생성자 호출
	3. 자식생성자 호출
	4. 자식 소멸자 호출
	5. 부모 소멸자 호출
	6. 메모리 반환

### protected
private속성을 띄지만 자식클래스에게는 public처럼 접근가능하게 한다.
부모객체에 있는 멤버 변수는 자식에서 접근가능하다.


```
class CObj
{
public:
    CObj() {}
    CObj(int _iA) : m_iA(_iA) { cout << "부모 생성자 호출 " << endl; };
    ~CObj() { cout << "부모 소멸자 호출" << endl; }

protected: // 자식에게 멤버 변수 접근을 허용하겠다.
    int m_iA;
};

class CChild : public CObj
{
public:
    CChild()  { cout << "자식 생성자 호출 " << endl; }
    ~CChild() { cout << "자식 소멸자 호출 " << endl; }
   
public:
    void Render() { cout << "자식 함수" << endl; }

};
int main() {
   
    CChild Chi;
    Chi.Render();
    return 0;
}
```

## 바인딩
프로그램 소스에 쓰인 각종 내부요소, 이름, 식별자 들에 대해 값 또는 속성을 확정한 **시점**

## 정적 바인딩
정적바인딩 : 바인딩 과정이 **컴파일 시점** 에 이루어지는 바인딩을 정적 바인딩이라고한다.
			소스상에 명시적으로 타입과 그 타입의 변수를 선언하는것을 정적 바인딩이라고한다.
			- 장점 : 컴파일시 타입에 대한 정보가 결정되기 문에 속도가 빠르고, 타입에러로 인한 문제를 조기에 발견가능.
			- 단점 : 컴파일시 결정되어 그이후 런타임 에 변경이 불가능하다.

## 동적 바인딩
동적 바인딩 : 바인딩 과정이 **실행중** 에 이루어지는 바인딩을 동적 바인딩이라고한다.
			 - 장점 : 실행중에 필요한 객체의 함수를 호출 함으로써 유연성을 가지고 있다.
			 - 단점 : 변수의 예상 치 못한 타입으로 인해 안정성이 떨어진다.


## 객체 포인터
객체의 주소를 저장하는 포인터로 객체 포인터를 사용하여 앞으로 자식클래스는 부모타입의 포인터로 사용할 것이다.

컴파일러는 선언되어 있는 자료형을 보고 바인딩을 하기 때문에 실제로 가리키는 객체가 무엇이든 포인터의 자료형을 기반으로
호출대상을 결정한다.

```
int main() {
   
    CObj* Child = new CChild();
    Chi.Render(); // 부모객체 포인터를 사용하여 CChild객체를 선언하였기 문에 Render함수에 접근할 수없다.
    return 0;
}
```

위처럼 부모클래스가 자식 클래스의 함수를 사용 할 수 없는 이유가 정적 바인딩 때문이다.


## 다형성
상속은 부모타입의 자료형으로 **그룹핑**하여 관리하겠다는 것이다. 그룹핑을하면 자식 데이터 타입 안의 정보를 부모 타입
이 알고있지 않아서 부모타입으로 객체를 생성했을 접근하지 못하는 문제가 생긴다.

이를 다형성을 통해 해결할 수있다.

다형성이란 부모타입 객체를 구체화(부모클래스에서 자식클래스로 내려갈 수록 개별적인 기능으로 변하는 것) 하여 사용하도록 만드는 문법이다.

### 다형성의 종류
	1. 오버라이딩 : 자식들이 모두 갖고 있어야하는 기능일  주로 사용.
	2. 자식 객체가 개별적인 기능을 갖고 있을때 주로 사용.

## 오버라이딩
클래스의 문법으로 
	- 클래스의 상속관계가 성립해야한다.
	- 부모와 자식 클레스에 생김새가 일치하는 함수가 있어야한다.
	- 부모의 함수 앞에 virtual 키워드(**가상함수**)가 있어야 한다.

## 가상 함수
가상 함수가 호출되는 것을 동적 바인딩이라고한다.
virtual 키워드가 붙게되면 vptr(가상포인터) 와 vtbl(가상테이블) 이 형성된다.
vptr은 가상함수 테이블의 가상함수를 불러오는 역활을하고, vtbl은 가상함수 들을 모아놓은 목록이다.

부모와 자식은 독립적인 vptr과 vtbl을 가지고 오버라이딩 된 가상함수들은 상속되어 내려가게된다.
이렇게 됨으로써 부모포인터로 자식 객체를 생성 했을때 가상함수 오버라이딩으로 자식안에 있는 가상함수에 접근이 가능하여 사용할 수 있게된다.

```
class CObj
{
public:
    virtual void	Render() { cout << "부모" << endl; }	 
    virtual void	Draw() { cout << "부모" << endl; }
};

class CChild : public CObj
{
public:
    virtual void	Render() override { cout << "자식" << endl; } 
};

int main()
{
    CObj* Child = new CChild;
    Child->Draw();
    Child->Render();
```

## 순수 가상함수
오버라이딩의 수단으로만 만들어진 함수로 부모클래스에 선언하는 문법이다.

## 추상 클래스
**객체 생성이 불가능한 상태** 로 오로지 내부의 메소드를 제공하기 위한용도의 자료형이다.
순수 가상함수를 포함하는 객체를 추상클래스라고한다. 추상클래스는 개별적으로 객체 생성이 불가능하다.
또한 순수 가상함수는 반드시 자식클래스에서 몸체를 구현해야한다.

```
class CObj abstract // 추상클래스 키워드
{
public:
    virtual void	Render() = 0; // 순수 가상함수
    virtual void	Draw() { cout << "부모" << endl; }
};

class CChild : public CObj
{
public:
    virtual void	Render() { cout << "자식" << endl; } // 자식클래스에서 반드시 몸체를 구현해야한다.
};

int main()
{
    CObj* Child = new CChild;
    Child->Render();
}
```


## 가상 소멸자
부모 포인터로 자식타입의 객체를 선언했을때 자식 객체의 소멸자가 호출되지 않는다.
객체의 소멸과정은 자식 소멸자 -> 부모 소멸자 -> 메모리 반환 순이다. 소멸자에 virtual 을 붙이지 않게되면 부모 포인터로 접근해도
자식의 객체의 정보를 알 수 없기 때문에 virtual을 붙여 부모 포인터를 통해 자식 클래스의 소멸자를 호출 시켜 올바른 소멸 과정을 유도해야한다.

```
class CObj abstract // 추상클래스 키워드
{
public:
    CObj() { cout << "부모 생성자 호출" << endl; }
    virtual ~CObj() { cout << "부모 소멸자 호출" << endl; }
    virtual void	Render() = 0; // 순수 가상함수
    virtual void	Draw() { cout << "부모" << endl; }

protected:
    int m_iA;
};

class CChild : public CObj
{
public:
    CChild() { cout << "자식 생성자 호출 " << endl; }
    ~CChild() { cout << "자식 소멸자 호출 " << endl; }
    virtual void	Render() { cout << "자식" << endl; } // 자식클래스에서 반드시 몸체를 구현해야한다.
};

int main()
{
    CObj* Child = new CChild;
    Child->Render();
    delete Child;
}
```

## 다운캐스팅
C++의 캐스팅 연산자로 어떤 종류의 캐스팅이건 **안전한 케스팅은 존재 하지 않는다.**

	1. static_cast<>() : 컴파일 타임에 형변환을 한다. C스타일에 캐스팅과 유사 논리적인 캐스팅이다.
	2. dynamic_cast<>() : 가상함수 테이블을 사용하고, 런타임중에 안전검사를 사용하기 때문에 
						  static_cast보단 안전하지만 속도가 느리다. 안전하지 않은 형변환일는 nullptr을 반환한다.
	3. const_cast<>()_ : const 속성을 벗겨내기 위한 도구, 포인터나 레퍼런스 자료형만 적용 가능
	4. reinterpret_cast : const 포인터를 제외한 모든 포인터 형 변환을 허용, 논리적으로 맞지 않는 형 변환도 허용한다.
						  예측 할 수 없는 결과를 초래하기 때문에 사용하지 않을 것을 권장한다.



## 인라인 함수
inline 함수는 함수를 선언과 동시에 몸체까지 완전 구현해 놓은 상태로 매크로 함수와 유사하지만 
			  자료형에 따라 함수를 계속 만들어야 한다.

```
inline int			Mul(int x)
{
	return x * x;
}
```

## 연산자 오버로딩
연산자 오버로딩은 함수 문법으로, 사용자가 연산자 이름으로 된 함수를 만들어서 사용하는 문법으로
				 객체 만 사용 가능하고, 연산자 기준으로 왼쪽 기준으로 작동한다.
				 연산자 오버로딩은 stl에서 주로 사용하고 함수객체를 만들어야 하기 문에 알아야하는 문법이다.
				 
#### 연산자 오버로딩을 통한 대입연산자 구현
```
#include "pch.h"

class CObj
{
public:
    CObj() {}
    explicit CObj(int _iX, int _iY) : m_iX(_iX), m_iY(_iY) {}

    // 연산자 오버로딩을 통해 default 대입 연산자 구현
    CObj& operator =(CObj& rObj)
    {
        m_iX = rObj.m_iX;
        m_iY = rObj.m_iY;

        return *this;
    }
public:
    void Render() { cout << m_iX << "\t" << m_iY << endl; }


private:
    int m_iX;
    int m_iY;
};


int main()
{
    CObj Temp(10,20);
    CObj Src = Temp;

    Temp.Render();
    Src.Render();

    return 0;
}


```

#### 연산자 오버로딩 전역함수 
```
public:
    void Render() { cout << m_iX << "\t" << m_iY << endl; }

    
    CObj operator +(CObj& rObj)
    {
        CObj Test(m_iX + rObj.m_iX, m_iY + rObj.m_iY);
        return Test;
    }

    CObj operator +(int _iData)
    {
        CObj Test(m_iX + _iData, m_iY + _iData);
        return Test;
    }
```

```

//  전역함수로 연산자 오버로딩 함수를 만든다.
CObj operator +(int _iData, CObj& rObj)
{
    CObj Test(rObj + _iData); // +연산자 오버로딩을 한 멤버 함수를 호출하여 사용
    return Test;
}

```


## 임시객체
임시 객체는 특정 표현식에서 일시적으로 생성되어 해당 표현식이 끝나면 바로 소멸하는 객체를 말한다.

임시객체는 이름이 없고 생성된후 해당 문장이 끝나면 바로 소멸된다. 또한 함수가
객체를 반환할 때 반환 값을 잠깐 담아두기 위해 임시객체가 생성되곤 한다.
```
class CTest
{
public:
    CTest(const char* pStr)
    {
        strcpy_s(m_szName, sizeof(m_szName), pStr);
        cout << m_szName << "생성자" << endl;
    }
    ~CTest()
    {
        cout << m_szName << "소멸자" << endl;
    }

private:
    char m_szName[20];
};

int main()
{
    CTest Test("일반적인 객체");
    cout << "임시객체 생성 " << endl;
    CTest("임시 객체"); // 임시 객체
    cout << "임시객체 소멸 " << endl;

    return 0;
}
```

#### 임시객체 생성자 소멸자 호출순서
	1. 일반적인 객체 생성자 호출
	/////////////////////////////////////////
	2. 임시 객체 생성자 호출
	3. 임시 객체 소멸자 호출
	//////////////////////////////////////// 한줄 만에 생성되고 소멸되게 된다.
	4. 일반적인 객체 생성자 호출


## 함수 객체
() 연산자 오버로딩을 통해 객체를 함수처럼 사용하는 문법이다.
	- 같은 호출 문장이라도 실제 어떤 객체냐에 따라 각기 다른 상태를 지닐 수 있다.
	- 클래스 선언부에 맴버 형태의 함수를 구현하다보니 자동으로 
		inline화 되어 일반 함수보다 호출 속도가 빠르다.

```

class CPlus
{
public:
    int operator()(int _Dst, int _Src)
    {
        return _Dst, _Src;
    }
};

int main()
{
    CPlus Plus;
    cout << Plus(10 , 20) << endl;
    return 0;
}

```


## template
템플릿은 틀, 찍어내기 위한 도구로 기능은 결정되어 있으나 자료형은 결정되어 있지 않은 상태이다.


### template의 종류

- 함수 템플릿 : 함수의 형식을 띄고 있는 템플릿, 함수를 찍어내는 도구
- 클래스 템플릿 : 클래스의 형식을 띄고 있는 템플릿, 클래스를 찍어내는 도구
- 템플릿 함수 : 템플릿에 의해  **컴파일러** 가 생성한 함수
- 템플릿 클래스 : 템플릿에 의해 **컴파일러** 가 생성한 클래스

## 함수 템플릿

### 단항템플릿으로 더하기 템플릿함수 생성
```
template<typename T>
T Plus(T _Dst, T _Src)
{
    return _Dst + _Src;
}

int main()

{

    cout << Plus<int>(10, 20) << endl; // 템플릿 함수
    cout << Plus<float>(5.3, 6.2) << endl; // 템플릿 함수
    
    return 0;

}
```
### 템플릿 특수화
특정 자료형만 예외적인 코드를 적용하도록 만든 오버로딩 문법

#### 문자열 템플릿 특수화
```
template<>
const char* Plus(const char* pDst, const char* pSrc)
{
    int iLength = (int)strlen(pDst) + (int)strlen(pSrc);
    char* pString = new char[iLength + 1];

    strcpy_s(pString, iLength + 1, pDst);
    strcat_s(pString, iLength + 1, pSrc);

    return pString;
}

template<>
char* Plus(char* pDst, char* pSrc)
{
    int	iLength = (int)strlen(pDst) + (int)strlen(pSrc);

    char* pString = new char[iLength + 1];

    strcpy_s(pString, iLength + 1, pDst);
    strcat_s(pString, iLength + 1, pSrc);

    return pString;
}

int main()

{

    cout << Plus("권", "성은") << endl;
    cout << Plus<const char*>("성은", "권") << endl;
    
    return 0;

}
```

### 다항 템플릿
다양한 자료형의 매개변수에 대응하여 유연하게 동작하게 템플릿을 만들 수 있다.

#### 다항템플릿 예시
int 자료형과 float 자료형을 더해서 double형으로 반환하는 템플릿 함수이다. 
```
template<typename T1, typename T2, typename T3>
T3 Add(T1 Dst, T2 Src)
{
    return Dst + Src;
}


int main()

{

    double dNumber = Add<int, float, double>(10, 20.1f);
    cout << dNumber << endl;
    
    return 0;

}
```

### static과 template
같은 자료형의 템플릿 끼리는 static메모리 공간을 공유한다.
아래 코드를 보면 int 형과 float형의 각각 값이 중첩되어 더해진 결과 값이 나오는 것을 볼 수 있다. 

```
template<typename T>
T	Func(T Number)
{
    static	T Test = 0; // 메모리 공간을 공유

    Test += Number;

    return Test;
}


int main()

{
     Func<int>(10); // 10
     Func<float>(1.1f); // 1.1
     
     cout << Func<int>(20) << endl; // 30
     cout << Func<float>(22.2f) << endl; // 23.3
   
    
    return 0;

}
```

### +
인라인 함수도 템플릿 함수 처럼 호출이 아니라 삽입하는 함수지만 자료형에 따른 함수들을
만들어야하는 단점이 있었다. 템플릿함수를 사용해서 이러한 단점을 해결 가능하다.


## 템플릿 클레스
클레스 템플릿은 찍어내는 코드라서 따로 분리해서 CPP에 넣을 필요가 없다. 되도록이면 중요하지 않고 공개 될 수 있는 코드를 템플릿으로 만들도록 하자.
템플릿은 상속이 가능하다.

#### 클래스 템플릿으로 템플릿 클래스를 생성

```
template<typename T> // 클래스 템플릿
class Cobj
{
public:
    Cobj() {}
    Cobj(T X, T Y) : m_iX(X), m_iY(Y) {}
    ~Cobj(){}

public:
    T Plus(T _Dst, T _Src)
    {
        return _Dst + _Src;
    }

private:
    T m_iX;
    T m_iY;

};


int main()

{
    Cobj<int> intBase(10, 20); // 템플릿 클래스
    cout << intBase.Plus(10, 20) << endl; 
    
    return 0;

}
```

### 클레스 템플릿의 특수화

```
template<>
class CBase<const char*>	
{
public:
	const char*	Plus(const char* pDst, const char* pSrc)
	{
		int	iLength = (int)strlen(pDst) + (int)strlen(pSrc);

		char* pString = new char[iLength + 1];

		strcpy_s(pString, iLength + 1, pDst);
		strcat_s(pString, iLength + 1, pSrc);

		return pString;
	}
};

```

### 부분 특수화

```
template<typename T1, typename T2>
class CTest {};

// 부분 특수화 예 1
template<>
class CTest<int, char*> {}; // 첫번째 타입이 int형이고, 두번째 타입이 char* 일 때 사용됨.

// 부분 특수화 예 2
template<typename T>
class CTest<T, char*> {}; // 첫번째 타입이 임의의 타입이고, 두번째 타입이 char* 일 때 사용됨

```

## Standard Template Library
앞으로 관리해야하는 데이터를 한곳에 모아두고 관리하게 편하게 하기 위해서라도 STL을 사용해야한다.

## 라이브러리 : 바이너리로 번역된 함수들을 모아놓은 파일
라이브러리화는 보여주지 않겠다. 함수를 제공하겠다 라는 뜻을 내포한다.

- 코드 재사용을 위한 방법 중 하나
- 다른 프로그램에서 사용할 수 있도록 운영체제, 개발자에 의해 제공
- 대다수의 함수의 정의 및 선언들을 필요로 하기 떄문에 전처리기 시점에 포함시킨다.
- 사용자의 프로그램과 링크되어 실행이 가능한 완전한 프로그램을 이루게 된다.

## STL의 구성요소

## 컨테이너 
데이터를 저장하는 객체로, 자료구조를 구현한 객체이다. 클래스 템플릿으로 설계 되어있다.

- 원소 배치 방식에 따른 구분
    1. 표준 시퀀스 컨테이너 : vector, deque, list, array, forward_list
    2. 표쥰 연관 컨테이너 : set, multiset, map, multimap
    3. 정렬하지 않는 표준연관 컨테이너 : unordered_set, unordered_multiset, unordered_map, unordered_multimap
    4. 메모리 저장 방식에 따른 구분
        - 배열 기반 컨테이너 : vector, deque, array
        - 노드 기반 컨테이너 : list, set, multiset, map, multimap, 
                              forward_list, unordered_set, unordered_multiset,
                              unordered_map, unordered_multimap
    5. 모던 c++ 추가된 컨테이너들 : array, forward_list, unordered_set, unordered_multiset, unordered_map, unordered_multimap
    6. 컨테이너 어댑터 : 기존 컨테이너의 기능 중 일부 기능만을 사용 가능하며, 기능 제한이나 기능이 변형 되어 있음
                        stack, queue, priority_queue

    7. 근사 컨테이너 : 템플릿으로서의 속성을 모두 만족 시키지 못한 컨테이너 : string, wstring

## 알고리즘 
컨테이너 안에 있는 원소들의 정렬, 삭제, 탐색 등을 해결하는 일반화된 방법을 제공하는 함수 템플릿으로,
대부분의 알고리즘은 전역함수 현태로 제공되고, 일반화 프로그래밍의 특성 상 다수 컨테이너에 대해 적용 가능하다.

## 함수객체

객체를 함수처럼 사용하는 문법으로 알고리즘의 조건자의 형태로 제공하기 위해 만든 문법이다.
'functionnal' 파일을 포함하면 만들어진 함수객체를 사용할 수 있었지만 vs2022 부터 기본으로 포함되었다.

## 반복자

컨테이너 안에 있는 원소들을 순회하는 객체로 **절대 포인터가 아닌 객체**이다.
(포인터를 이요하여 사용하는 연산자 (*, ., ->)가 오버로딩 되어있는 것)
그리고 컨테이너 마다 각각의 반복자 객체를 템플릿화 하여 가지고 있다.

## vector
벡터는 배열기반 클레스 템플릿으로 구현된 컨테이너로 탐색이 O(1)로 빠른 특징이 있다.

### 벡터 선언

```
#include <vector>


    vector<int> vecInt;
```

### push_back
벡터의 가장 뒤에 값을 삽입.

```
    vecInt.push_back(1);
    vecInt.push_back(2);
    vecInt.push_back(3);
    vecInt.push_back(4);
```

### size()와 capacity
size : 벡터안의 값의 개수 / capacity : 배열의 크기 재할당을 할경우 n + n/2 의 크기로 배열을 재할당 받는다.

```
    cout<< "size :" << vecInt.size() << "\t capacity: " << vecInt.capacity() << endl;

    vecInt.push_back(5);
    vecInt.push_back(6);

    cout << "size :" << vecInt.size() << "\t capacity: " << vecInt.capacity() << endl;
```

### Pop()
벡터안에 값을 뒤에서 부터 하나씩 삭제 하는 함수로, 값이 삭제되도 배열은 재할당하지 않는다.

```
    //늘어난 벡터는 다시 줄어드는 쪽으로 재할당 X
    vecInt.pop_back();
    vecInt.pop_back();
    vecInt.pop_back();
    cout << "size :" << vecInt.size() << "\t capacity: " << vecInt.capacity() << endl;
```
### front()
백터 안의 가장 첫번째 인덱스 값을 반환한다.

```
    cout << vecInt.front() << endl;
```

### back()
벡터 안의 가장 뒤의 인덱스 값을 반환하는 함수.

```
    cout << vecInt.back() << endl;
```


## 반복자
벡터 배열안을 순회하여 메모리에 접근하는 도구이다.

```
    vector<int>::iterator iter = vecInt.begin(); // begin()은 배열안의 가장 첫번째를 가리키는 반복자를 반환한다.

    //반복자를 통해 벡터 안을 순회하여 * 출력 연산자를 통해 iter접근한 메모리의 값을 출력한다.
    for (iter; iter != vecInt.end(); iter++)
    {
        cout << *iter << "\t";
    }
    cout << endl;

```

## clear()
벡터안의 값을 모두 지우는 함수.

```
    for (int i = 0; i < vecInt.size(); i++)
    {
        cout << vecInt[i] << endl;
        // [] 연잔자 오버로딩을 통해 배열에 접근 가능. 배열의 []연산자와 다르다.
    }
```

## erase()
벡터안의 값중 선택하여 삭제하는 함수.

```
    iter = vecInt.begin();
    for (iter; iter != vecInt.end();)
    {
    if (*iter == 2)
    {
        iter = vecInt.erase(iter); // erase()는 iterator를 인자 값으로 받아서 iter가 가리키는 값을 지우는 기능이다.
    }
        iter++;
    }
    // iter가 가리키는 값이 2 면 해당 값을 지우라고 했으니 2가 지워지고 뒤의 인덱스 값을 떙겨서 연속적인 메모리공간을 유지한다.
    for (vector<int>::iterator iter = vecInt.begin(); iter != vecInt.end(); iter++)
    {
        cout << *iter << "\t";
    }
    cout << endl;

```

### resize()
벡터의 크기를 제 조정하고 값을 0으로 초기화 한다.

```
vector<int> vecTemp;

    cout << "size :" << vecTemp.size() << "\t capacity : " << vecTemp.capacity() << endl;
    "=============================resize=================================" << endl;

    vecTemp.resize(6);

    cout << "size :" << vecTemp.size() << "\t capacity : " << vecTemp.capacity() << endl;

    for (vector<int>::iterator iter = vecTemp.begin(); iter != vecTemp.end(); iter++)
    {
        cout << *iter << endl;
    }
    cout << endl;

```

### reserve()
벡터의 메모리 공간을 예약하는 함수

```
    cout << "=============================reserve=================================" << endl;

    vecTemp.reserve(9); // 벡터의 메모리공간을 예약하는 함수

    cout << "size :" << vecTemp.size() << "\t capacity : " << vecTemp.capacity() << endl;

    for (vector<int>::iterator iter = vecTemp.begin(); iter != vecTemp.end(); iter++)
    {
        cout << *iter << endl;
    }
    cout << endl;

```

## List
리스트는 비연속적인 메모리 블럭을 연속적인 메모리공간처럼 만든 구조이다.
노드기반(값, 이전 다음 노드의 주소를 가지고있다.) 컨테이너 양방향 반복자 형태이다.
원소를 삽입과 삭제에 유리하지만 탐색은 순차 탐색을 해야하기 떄문에 O(n)으로 불리하다.

### 리스트 선언

```
#include <list>

list<int> lstInt;
```

### Push_back()
리스트의 뒤에 값을 추가하는 기능.
```

    lstInt.push_back(1);
    lstInt.push_back(2);
    lstInt.push_back(3);

```

### size()
리스으 안의 값의 개수를 반환하는 기능.

```
    //for (int i = 0; i < lstInt.size(); i++)
    //{
    //    cout << lstInt[i] << "\t"; 
    // list에는 [] 가 연산자 오버로딩이 되어있지 않기때문에 사용 불가능하다.

    //반복자를 사용해서 출력을 list의 노드에 접근하여 값을 출력한다.
     list<int>::iterator iter = lstInt.begin();
     for (iter; iter != lstInt.end(); iter++)
     {
         cout << *iter << "\t";
     }
     cout << endl;

```

### pop_back()
리스트의 가장 뒤의 값을 지우는 기능.

```
    lstInt.pop_back(); 
    lstInt.pop_back();

```


### 양방향 반복자 ++, --

```
     iter = lstInt.begin();
     for (iter; iter != lstInt.end(); iter++)
     {
         cout << *iter << "\t";
     }
     cout << endl;

     iter = lstInt.begin();
     
     iter++; // 양방향 반복자 : iter를 1증가 함으로써 다음 노로 접근한다.
     iter++;
```

### insert()
리스트 중간에 값을 삽인하는 기능
```
    lstInt.insert(iter, 5);
    //반복자가 가리키는 노드에 5라는 값을 넣었다.

```

### reverse() 리스트안의 노드를 반전 시키는 함수.

```
    lstInt.reverse(); 

```

### push_front() 
리스트 가장 앞에 값을 삽입하는 기능.

```
     list<int> lstTemp;

     lstTemp.push_front(10); // 리스트에 가장앞에 값을 삽입하는 기능.
     lstTemp.push_front(20);
     lstTemp.push_front(30);
     lstTemp.push_front(40);

```

### pop_front()
리스트 가장 앞에 값을 삭제하는 기능.

```
    lstTemp.pop_front();

```

### splice() 
반복자의 위치에 다른 리스트를 잘라서 붙이는 기능

```
     iter = lstInt.begin();
     lstInt.splice(iter,lstTemp);

     for (list<int>::iterator iter = lstInt.begin(); iter != lstInt.end(); iter++)
         cout << *iter << "\t";

     cout << endl;

     // 먼저 선언한 리스트에 반복자 위치를 가장 앞으로 초기화하고
     // 나중에 선언한 리스트를 splice의 매개변수로 사용함으로써
     // 반복자 위치에 Temp리스트 전체를 삽입하였다.

```

### sort()
정렬알고리즘은 배열기반으로 되어 있기 때문에 리스트는 sort를 따로 가지고있다.

```
    lstInt.sort();
    for (list<int>::iterator iter = lstInt.begin(); iter != lstInt.end(); iter++)
            cout << *iter << "\t";

```

## map

```

```