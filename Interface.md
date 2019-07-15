# INTERFACE
---

###����
��ü ������ ���� �������̽� �ƴϰڽ��ϱ� ?
�߼� -> ����� �Ѿ�� ���� �庮�� ����

###�������̽��� �����̳� ?


~~~
using System;
class Triangle1
{
    private int width; private int height; private int area;
    public int Width
    {
        get { return width; }
        set { width = value; }
    }
    public int Height
    {
        get { return height; }
        set { height = value; }
    }
    public int Area
    {
        get { return width * height / 2; }
    }
}
~~~

�� �ణ �̷������� ������ ���� PRIVATE���� ����� ������ �ǵ帮�� �ʰ�, ����Ѵ�.
~~~
class Triangle2
{
    public int Width
    {
        get;
        set;
    }
    public int Height
    {
        get;
        set;
    }
    public int Area
    {
        get { return Width * Height / 2; }
    }
}
~~~
������ ���� �̷������� �ڵ����� ������Ƽ�� ����ϴ� ��찡 �ִ� ����.

�� ���⼭ ������ ���������°� �ƴϳ� ?? �� �� �ֵ�.

OOP ���� �����̶� : ��ü�� �����Ϳ� �ܺ� �ڵ尡 ���� �����ϴ� ���� ���´ٴ� �Ϳ� �ǹ̸� �д�.

�� GETTER�� SETTER�� �̿��Ͽ����� �����Ϳ� ������ �� �����Ƿ� ���м��� �������ٰ� �� �� �ִ�.


## [ ���� 1 ] ##
~~~
class MyClass

{

public string name; 

}
~~~
: name�� ���� �� �� �ִ� ����� ���� ����.


## [ ���� 2 ] ##
~~~
class MyClass

{

private string name; 

public string Name {get{return name;} set {name=value;}}

}
~~~

: ������ �Ʒ��� ���� ������Ƽ�� �̿��ϸ� ������ ������ ����ϴ�. name �ʵ忡 ���� �������� ������ �����ϱ��.

(Caller Attribute�� �̿��ϸ� � �ڵ忡�� �����ϰ� �ִ����� ������ ���� �ֽ��ϴ�.)



set ������Ƽ�� ���� �����غ����?


## [ ���� 3 ] ##
~~~
class MyClass

{

private string name; 

public string Name {

get{return name;} 

set 

{

if ( value.Length mmgt 16 )

throw new System.Exception("16�� �̻��� �̸��� ����� �� �����ϴ�.");

else if ( value.Length mmlt 2 )

throw new System.Exception("�̸��� �� ���� �̻��� �Է����ּ���.);

else

name = value;

}}}
~~~

: �̷��� ���Ŀ� ������ �̻��� ���� ����! ���� ���׸� �ذ� �� �� �ܼ��� ������Ƽ�� ��ȿ���� �˻��� �ָ� 

��ġ�� �� ������ ���� �� ���� ������ �����ϴ�.

��Ƽ�� ���м��� �����ͷ��� �������� ������ ���� �͸����� �޼��ߴٰ� �� �� �ֽ��ϴ�. 

�������� ������ �󸶳� ��ٷӰ� ���� �������� ���α׷��ӿ� �䱸���׿� �޷�������.

