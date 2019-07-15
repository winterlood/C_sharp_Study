# INTERFACE
---

### 서론
객체 지향의 꽃은 인터페이스 아니겠습니까 ?
중수 -> 고수로 넘어가기 위한 장벽쓰 ㅎㅎ

### 인터페이스가 무엇이냐 ?


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

public string name; 

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

