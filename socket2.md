# Socket with C#

![](./socket6.jpg)

오늘은 요 빨간색 부분 할겁니다.

군말없이 바로 가도록 하죠


저번에 소켓을 연결하는데 까지만 하고 뭔가 전송은 안해봤습니다 

이제는 실제로 뭔가를 주고 받아 보도록 하겠습니다

우리의 목표는 메신저이므로 **문자열** 을 목표로 해보도록 하겠습니다.

## Server : Send Message

자. 이제 저번에 만들었던 tmpSock 이라는 client와 연결된 Socket 객체를 통해 메세지를 보내 볼게요

~~~
using System;
using System.Net.Sockets;
using System.Net;
using System.Text;

namespace sockettest
{
    class Program
    {
        static void sendStr(IAsyncResult a)
        {
            Socket tmpSock = (Socket)a.AsyncState;
            int strlen = tmpSock.EndSend(a);
        }
        static void Main(string[] args)
        {
            Socket serverSock = new Socket(AddressFamily.InterNetwork, SocketType.Stream, ProtocolType.IP);
            serverSock.Bind(new IPEndPoint(IPAddress.Any, 10801));
            serverSock.Listen(100);
            Console.WriteLine("정환 서버 Listen중........");
            Socket tmpSock = serverSock.Accept();
            byte[] msg = Encoding.Default.GetBytes("aaaaaaaaaaa");
            tmpSock.BeginSend(msg, 0, 11, SocketFlags.None, new AsyncCallback(sendStr), tmpSock);
        }
    }
}
~~~

이번엔 뭐가 좀 많습니다...

차근차근 하나씩 뜯어 보도록 할게요

### 보낼 텍스트 정하기
~~~
byte[] msg = Encoding.Default.GetBytes("aaaaaaaaaaa");
~~~

msg 라는 byte형 객체에 "aaaaaaaaaaa" 을 담습니다.

byte 형식으로 보내게 되있으므로 인코딩 과정을 거쳤습니다.

> **using System.Text;** 을 using 해주셔야 Encoding 을 이용하실 수 있어용

### 보내기

~~~
tmpSock.BeginSend(msg, 0, 11, SocketFlags.None, new AsyncCallback(sendStr), tmpSock);
~~~

우선 **BeginSend()** 메서드는 데이터를 전송해줍니다.

파라미터로는 여러개가 필요한데요 이것도 하나하나 뜯어 봅시다...


#### 1. msg

그냥 byte형 메세지 입니다. 

#### 2~3. 0,11

그냥 0부터 11글자 라는겁니다.

aaaaaaaaaaa 가 11글자입니다..


#### 4. SocketFlags.None

SocketFlags 는 전송 옵션입니다.

사실 고급 옵션입니다. 우리는 그냥 None을 쓰도록 합시다 ..

사실 저도 잘 몰라유 ㅠ..


#### 5. new AsyncCallback(sendStr)

자 보시면 매개변수로 AsyncCallback이라는 메서드가 sendStr이라는 메서드를 받는걸 보실 수 있는뎅

제가 이게 뭐라그랬죠?

맞아요! 이게바로 그 유명한 **Call Back Method**입니다!!

분명 Delegate 설명하면서 했을 거에요

자 뭐하는 거냐? 전송과정이 다 끝난 뒤에 sendStr을 호출하라는 겁니다.

해당되는 비동기 작업을 완료할 때 호출되는 메소드를 지정해주는 친구입니다.

가장 중요한 점 기억하셔야 될건 전송이 끝나면 sendStr을 호출한다는 점이에요


#### 5-1. sendStr

이것도 메서드이므로 구현 해주어야 합니다.

자 그럼 얘가 뭐길래 전송이 끝나면 호출이 되는 거시냐 ?!

~~~
 static void sendStr(IAsyncResult a)
        {
            Socket tmpSock = (Socket)a.AsyncState;
            int strlen = tmpSock.EndSend(a);
        }
~~~

보시면, tmpSock 이라는 소켓 객체가 (Socket) 으로 명시적으로 캐스팅 된 a의 

