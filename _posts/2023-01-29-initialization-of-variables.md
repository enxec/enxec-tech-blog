---
title: "[Java] 변수의 초기화"
description: 
author: Enxec
date: 2023-01-29
categories: [Language, Java]
tags: [java, 자바, variable, 변수]
pin: false
math: true
mermaid: true
image:
  path: /thumbnail/java-logo.png
  lqip: 
  alt: 
---

저번 변수 포스팅에서 변수의 초기화를 간략히 짚고넘어간적이 있는데, 이번 포스팅에서는 좀 더 자세히 변수의 초기화에 대해 다루어보고자 한다.

## 변수의 초기화
---
변수를 선언하고 처음으로 값을 저장하는 것을 '변수의 초기화' 라고 한다. 변수의 초기화는 경우에 따라서 필수적이기도 하고 선택적이기도 하지만, 가능하면 선언과 동시에 적절한 값으로 초기화하는 것이 바람직하다.

멤버변수는 초기화를 하지 않아도 자옫적으로 변수의 자료형에 맞는 기본값으로 초기화가 이루어지므로 초기화하지 않고 사용해도 되지만, __지역변수는 사용하기 전에 반드시 초기화해야 한다.__

```java
class Om {
  int x;
  int y = x;

  void method() {
    int i;
    int j = i;
  }
}
```

위의 코드에서 x, y는 인스턴스 변수이고 i와 j는 지역변수이다. 그 중 x와 i는 선언만 하고 초기화를 하지 않았다. 그리고 y를 초기화 하는데 x를 사용하였고, j를 초기화하는데 i를 사용하였다.

인스턴스 변수 x는 초기화를 해주지 않아도 자동적으로 int형의 기본값인 0으로 초기화되므로, 'int y = x;'와 같이 할 수 있다. x의 값이 0이므로 y역시 0이 저장된다.

하지만, method()의 지역변수 i는 자동적으로 초기화되지 않으므로 초기화 되지 않은 상태에서 변수 j를 초기화 하는데 사용될 수 없다. 컴파일하면, 에러가 발생한다.

__알아두기__  
각 타입의 기본값은 다음과 같다.

|자료형|기본값|
|:---:|:---:|
|boolean|false|
|char|'\u0000'|
|byte, short, int|0|
|long|0L|
|float|0.0f|
|double|0.0d 또는 0.0|
|참조형 변수|null|

<br>
<br>

변수의 초기화에 대한 예를 몇 가지 더 살펴보자.

```java
int i = 10;             // int형 변수 i를 선언하고 10으로 초기화 한다.
int j = 10;             // int형 변수 j를 선언하고 10으로 초기화 한다.

int i = 10, j = 10;     // 같은 타입의 변수는 콤마(,)를 사용해서 함께 선언하거나 초기화 할 수 있다.

int i = 10, long j = 0; // 에러. 타입이 다른 변수는 함께 선언하거나 초기화할 수 없다.

int i = 10;             // 변수 i에 저장된 값으로 변수 j를 초기화 한다.
int j = i;              // 변수 j는 i의 값인 10으로 초기화 된다.

int j = i;              // 에러. 변수 i가 선언되기 전에 i를 사용할 수 없다.
int i = 10;
```

멤버변수의 초기화는 지역변수와 달리 여러 가지 방법이 있는데 앞으로 멤버변수의 초기화에 대한 모든 방법에 대해 비교, 정리할 것이다.

>멤버변수의 초기화 방법
>1. 명시적 초기화
>2. 생성자
>3. 초기화 블럭
> - 인스턴스 초기화 블럭 : 인스턴스변수를 초기화하는데 사용.
> - 클래스 초기화 블럭 : 클래스변수를 초기화하는데 사용.

<br>

## 명시적 초기화
---
변수를 선언과 동시에 초기화하는 것을 명시적 초기화라고 한다. 가장 기본적이면서도 간단한 초기화 방법이므로 여러 초기화 방법 중에서 가장 우선적으로 고려되어야 한다.

```java
class Car {
  int door = 4;             // 기본형 변수의 초기화
  Engine e = new Engine();  // 참조형 변수의 초기화
}
```

명시적 초기화가 간단하고 명료하긴 하지만, 보다 복잡한 초기화 작업이 필요할 때는 '초기화 블럭' 또는 생성자를 사용해야 한다.

<br>

## 초기화 블럭
---
초기화 블럭에는 '클래스 초기화 블럭'과 '인스턴스 초기화 블럭' 두 가지 종류가 있다. 클래스 초기화 블럭은 클래스변수의 초기화에 사용되고, 인스턴스 초기화 블럭은 인스턴스 변수의 초기화에 사용된다.

>__클래스 초기화 블럭__
> - 클래스변수의 복잡한 초기화에 사용된다.
> 
>__인스턴스 초기화 블럭__
> - 인스턴스변수의 복잡한 초기화에 사용된다.

초기화 블럭을 작성하려면, 인스턴스 초기화 블럭은 단순히 클래스 내에 블럭{}을 만들고 그 안에 코드를 작성하기만 하면 된다. 그리고 클래스 초기화 블럭은 인스턴스 초기화 블럭 앞에 단순히 static을 덧붙이기만 하면 된다.

초기화 블럭 내에는 메서드 내에서와 같이 조건문, 반복문, 예외처리구문 등을 자유롭게 사용할 수 있으므로, 초기화 작업이 복잡하여 명시적 초기화만으로는 부족한 경우 초기화 블럭을 사용한다.

```java
class Om {
  static {
    /* 클래스 초기화블럭입니다. */
  }

  {
    /* 인스턴스 초기화블럭입니다. */
  }
}
```

