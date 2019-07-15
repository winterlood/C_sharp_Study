DEPENDENCY PROPERTY
===

> 의존 속성은 기존의 PROPERTY를 확장하여 WPF적인 요소를 추가한 것이다.<br>
> **Code-Behind와, xaml 두 측에서 모두 접근이 가능하며,**<br>
> 의존 속성이 변경되면 그에 맞게 자동으로 렌더링 로드 등의 처리를 한다.<br>
> 데이터 바인딩 , 애니메이션에 사용된다<br>
> 기존의 프로퍼티에 변경을 통보 **Change Notification** <br>
> 프로퍼티 값을 상속 **Property value inheritance**<br>
> 등등의 개쩌는 특성을 갖는다.

정리
---
>**한마디로 속성 또는 멤버변수와 비슷한데, wpf에서 기능을 확장했다!**  라고 짚고 넘어가보자.

예를 들어 Button의 BackGround Brush를 바꾸면 Button이 자동으로 다시 그려진다!

사용법
---
 - 1. 의존 속성을 선언
 - 2. 의존 속성을 등록
 - 3. 프로퍼티 생성

다음과 같은 세가지 단계를 갖는다.

