# INDEXER

### 인덱서가 무엇이냐?!?

인덱서도 프로퍼티의 한 종류이며, 객체 내의 데이터에 접근하도록 도와주는 역할을 한다.

구조체를 배열형식으로 사용할 수 있께 해주는 기법이다.

즉 클래스나 구조체의 인스턴스를 배열처럼 인덱싱 할 수 있게 해주는 녀석

해당 접근자가 매개변수를 사용한다는 것을 제외한다면 프로퍼티와 거의 유사하다.

주로 내부 배열을 캡슐화하기 위해 많이 사용한다고 한다.

한마디로 클래스를 배열처럼 쓰던... 진짜 배열을 뭘 쓰던 하여간 인덱스를 활용하려면 인덱서를 써야 한다!

C#의 프로퍼티 버전의 배열이다! 라고 보면 될듯하다.

이것도 물론 OOP의 정보 은닉성을 지키기 위해 사용된다.



## [클래스 선언] ##
~~~
Class IndexerText
{
  string [] test = "this is Text Code".Split();
  public string this [int index] // <== 요놈이 인덱서다.
  {
    get; set;
  }
}
~~~
: set을 생략하면 read-only 인덱서가 된다.

#### [ 참고 ] ####
~~~
public string this[int index] => test[index];
~~~
: 이런식으로 간결하게 정의가 가능하다.
 이해가 안된다면 
 [delegate and LamdaExpression](./delegate&lamda)참고바람.
 
 

## [ 사용 ] ##
~~~
indexerText it = new IndexerText();
Console.WriteLine(it[3]); // <== Code 를 반환할 것이다. split으로 내가 잘라놓았으니까 ㅎㅎ
it[3] = "SourceCode";
Console.WriteLine(it[3]); // <== SourceCode 를 반환한다. 
~~~

하나의 타입에 여러개의 인덱서 물론 사용 할 수 있다.

단 매개변수의 형식이 달라야 한다.



여기서 **인덱서** 가 뭐죠 ? .. 라고 할 수 있는데.

**[인덱서](./indexer)** 를 참조하길 바람.

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

또한 이것은 객체를 생성할 수 없다... 

그럼 어떻게 쓰라는거지 ?? 구현도 없고.. 객체도 못만들고 .. ?

정답 : 인터페이스는 해당 인터페이스를 참조하는 파생클래스로부터 객체를 생성하여 사용할 수 있다.

