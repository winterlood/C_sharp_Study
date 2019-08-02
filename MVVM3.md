How to Implement MVVM? 
===

1. In Code Behind.
---

View에서 View Model을 분리함에 집중하라.

전편에서 기술하였듯, Data Context를 통해 View와 View Model간의 의존성을 만들고, 

바인딩으로 프로퍼티를 조작하여 사용한다고 하였다.

Data Context를 그럼 어떻게 할당하는가 ?? 에 대하여 이야기 해 보자.

~~~
  public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();
            this.DataContext = new ViewModel();
        }
    }
~~~

가장 기본중의 기본이 되는 behind code영역 에서의 Data context 할당이다.

ViewModel이라는 class를 인스턴스화 하여 현재 View의 Data Context로 삼는것이다.

이렇게 Window 자체의 Data Context를 할당해주면,

Data Context == null 인 모든 하위 오브젝트 들은 (UIElement 들)

ViewModel을 Data Context로 삼게 된다.
> 별도의 할당이 있다면 그것을 Data Context로 삼는다.


2. In XAML
---

1번에서는 Behind 코드에서 DataContext를 할당했다면, 이번에는 XAML에서 할당하도록 하자.

DATA CONTEXT는 어짜피 DEPENDENCY PROPERTY이므로 XAML에서 직접 접근할 수있따.

다음과 같은 방식으로 활용한다.

~~~
    <Window.DataContext>
        <local:ViewModel></local:ViewModel>
    </Window.DataContext>
~~~

현재 Window의 Data Context에 Local Namespace 의 View Model의 인스턴스를 할당했다.

Local이 뭐냐 ? 할 수 있는데.

~~~
<xmlns:local="clr-namespace:자기솔루션이름">
~~~
이런식으로 xmlns를 선언하면, local namespace를 통해 viewmodel.cs에 접근 할 수 있다.

물론 현재 View파일과 ViewModel 파일이 같은 폴더내에 위치해야만 한다.


