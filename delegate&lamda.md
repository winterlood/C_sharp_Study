# Delegate with CollBack Method &Lamda

## Lamda Expression 

람다식!! 굉장히 엄청난 녀석이다 이녀석을 알게된 후로는 코딩이 매우 편하고 재미있어 질 것이다.

함수의 구현을 단순히 계산식으로 표현해 낸 것이다.


**[예제 1]**
~~~
void func ()
{
    console.wirte("하하");
}
~~~
다음 예제는 지금까지 우리가 정의해왔고 구현해왔던 함수의 방식이다.


**[예제 2]**
~~~
void func() => console.write("하하");
~~~
이렇게 계산식처럼 간결하게 표현하는 것이 바로 람다식 이다.

그냥 구현부를 화살표로 표시해 준 것.

일단은 여기까지만 알아보도록 하자.


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

### 5. Func, Action Delegate

프로그램을 작성 하던 도중 갑작스레 무명 메소드가 필요해진 상황이 존재 할 것이다.

허나 무명 메소드를 사용하기 위해서는 delegate 변수가 있어야 하며,

변수를 만들기 위해 delgate type도 선언 해야 한다.

각기 다른 타입의 무명 메소드를 과연 효율적으로 어떻게 만들까 ??

- 무식하게 : 모든 타입의 delegate를 만들어 버리자!

아 매우 골치아픈 일이며, 유지보수 또한 어렵다.

- 똑똑하게: Func, Action 변수를 사용한다.


정답은 **똑똑하게** 이다.

#### 5-1. Func Delegate

Func는 C#에서 제공하는 Default Delegate 변수이다.

return value가 있는 method를 참조하는 변수로써, 

.NET FRAMEWORK 상에는 총 17개의 DELEGATE가 존재한다.

즉 매개변수가 0개 부터 16개 까지 모두 지원한다는 뜻!

다음과 같은 문법으로 사용한다.

~~~
Func <float> func0 = () => 0.1f;
// 0.1f를 반환
// 매개변수는 없다. 반환값은 float 형

Func <int, float> func0 = (a) => a * 0.1f;
// 매개변수는 int형 a이다. 반환값은 float 형.

Func <int,int,float> func0 = (a,b) => (a+b)*0.1f;
// 매개변수는 int a 와 int b이다.
// 반환값은 float 형이다.
~~~

즉 **Func< Parameters{,} , Return Type > instanceName = ( Parameters{} ) => implement Expression;**

식으로 사용 가능하다.


**[ 예제 ]**
~~~
using System;

namespace ConsoleApp1
{
    class Program
    {
        static float temp(int a, int b, int c) => (a + b + c) * 0.1f;
        static void Main(string[] args)
        {
            Func<float> func0 = () => 0.1f ;
            Func<int, float> func1 = (a) => a * 0.1f;
            Func<int, int, float> func2 = (a, b) => (a + b) * 0.1f;
            Func<int,int,int,float> func3 = new Func<int,int,int,float>(temp);
        }
    }
}
~~~
: 다음과 같이 Func delegate 변수를 활용 할 수 있다.


#### 5-2. Action Delegate

~~~
using System;

namespace ConsoleApp1
{
    class Program
    {
        static float temp(int a, int b, int c) => (a + b + c) * 0.1f;
        static void Main(string[] args)
        {
            Action func0 = () => Console.WriteLine("good");
            Action <int,int> func1 = (a, b) => Console.WriteLine("dfd");
        }
    }
}
~~~
: Action Delegate 변수는 그냥 Func에 Return Type이 없을 뿐 이다.

