# Delegate with CollBack Method &Lamda

## Delegate 

Delegate 는 한국말로 "대리인" 이라는 뜻으로,

메소드를 참조하는 변수이다.

특정 메소드를 대리하여, 결과를 반환하는 변수라고 보면 된다.

즉 특정 메소드를 처리할 때, 그 메소드를 직접 호출하여 처리해야 했다면 (지금 까지는)

이제부터는 Delegate를 이용하여 대리자로써 역할을 수행 시킬 것 이다.

### 1. 선언

Delegate로 특정 메소드를 대리하기 위해서는 

해당 메소드와 동일한 타입을 가져야 한다.

예를들어 
~~~
delegate void typeA(void) // void funcA(void)

delegate int typeB(int) // int funcB(int)
~~~
이런식으로 동일한 타입을 가져야 대리할 수 있게 된다.

메소드의 타입은 파라미터와 리턴타입에 의존적이므로, 

Delegate타입도 똑같이 대리할 메소드의 타입와 일치시켜야 한다.

자 그럼 어떻게 써먹느냐 ?!

### 2. 사용

~~~
using System;
namespace ConsoleApp1
{
    delegate int Mydel(int a, int b);
    class Program
    {
        public static int Plus(int a, int b) => a + b;
        public static int Minus(int a, int b) => (a > b) ? a - b : b - a;
        static void Main(string[] args)
        {
            Mydel delA = new Mydel(Plus);
            int sum = delA(1, 2);
            delA = new Mydel(Minus);
            int min = delA(1, 2);
            Console.WriteLine("A :  {0} , B : {1}", sum, min);
        }
    }
}
~~~
자 이런식으로 Plus와 Minus를 각각 대리하여 사용하도록 하였다.


### 3. Call Back Method

Delegate의 진가는 이제부터 시작이다.

여러분이 덧셈과 뺄셈 곱셈기능을 해야하는 계산기를 만든다고 하자.

각각 덧셈과 뺄셈과 곱셈기능을 하는 함수를 구현하고, 

덧셈을 원하는지 뺄셈을 원하는지 곱셈을 원하는지 판별하여 해당 기능에 맞는 메소드를 호출해줘야 하는데,

이게 얼마나 귀찮은 일인가 .. ?

자 여기서 Call Back 메서드 설명 들어가도록 하자.

**Call Back Method** ?!

A라는 메소드를 호출 할 때, B라는 메소드를 파라미터로 넘겨주어,

A로 하여금 B를 호출하여 원하는 결과를 얻게 하는 것이다

예제를 통해 무슨말인지 다시 알아보자.

~~~
using System;

namespace ConsoleApp1
{
    delegate int Mydel(int a, int b);
    class Program
    {
        public static int Plus(int a, int b) => a + b;
        public static int Minus(int a, int b) => (a > b) ? a - b : b - a;
        public static int Product(int a, int b) => a * b;
        public static void Print(int a, int b, Mydel del)
            => Console.WriteLine("result is : {0}", del(a, b));
        static void Main(string[] args)
        {
            Mydel delA = new Mydel(Plus);
            Print(1, 2, delA);
            delA = new Mydel(Minus);
            Print(1, 2, delA);
            delA = new Mydel(Product);
            Print(1, 2, delA);
        }
    }
}
~~~

뭐 대충 이런식으로 쓸 수 있따는 놀라운 점 .. 와우

다시 설명하자면 Print라는 메소드는 del이라는 메소드를 넘겨 받아,

실행시킨 결과값을 통해 출력을 하고 있다. 이게바로 콜백 메서드이다.


### 4. Normalization Delegate

Delegate의 일반화 이다.

무슨말이냐면 아, 솔직히 반환타입 쓰기도 귀찮고 매개변수 쓰기도 귀찮다 그냥 delegate 객체 하나 선언하고 쓸란다!!

할 때 쓸 수 있는것으로,

~~~
using System;

namespace ConsoleApp1
{
    delegate T Mydel<T> (T a , T b);
    class Program
    {
        public static int Plus(int a, int b) => a + b;
        public static int Minus(int a, int b) => (a > b) ? a - b : b - a;
        public static int Product(int a, int b) => a * b;

        public static float FPlus(float a, float b) => a + b;
        public static void Print<T>(T a, T b, Mydel<T> del)
            => Console.WriteLine("result is : {0}", del(a,b));
        static void Main(string[] args)
        {
            Mydel<int> delA = new Mydel<int>(Plus);
            Print(1, 2, delA);
             delA = new Mydel<int>(Minus);
            Print(1, 2, delA);
            Mydel<float> delF = new Mydel<float>(FPlus);
            Print(1.0f, 2.4f, delF);
        }
    }
}
~~~
머 .. 이런식으로 템플릿 조차도 대리하여 사용할 수 있따..

### 4. Delegate Chain

지금까지는 하나의 delegate에 하나의 method만을 참조하였다.

하지만 chain을 이용하여,  하나의 delegate에 여러가지의 메소드를 참조 시킬 수 있다.

~~~
MyDelegate del;
del = new Mydel(func0);
del += func1;
del += func2;
// del에 func0,1,2가 순서대로 들어가 있음
del -= func0;
// del에 func1,2가 존재
~~~

자 이렇게! del이라는 대리자 변수에 func1과 func2를 추가하고 func0을 빼는 등 chain을 통해 여러가지의 메소드를 연결해 이용 할 수 있다.

~~~
using System;

namespace ConsoleApp1
{
    delegate void Mydel();
    class Program
    {
        public static void func0() => Console.Write("Func0");
        public static void func1() => Console.Write("Func1");
        public static void func2() => Console.Write("Func2");
        static void Main(string[] args)
        {
            Mydel del = new Mydel (func0);
            del();
            Console.WriteLine();
            del += func1;
            del();
            Console.WriteLine();
            del += func2;
            del();
            Console.WriteLine();
            del-=func1;
            del();
            Console.WriteLine();
        }
    }
}
~~~

실전 예제이다.
