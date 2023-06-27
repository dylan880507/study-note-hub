## 1>相关文章

[C#中Struct与Class的区别](https://www.cnblogs.com/gsk99/archive/2010/12/13/1904552.html)

[SQL Server 2012使用Offset/Fetch Next实现分页](https://www.cnblogs.com/godbell/p/7260704.html)





## 2>Tuple(元组)

```C#
//Tuple元组: C# 4.0的新特性, 只读
//是一种数据结构，引用类型，具有特定数量和元素序列
//最多有八个元素，要想更多只能通过最后一个元素进行嵌套扩展，（使用值元组的嵌套和Rest属性实现）
//访问元素通过ItemX去访问，使用前需要明确元素顺序，属性名字没有实际意义
private System.Tuple<string, int> TestFunc6()
{
	System.Tuple<string, int> tuple = new System.Tuple<string, int>("key", 1);
	Debug.Log(tuple.Item1 + tuple.Item2);
	return tuple;
}
```

## 3>ValueTuple(值元组)

```C#
//ValueTuple值元组: C# 7.0的新特性
//也是一种数据结构，是值类型，用于表示特定数量和元素序列
//值元组元素是可变的，不是只读的，值元组的数据成员是字段不是属性
private System.ValueTuple<string, int> TestFunc7()
{
	System.ValueTuple<string, int> valueTuple = new System.ValueTuple<string, int>("key", 1);
	Debug.Log(valueTuple.Item1 + valueTuple.Item2);
	return valueTuple;
}
//ValueTuple值元组，返回值可以不明显指定ValueTuple，如(string, int)
private (string, int) TestFunc8()
{
	return ("key", 1);
}
//ValueTuple值元组，返回值可以指定元素名字，方便赋值和访问
private (string key, int value) TestFunc9()
{
	return (key: "key", value: 1);
}
```

## 4>switch类型模式

```C#
public string GetDataFormat(IFormatCreater entity, Data data) => entity switch
{
	CSVFormatCreater csvFormatCreater => csvFormatCreater.ToCSV(data),
	JsonFormatCreater jsonFormatCreater => jsonFormatCreater.ToJson(data),
	XMLFormatCreater xmlFormatCreater => xmlFormatCreater.ToXML(data),
	YamlFormatCreater yamlFormatCreater => yamlFormatCreater.ToYAML(data),
	_ => "this format is not adapted"
};
```

## 5>[sealed关键字](https://www.cnblogs.com/ring1992/p/5980336.html)

*`当对一个类应用 sealed 修饰符时，此修饰符会阻止其他类从该类继承。类似于Java中final关键字。`

```C#
class A {}
sealed class B : A {}
```

*`能够允许类从基类继承，并防止它们重写特定的虚方法或虚属性。`

```C#
public class D  
{  
    /* ConsoleApplication1.MSFun.Sealed.D.M()'   
     * cannot be sealed because it is not an override   
     */  
    public sealed void M() { Console.WriteLine("D.M()"); }  
}

public class A  
{  
    protected virtual void M() { Console.WriteLine("A.M()"); }  
    protected virtual void M1() { Console.WriteLine("A.M1()"); }  
}  
  
public class B : A  
{  
    protected sealed override void M() { Console.WriteLine("B.M()"); }  
    protected override void M1() { Console.WriteLine("B.M1()"); }  
}  
  
public sealed class C : B  
{  
    /* ConsoleApplication1.MSFun.Sealed.C.M()': 
     * cannot override inherited member 'ConsoleApplication1.MSFun.Sealed.B.M()' 
     * because it is sealed */  
    //protected override void M() { Console.WriteLine("C.M()"); }  
  
    protected override void M1() { Console.WriteLine("C.M1()"); }  
} 
```

