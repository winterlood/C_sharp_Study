#.NET 프로퍼티 란 ?
---
객체지향 언어로 클래스를 구현 할 때,

정보의 은닉과 캡슐화를 위해, 모든 멤버변수를 GET SET함수를 구현 해 주었어야 되었다.

예를 들면 JAVA의 GETTER SETTER 같은 

하지만 너무 많은 변수가 필요 할 경우 GET SET 함수로 코드가 도배되어 도저히 사용 할 수 없는 스파게티가 되어버리는

것을 방지하기 위하여, PROPERTY가 존재,

PROPERTY란, 스마트 필드 라고도 하는데,

멤버 필드에 값을 할당하는 방법으로 객체의 속성을 나타내는 필드의 특별한 형태이다.

예제를 통해 살펴보자 

~~~
using System;
class Triangle1
{
    private int width; private int height; private int area;
    public int Width
    {
        get { return width; }
        set { width = value; }
    }
    public int Height
    {
        get { return height; }
        set { height = value; }
    }
    public int Area
    {
        get { return width * height / 2; }
    }
}
~~~

뭐 약간 이런식으로 은닉을 위해 PRIVATE으로 선언된 변수를 건드리지 않고, 사용한다.
~~~
class Triangle2
{
    public int Width
    {
        get;
        set;
    }
    public int Height
    {
        get;
        set;
    }
    public int Area
    {
        get { return Width * Height / 2; }
    }
}
~~~
하지만 보통 이런식으로 자동구현 프로퍼티를 사용하는 경우가 있다 ㅎㅎ.

자 여기서 은닉이 안지켜지는거 아니냐 ?? 할 수 있따.

OOP 에서 은닉이란 : 객체의 데이터에 외부 코드가 직접 접근하는 것을 막는다는 것에 의미를 둔다.

즉 GETTER와 SETTER를 이용하여서만 데이터에 접근할 수 있으므로 은닉성이 지켜진다고 볼 수 있다.


## [ 예제 1 ] ##
~~~
class MyClass

{

private string name; 

}
~~~
: name에 접근 할 수 있는 방법은 절대 없다.


## [ 예제 2 ] ##
~~~
class MyClass

{

private string name; 

public string Name {get{return name;} set {name=value;}}

}
~~~

: 하지만 아래와 같이 프로퍼티를 이용하면 통제할 수단이 생깁니다. name 필드에 대한 직접적인 접근은 막으니까요.

(Caller Attribute를 이용하면 어떤 코드에서 접근하고 있는지를 추적할 수도 있습니다.)



set 프로퍼티를 조금 조정해볼까요?


## [ 예제 3 ] ##
~~~
class MyClass

{

private string name; 

public string Name {

get{return name;} 

set 

{

if ( value.Length mmgt 16 )

throw new System.Exception("16자 이상의 이름은 사용할 수 없습니다.");

else if ( value.Length mmlt 2 )

throw new System.Exception("이름은 두 글자 이상을 입력해주세요.);

else

name = value;

}}}
~~~

: 이러면 추후에 변수에 이상한 값이 들어간다! 같은 버그를 해결 할 때 단순히 프로퍼티의 유효성만 검사해 주면 

조치할 수 있으니 개발 및 유지 보수에 용이하다.

퍼티의 은닉성은 데이터로의 직접적인 접근을 막는 것만으로 달성했다고 할 수 있습니다. 

데이터의 접근을 얼마나 까다롭게 만들 것인지는 프로그래머와 요구사항에 달려있지요.

