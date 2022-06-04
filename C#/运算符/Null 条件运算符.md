# Null 条件运算符 ?. 和 ?[]
[成员访问运算符和表达式 - C# 参考 | Microsoft Docs](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/operators/member-access-operators#null-conditional-operators--and-)

仅当操作数的计算结果为非 null 时，null 条件运算符才会将[成员访问](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/operators/member-access-operators#member-access-expression-)[](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/operators/member-access-operators#member-access-expression-) 或[元素访问](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/operators/member-access-operators#indexer-operator-)[](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/operators/member-access-operators#indexer-operator-) 运算应用于其操作数；否则，将返回 `null`。

[方法返回值 有个问号，这是什么语法？-CSDN社区](https://bbs.csdn.net/topics/390251687)
返回值带？，表示可空类型；

## 空合并运算符(??)

用于定义可空类型和引用类型的默认值。  
如果此运算符的左操作数不为null，则此运算符将返回左操作数，否则返回右操作数。  
例如：a??b 当a为null时则返回b，a不为null时则返回a本身。  
空合并运算符为右结合运算符，即操作时从右向左进行组合的。  
如，“a??b??c”的形式按“a??(b??c)”计算。