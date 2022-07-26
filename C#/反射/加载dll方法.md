```C#
//dll名称无后缀，从目录加载
Assembly assembly = Assembly.Load("DB.MySql");
//带后缀或者完整路径
Assembly assembly2 = Assembly.LoadFrom("DB.MySql.dll");
```