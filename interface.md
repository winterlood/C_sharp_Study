# INTERFACE

### 서론
객체 지향의 꽃은 인터페이스 아니겠습니까 ?
중수 -> 고수로 넘어가기 위한 장벽쓰 ㅎㅎ

### 인터페이스가 무엇이냐 ? 

## [예제 1] ##
~~~
interface [이름]
{
//인터페이스의 포함 요소는 다음과 같다
    메소드...
    이벤트...
    인덱서...
    프로퍼티...
}
~~~
여기서 **인덱서** 가 뭐죠 ? .. 라고 할 수 있는데.

**[인덱서](./indexer.md)** 를 참조하길 바람.

클래스의 한 종류로써

다음과 같은 형식으로 구현은 없는 그냥 정의만 있는 클래스를 interface라고 한다.

즉 뼈대만 가진 클래스 라는것이다.

## [예제 2] ##
~~~
public interface StringList
{
void Add(string s); // 메소드
int Count{get; set;} // 프로퍼티
event StringListEvent changed; // 이벤트
string this[int index]{get; set;} // 인덱서
}
~~~

특정 interface를 상속받는 class는 

해당 interface의 **모든 메소드 들을 구현해야 한다.**

또한 이것은 객체를 생성할 수 없다... 

그럼 어떻게 쓰라는거지 ?? 구현도 없고.. 객체도 못만들고 .. ?

정답 : 인터페이스는 해당 인터페이스를 참조하는 **파생클래스로부터 객체를 생성하여 사용할 수 있다.**


**[ 인터페이스 메소드 사용 예제 ]**
~~~
using System;

namespace ConsoleApp1
{
    class Program : abc
    {
        static void Main(string[] args)
        {
            Program pr = new Program();
            abc dd = pr;
            dd.hi();
        }
        void abc.hi()
        {
            Console.WriteLine("Hi in abc");
        }
    }

    public interface abc
    {
      void hi();
    }
}
~~~

: 요런 느낌으로 abc interface의 hi라는 메소드를 

파생클래스인 Program의 클래스로 인스턴스화 하여, hi 메소드를 구현하고 사용하였다.

### 다중 상속

백문이 불여일견.

거두 절미 하고 코드를 보자.

~~~
using System;

namespace ConsoleApp1
{
    class Program : abc, bcd
    {
        static void Main(string[] args)
        {
            Program pr = new Program();
            abc dd = pr;
            dd.hi();
            bcd bc = pr;
            bc.hello();
        }
        void abc.hi()
        {
            Console.WriteLine("Hi in abc");
        }
        void bcd.hello()
        {
            Console.WriteLine("Hello in bcd");
        }
    }

    interface bcd
    {
        void hello();
    }

     interface abc
    {
      void hi();
    }
}
~~~

다음과 같이 abc와 bcd interface를 Class Program에서 다중으로 상속 받을 수 있다.

물론 동일하게 bcd도 상속받았다면 **bcd의 모든 method를 구현해야 한다.**

(물론 사용은 안해도 무관)


### 다단계 상속

역시 코드로 보자.

~~~
using System;

namespace ConsoleApp1
{
    class Program : abc
    {
        static void Main(string[] args)
        {
            Program pr = new Program();
            abc dd = pr;
            dd.hi();
            dd.hello();
        }
        void abc.hi()
        {
            Console.WriteLine("Hi in abc");
        }
        void bcd.hello()
        {
            Console.WriteLine("Hello in bcd");
        }
    }

    interface bcd
    {
        void hello();
    }

     interface abc : bcd
    {
      void hi();
    }
}
~~~

: 차이점이 보이는가 ?

abc가 bcd를 상속하며, program에서는 abc의 인스턴스로 bcd의 메소드 까지 호출 가능 하지만,

구현은 bcd.hello() 이런 식으로 해줘야 한다.

