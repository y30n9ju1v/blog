---
title: "[C++] This call"
date: 2022-07-23T08:41:21+09:00
categories: [
    "C++",
]
---

## 작성중 ##

~~~c++
#include <iostream>

using std::cout;
using std::endl;

class Point {
	int x, y;
public:
	// void set(Point* const this, int a, int b)
	void set(int a, int b)
	{	
		x = a;  // this->x = a;
		y = b;  // this->y = b;
	}	

    void get() const
    {
        cout << "x : " << x << ", y : " << y << endl;
    }

	// 정적 멤버 함수: 객체를 생성하지 않아도 호출이 가능합니다.
	// this가 전달되지 않습니다.
	static void foo(int a)
	{
        // this->x = a; 가 되어야 하는데, this가 없기 때문에 컴파일 에러 발생
		// x = a;   
	}
};

int main()
{
	Point p1, p2;

	p1.set(10, 20);  // Point::set(&p1, 10, 20)
    p1.get();
	p2.set(30, 40);  // Point::set(&p2, 10, 20)
    p2.get();

    return 0;
}
~~~

~~~c++
#include <iostream>

using std::cout;
using std::endl;

class Sample {
	int data;
public:
	// void f1(Sample* const this) {}
	void f1()
    {
        cout << "f1" << endl;
    }

	// C++ 표준에서는 널 객체에 대한 함수 호출은 미정의 동작입니다.
	static int safe_f2_2(Sample* const self) 
	{
		if (self)
			return self->f2();
		return 0;
	}

	int safe_f2()
	{
		if (this)
			return f2();

		return 0;
	}

private:
	int f2()
    {
        cout << "f2" << endl;
        return data; // this->data;
    }
};

int main()
{
	Sample* p = nullptr;

	p->f1(); // Sample::f1(p) / Sample::f1(nullptr)

	cout << p->safe_f2(p) << endl;
	cout << Sample::safe_f2_2(p) << endl;

    return 0;
}
~~~


~~~c++
#include <iostream>

using std::cout;
using std::endl;

class Dialog {
public:
    // void open(Dialog* const this)
    void open() {
        cout << "Dialog open" << endl;
    }

    static void close()
    {
        cout << "Dialog close" << endl;
    }
};

int main()
{
    // 정적 멤버 함수는 일반 함수와 시그니처가 동일합니다.
    void (*fp)() = &Dialog::close;
    // 일반 함수 포인터를 통해 정적 멤버 함수를 호출할 수 있습니다.
    fp();

    // 1. 멤버 함수 포인터 타입을 만드는 방법
    void (Dialog::*fp2)();

    // 2. 멤버 함수의 주소를 얻는 방법
    fp2 = &Dialog::open;

    // 3. 멤버 함수 포인터를 통해 멤버 함수를 호출하기 위해서는 반드시 객체가 필요합니다.
    Dialog dlg;
    (dlg.*fp2)();

    Dialog* pDlg = &dlg;
    (pDlg->*fp2)();

    return 0;
}
~~~

~~~c++
#include <iostream>

using std::cout;
using std::endl;

class Test {
public:
    // 아래 멤버 함수를 통해서 내부의 값이 변경되지 않는다는 것을 보장합니다.
    // void print(const Test* const this)
    void print() const
    {
        cout << "call print() const" << endl;
    }

    void print()
    {
        cout << "call print()" << endl;
    }
};

int main()
{
    Test t1;
    t1.print();

    // 상수 객체는 상수 멤버 함수만 호출이 가능합니다.
    const Test t2;
    t2.print();

    return 0;
}
~~~