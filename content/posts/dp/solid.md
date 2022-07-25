---
title: "SOLID"
date: 2022-07-25T19:05:50+09:00
categories: [
    "Design Pattern",
]
---

# 객체 지향 디자인 5대 원칙 (SOLID)

## 1) SRP(Single Reponsibility Principle, 단일 책임의 원칙)
* 프로그램의 모든 클래스, 모듈 또는 함수는 프로그램에서 하나의 책임/목적을 가져야 한다.

## 2) OCP(Open Close Principle, 개방 폐쇄의 원칙)
* 기존의 코드를 변경하지 않고(Closed) 기능을 수정하거나 추가할 수 있도록(Open) 설계해야 한다.

## 3) LSP(Liskov Substitution Principle, 리스코프 치환 원칙)
* 자식의 공통된 기능은 부모로부터 비롯되어야 한다.

## 4) ISP(Interface Segregation Principle, 인터페이스 분리 원칙)
* 범용 인터페이스보다는 세분화된 인터페이스가 좋다.

## 5) DIP(Dependency Inversion Principle, 의존 관계 역전 원칙)
* 의존 관계를 맺을 때, 변화하기 쉬운것 보단 변화하기 어려운 것에 의존해야 한다는 원칙이다.
* 즉, 구체적인 타입을 직접 이용하는 것이 아니라 추상 개념에 의존해야 한다.