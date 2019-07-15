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

Call Back Method 란

