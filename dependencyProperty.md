DEPENDENCY PROPERTY
===

> 의존 속성은 기존의 PROPERTY를 확장하여 WPF적인 요소를 추가한 것이다.<br>
> **Code-Behind와, xaml 두 측에서 모두 접근이 가능하며,**<br>
> 의존 속성이 변경되면 그에 맞게 자동으로 렌더링 로드 등의 처리를 한다.<br>
> 데이터 바인딩 , 애니메이션에 사용된다<br>
> 기존의 프로퍼티에 변경을 통보 **Change Notification** <br>
> 프로퍼티 값을 상속 **Property value inheritance**<br>
> 등등의 개쩌는 특성을 갖는다.

뭔소리냐?!
---
>**속성 또는 멤버변수와 비슷한데, wpf에서 기능을 확장했다!**  라고 짚고 넘어가보자.

예를 들어 Button의 BackGround Brush를 바꾸면 Button이 자동으로 다시 그려진다!

**의존** 이란 간단히 말해, 어떤 객체의 모습 혹은 행동이 의존 속성에 의해 영향을 받는다는 뜻 이다.

실제로 의존 속성의 값이 변경되면, **자동적으로 객체의 모습 또는 행동이 변하게 된다는 뜻이다.**

이것이 바로 데이터 바인딩을 할 수 있는 이유이다.




의존 속성의 구성요소
---
 - 1. System.Windows.DependencyObject
 - 2. System.Windows.DependencyProperty
 - 3. System.Windows.PropertyMetadata 

요렇게 세가지의 구성요소를 갖는데 자세히 알아 보도록 하자.

<br><br>
Dependency Object
---
Object다! 객체이다. 

곧 의존속성을 갖는 객체이다.

WPF의 대부분의 UI요소는 Dependency Object를 상속받아 구현되어있다.

이 Dependency Object는 GetValue와 SetValue 메소드를 지니고 있다. 

결국 모든 의존 속성들은, GetValue와 SetValue를 통하여 구현되어 있다고 볼 수 있다.

<br><br>
Dependency Property
---
의존 속성! 그 자체를 정의한 것이다.

예를들어, Button의 BackGround Brush에 대한 DP가 있을것이고, Brush의 Color에 대한 DP도 있을 것이다.

Dependency Property는 Dependency Object의 Instance가 아닌 Class로써 정의된다.

이게 무슨 의미를 갖느냐면, 

인스턴스는 있을수도 있고, 없을수도 있는것이지만, 클래스는 항상 존재하는 것이다,

고로, 모든 button에 BackGround Brush가 있다. => O

특정 button에만 BackGround Brush가 있다> => X

라는 말이다.

<br><br>
Dependency Metadata
---
Dependency Property의 부가 정보이다.

