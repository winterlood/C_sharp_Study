DATA BINDING
===
### DATA BINDING 이란 ?
---

CONTROL과, ELEMENT를 데이터에 연결시키는 기술이다.

데이터 바인딩은 간단하지만 복잡하다..

**즉 어플리케이션에서 <span style="color:red">내용</span> 화면에있는 객체 와 , 데이터를 일치시키는 기술이다.**

**CONTROL**은 다음 두가지 기능을 제공한다.

 - 데이터를 사용자에게 표시
 - 사용자가 데이터를 변경할 수 있게 해줌
    > 이 CONTROL들을 사용하면 너무 코드가 길다..
 
이 데이터 바인딩은 이벤트 핸들러를 대체 할 수 있다. 이것은 다음과 같은 이점을 갖는다.

 - C# 코드의 양을 매우 현저하게 줄여준다.
    > XAML에 정의된 데이터 바인딩은 C# 비하인드 코드에 이벤트 핸들러를 정의할 필요가 없어 <BR>
    > 비하인드 파일 자체가 필요 없는 경우도 있음
    
데이터 바인딩은 **소스**와 **타겟** 이 필요하다.

일반적으로 **소스 = 데이터** 이고, **타겟 = 컨트롤** 이다.

하지만 이것은 일반적인 예시 일 뿐 경우에 따라 다르다.

가장 간단한 바인딩의 예제를 통해 바인딩을 살펴보도록 하자.

[ 스크롤바의 VALUE 프로퍼티를 보여주기 위한 LABEL 컨트롤 ]
- 1. 스크롤바의 VALUE CHANGED 이벤트 핸들러를 이용 
        > 이것은 하지 않도록 하자.
  
- 2. 비하인드 코드 없이 DATA BINDING을 이용

### DATA BINDING 설정1
---
#### [예제 1]
~~~
<Window x:Class="DataBindingExam.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:DataBindingExam"
        mc:Ignorable="d"
        Title="MainWindow" Height="450" Width="800"
         >
    <StackPanel>
        <ScrollBar x:Name="scrollbar" Orientation="Horizontal"
                Margin="24" LargeChange="10" SmallChange="1" Maximum="100" Minimum="1"   ></ScrollBar>
        <Label HorizontalAlignment="Center"
               Content="{Binding ElementName=scrollbar, Path=Value}" Height="91" Margin="196,0,142,0" RenderTransformOrigin="0.5,0.5" Width="454">
            <Label.RenderTransform>
                <TransformGroup>
                    <ScaleTransform ScaleY="-1" ScaleX="-1"/>
                    <SkewTransform AngleY="0" AngleX="0"/>
                    <RotateTransform Angle="-180"/>
                    <TranslateTransform/>
                </TransformGroup>
            </Label.RenderTransform>
        </Label>
    </StackPanel>
</Window>
~~~

여기서 Target과 Source를 맞춰 보아라.

정답 : Target = **Label**, Source = **Scrollbar**


바인딩 자체는 언제나 타겟에 설정해야 한다. 

타겟인 label 컨트롤 패널에 
~~~
content = {Binding Elementname=scrollbar path=value} 
~~~

위 코드 처럼 Binding의 프로퍼티 중 ElementName 에는 Scorllbar의 Name이 정의 되고,

Path는 Scrollbar의 value가 설정되었다.


~~~
  Content="{Binding ElementName="scrollbar", Path="Value"}"
~~~

물론 따옴표도 써도 된다 ㅎㅎ
