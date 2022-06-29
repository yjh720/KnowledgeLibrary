[C#中 ??、 ?、 ?: 、?.、?[ ] 问号 - 幽冥狂_七 - 博客园 (cnblogs.com)](https://www.cnblogs.com/youmingkuang/p/11459615.html)
[C# ??, ?, ?:, ?., ?[] question mark - Programmer All](https://www.programmerall.com/article/20582221/)
[operators - What does a question mark mean in C# code? - Stack Overflow](https://stackoverflow.com/questions/43075113/what-does-a-question-mark-mean-in-c-sharp-code)

# 可空类型修饰符（?）
引用类型可以使用空引用表示一个不存在的值，而值类型通常不能表示为空。  

例如：string str=null; 是正确的，int i=null; 编译器就会报错。  
为了使值类型也可为空，就可以使用可空类型，即用可空类型修饰符"？“来表示，表现形式为"T？”  

例如：int? 表示可空的整形，DateTime? 表示可为空的时间。  
T? 其实是System.Nullable(泛型结构）的缩写形式，  
也就意味着当你用到T？时编译器编译时会把T？编译成System.Nullable的形式。 

例如：int?,编译后便是System.Nullable的形式。

# 三元（运算符）表达式（?: )
例如：x?y:z 表示如果表达式x为true，则返回y；  
如果x为false，则返回z，是省略if{}else{}的简单形式。

# 空合并运算符(??)
用于定义可空类型和引用类型的默认值。  
如果此运算符的左操作数不为null，则此运算符将返回左操作数，否则返回右操作数。  
例如：a??b 当a为null时则返回b，a不为null时则返回a本身。  
空合并运算符为右结合运算符，即操作时从右向左进行组合的。  
如，“a??b??c”的形式按“a??(b??c)”计算。

# NULL检查运算符（?.）
例如我们要获取一个Point序列的第一个点的X坐标，第一感觉会这么写：  
int firstX = points.First().X;  
但是，老鸟会告诉你，这儿没有进行NULL检查，正确的版本是这样的：
```C#
int? firstX = null;
if (points != null)
{
　　var first = points.FirstOrDefault();
　　if (first != null)
　　firstX = first.X;
}
```

正确倒是正确了，代码取变得难读多了。在C# 6.0中，引入了一个 ?. 的运算符，前面的代码可以改成如下形式：
```C#
int? firstX = points?.FirstOrDefault()?.X;
```

从这个例子中我们也可以看出它的基本用法：如果对象为NULL，则不进行后面的获取成员的运算，直接返回NULL

需要注意的是，由于"?.“运算符返回的可以是NULL，当返回的成员类型是struct类型的时候，”?.“和”."运算符的返回值类型是不一样的。
```C#
　Point p = new Point(3, 2);
　Console.WriteLine(p.X.GetType() == typeof(int)); //true
　Console.WriteLine(p?.X.GetType() == typeof(int?)); //true
```

#  "?[]"运算符：
```C#
int? first = customers?[0].Orders.Count();
```
[Member access operators and expressions - C# reference | Microsoft Docs](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/member-access-operators#null-conditional-operators--and-)

-   If `a` evaluates to `null`, the result of `a?.x` or `a?[x]` is `null`.
- If `a` evaluates to non-null, the result of `a?.x` or `a?[x]` is the same as the result of `a.x` or `a[x]`, respectively.