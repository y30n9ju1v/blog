---
title: "[C++] 타입 캐스팅"
date: 2022-07-23T11:12:17+09:00
categories: [
    "C++",
]
---

## 작성중

~~~c++
#include <iostream>

using std::cout;
using std::endl;
using std::string;

class Animal {
public:
     virtual ~Animal() {}
};

class Dog : public Animal {
public:
    int age = 10;
};

class Cat : public Animal {
public:
    string name = "Cat";
};

int main()
{
    //  1) static_cast
    //    : 다른 타입 간의 변환에 사용됩니다.
    //      연관성 있는 변환만 허용됩니다.
    int* p = static_cast<int*>(malloc(sizeof(int)));
    *p = 10;
    cout << *p << endl;

    int n = 0x12345678;
    // char* p2 = static_cast<char*>(&n); // error!

    //  2) reinterpret_cast
    //    : 메모리 재해석 목적
    char* p2 = reinterpret_cast<char*>(&n);
    printf("%x %x %x %x\n", p2[0], p2[1], p2[2], p2[3]);

    const int i = 100;

    // int* p3 = static_cast<int*>(&i); // error!
    // int* p3 = reinterpret_cast<int*>(&i); // error!

    //  3) const_cast
    //    : 상수성을 제거하는 목적으로 사용합니다.
    //     - 타입의 불일치 문제를 해결하기 위해 사용합니다.
    int* p3 = const_cast<int*>(&i);
    *p3 = 200;
    cout << *p3 << endl;

    Animal* a = new Cat; //new Dog;

    //  4) dynamic_cast
    //    가상 함수 테이블이 없으면 사용할 수 없습니다.
    //   : RTTI(Run Time Type Information)
    Cat* c = dynamic_cast<Cat*>(a);
    if (c) {
        cout << c->name << endl;
    }

    return 0;
}
~~~