---
title: "[C++] 다형성"
date: 2022-07-23T10:21:45+09:00
categories: [
    "C++",
]
---

## 작성중 

~~~c++
#include <iostream>

class Animal { };

class Dog : public Animal { };

// 1. Upcasting
// 2. is-a
//     자식 클래스 is a 부모 클래스
// 3. Upcasting은 public 상속에서만 허용됩니다.
int main()
{
    Dog d;

    // 부모의 포인터 타입을 통해 자식 객체의 주소를 담을 수 있습니다.
    Animal* p = &d;

    // 부모의 포인터 타입을 자식의 포인터 타입으로의 암묵적인 변환을 허용하지 않습니다.
    Dog* d2 = p;

    // 명시적인 캐스팅이 필요합니다.
    Dog* d3 = static_cast<Dog*>(p);

    return 0;
}
~~~

~~~c++
#include <iostream>
#include <vector>

using std::cout;
using std::endl;
using std::vector;

class Animal {
public:
    int getAge() const { return 10; }
};

class Dog : public Animal {};
class Cat : public Animal {};

// 1. 동종을 처리하는 함수를 만들 수 있습니다.
int GetAge(Animal* p)
{
    return p->getAge();
}

int main()
{
    // 2. 동종을 보관하는 컨테이너를 사용할 수 있습니다.
    vector<Animal*> animals;

    Dog d; Cat c;
    cout << GetAge(&d) << endl;
    cout << GetAge(&c) << endl;

    return 0;
}
~~~

~~~c++
#include <iostream>

using std::cout;
using std::endl;

class Animal {
public:
    virtual void go() { cout << "Animal go" << endl; }
};

class Dog : public Animal {
public:
    // 부모가 제공하는 멤버 함수를 자식 클래스가 재정의할 수 있습니다.
    // : 함수 오버라이딩
    void go() override
    {
        cout << "Dog go" << endl;
    }
};

// 1) 정적 바인딩(static binding)
//  : 컴파일러가 p의 타입을 보고, 컴파일 타임에 결정하는 것
//  => 컴파일러가 결정하기 때문에, 인라인화가 가능하기 때문에 빠릅니다.
//
// 2) 동적 바인딩(dynamic binding)
//  : 컴파일러가 p가 실행시간에 어떤 변수의 타입을 가지고 있는지 조사하는 코드를 삽입하고,
//    실행시간에 변수의 타입에 기반해서 함수를 호출하는 것
//  => 인라인화가 불가능하기 때문에, 상대적으로 호출이 느립니다.

int main()
{
    Animal a; Dog d;
    Animal* p = &a;
    p->go();

    p = &d;
    p->go();

    return 0;
}
~~~

~~~c++
#include <iostream>

using std::cout;
using std::endl;

class Animal {
public:
    Animal() { cout << "Animal()" << endl; }

    // 부모 클래스는 반드시 가상 소멸자가 제공되어야 합니다.
    virtual ~Animal() { cout << "~Animal()" << endl; }
};

class Dog : public Animal {
public:
    Dog() { cout << "Dog()" << endl; }
    ~Dog() { cout << "~Dog()" << endl; }
};

// 1. 부모의 포인터를 통해 자식의 소멸자가 제대로 호출되지 않는 문제가 발생합니다.
//   > 소멸자가 정적 바인딩을 하기 때문에 발생하는 이슈 입니다.
// 2. 소멸자도 동적 바인딩 기반으로 호출되어야 합니다.
//   > 가상 소멸자
// 3. 부모의 소멸자가 가상이면, 자식의 소멸자도 가상입니다.

int main()
{
    Animal* p = new Dog;
    delete p;

    return 0;
}
~~~