클래스 초기화 블럭은 클래스가 메모리에 처음 로딩될 때 한번만 수행되며, 인스턴스 초기화 블럭은 생성자와 같이 인스턴스를 생성할 때 마다 수행된다.

그리고 생성자 보다 인스턴스 초기화 블럭이 먼저 수행된다는 사실도 기억해두자.

__참고__  
클래스가 처음 로딩될 때 클래스변수들이 자동적으로 메모리에 만들어지고, 곧바로 클래스 초기화블럭이 클래스변수들을 초기화하게 되는 것이다.

인스턴스 변수의 초기화는 주로 생성자를 사용하고, 인스턴스 초기화 블럭은 모든 생성자에서 공통으로 수행되어야 하는 코드를 넣는데 사용한다.

```java
Car() {
  count++;                // 같은 코드 중복
  serialNo = count;       // 같은 코드 중복
  color = "White";
  gearType = "Auto";
}

Car(String color, String gearType) {
  count++;                // 같은 코드 중복
  serialNo = count;       // 같은 코드 중복
  this.color = color;
  this.gearType = gearType;
}
```

예를 들면, 위와 같이 클래스의 모든 생성자에 공통으로 수행되어야 하는 문장들이 있을 때, 이 문장들을 각 생성자마다 써주기 보다는 아래와 같이 인스턴스 블럭에 넣어주면 코드가 보다 간결해진다.

```java
{
  count++;            
  serialNo = count;
}

Car() {
  color = "White";
  gearType = "Auto";
}

Car(String color, String gearType) {
  this.color = color;
  this.gearType = gearType
}
```

이처럼 코드의 중복을 제거하는 것은 코드의 신뢰성을 높여주고, 오류의 발생가능성을 줄여 준다는 장점이 있다. 즉, 재사용성을 높이고 중복을 제거하는 것, 이것이 바로 객체지향프로그래밍이 추구하는 궁극적인 목표이다.

프로그래머는 이와 같은 객체지향언어의 요소들을 잘 이해하고 활용하여 코드의 중복을 최대한 제거하기 위해서 노력해야한다.

<br>

## 멤버변수의 초기화 시기와 순서
---
지금까지 멤버변수를 초기화하는 방법에 대해 알아보았다. 이번엔 초기화가 수행되는 시기와 순서에 대해서 정리해보도록 하자.

>__클래스변수의 초기화 시점__
> - 클래스가 처음 로딩될 때 단 한번 초기화 된다.
>
>__인스턴스변수의 초기화시점__
> - 인스턴스가 생성될 때마다 각 인스턴스별로 초기화가 이루어진다.
>
>__클래스변수의 초기화순서__
> - 기본값 -> 명시적초기화 -> 클래스 초기화 블럭
>
>__인스턴스변수의 초기화순서__
> - 기본값 -> 명시적초기화 -> 인스턴스 초기화 블럭 -> 생성자

프로그램 실행도중 클래스에 대한 정보가 요구될 떄, 클래스는 메모리에 로딩된다. 예를 들면, 클래스 멤버를 사용했을 때, 인스턴스를 생성할 때 등이 이에 해당한다.  
하지만, 해당 클래스가 이미 메모리에 로딩되어 있다면, 또다시 로딩하지 않는다. 물론 초기화도 다시 수행되지 않는다.

__참고__  
클래스의 로딩시기는 JVM의 종류에 따라 좀 다를 수 있는데, 클래스가 필요할 때 바로 메모리에 로딩하도록 설계가 되어있는 것도 있고, 실행효율을 높이기 위해서 사용될 클래스들을 프로그램이 시작될 때 미리 로딩하도록 되어있는 것도 있다.

```java
class Om {
  static int cv = 1;    // 명시적 초기화
  int iv = 1;           // 명시적 초기화

  // 클래스 초기화 블럭
  static {
    cv = 2;
  }

  // 인스턴스 초기화 블럭
  {
    iv = 2;
  }

  // 생성자
  Om() {
    iv = 3;
  }
}
```

위의 Om클래스는 클래스변수(cv)와 인스턴스변수(iv)를 각각 하나씩 가지고 있다. 'new Om();'과 같이 하여 인스턴스를 생성했을 때, 클래스 변수와 인스턴스 변수가 초기화되어가는 과정을 단계별로 살펴보면 다음과 같다.

![EMP 릴레이션](/posts/20230221/variable-init.png "멤버변수 초기화 과정"){: width="100%"}
<div style="color: gray; text-align: center; margin-bottom: 30px;">멤버변수 초기화 과정</div>

>__클래스변수 초기화(1~3)__
> - 클래스가 처음 메모리에 로딩될 때 차례대로 수행됨.
> 
>__인스턴스변수 초기화(4~7)__
> - 인스턴스를 생성할 때 차례대로 수행됨

\* 클래스 변수는 항상 인스턴스변수보다 먼저 생성되고 초기화 된다.

1. cv가 메모리(method area)에 생성되고, cv에는 int형의 기본값인 0이 cv에 저장된다.
2. 명시적 초기화에 의해서 cv에 1이 저장된다.
3. 클래스 초기화 블럭이 수행되어 cv에는 2가 저장된다.
4. Om클래스의 인스턴스가 생성되면서 iv가 메모리(heap)에 존재하게 된다. iv 역시 int형 변수이므로 기본값 0이 저장된다.
5. 명시적 초기화에 의해서 iv에 1이 저장된다.
6. 인스턴스 초기화 블럭이 수행되어 iv에 2가 저장된다.
7. 생성자가 수행되어 iv에는 3이 저장된다.

---

읽어주셔서 감사합니다. 😊 

__Reference__  
자바의 정석 - 남궁성  