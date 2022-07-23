---
title: "[C++] Online Formatter"
date: 2022-07-23T12:18:26+09:00
categories: [
    "C++",
]
---

https://formatter.org/cpp-formatter

앞으로 블로그에 올라가는 C++ 코드의 코딩 스타일은 위 싸이트를 이용하여 변환 후 올리려고 합니다.

* Coding Style = google
* Indent Width = 4
* Column Limit = 80

## before
~~~c++
#include<iostream>

using namespace std;

class CodesCracker
{
    public:
        void printHello();
};

void CodesCracker::printHello()
{
    cout<<"Hello, World!";
}

int main()
{
    CodesCracker c;
    c.printHello();
    cout<<endl;
    
    return 0;
}
~~~

## after
~~~c++
#include <iostream>

using namespace std;

class CodesCracker {
   public:
    void printHello();
};

void CodesCracker::printHello() { cout << "Hello, World!"; }

int main() {
    CodesCracker c;
    c.printHello();
    cout << endl;

    return 0;
}
~~~
