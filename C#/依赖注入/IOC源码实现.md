[百度网盘 - 视频播放 (baidu.com)](https://pan.baidu.com/play/video#/video?path=%2F%E5%9F%B9%E8%AE%AD%E8%B5%84%E6%96%99%2F%E5%A5%95%E9%BC%8E%E9%80%9A%E5%AD%A6%E4%B9%A0%E8%B5%84%E6%BA%90%2F.net%2F2022-04-19-%E4%BC%81%E4%B8%9A%E5%B8%B8%E7%94%A8%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F%2B.NET6%E6%BA%90%E7%A0%81%E6%B7%B1%E5%85%A5%E5%88%86%E6%9E%90%2F2022-04-19-%E4%BC%81%E4%B8%9A%E5%B8%B8%E7%94%A8%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F%2B.NET6%E6%BA%90%E7%A0%81%E6%B7%B1%E5%85%A5%E5%88%86%E6%9E%90.mp4&t=-1)


# 什么是IOC容器

基本功能
1. 创建对象
2. 存储对象
3. DI依赖注入 对象属性赋值

高级功能
1. AOP 面向切面编程 对象的代理
2. 生命周期 对象使用的范围-> 单例，scope，trinsient

# 条件
1. 工厂模式
2. 集合
3. 反射
4. 特性
5. 递归，自己调用自己


```C#
private Dictionary<string, object> iocContainer = new Dictionary<string, object>();
private Dictionary<string, Type> iocTypeContainer = new Dictionary<string, Type>();

public DefaultFactory()
{

	Assembly assembly = Assembly.Load("xxx.xxx.xxx");
	Type[] types = assembly.GetTypes();
	foreach(var type in types)
	{
		//1.创建对象
		object _object = CreateObject(type,types);
		

		//2.存储对象
		//全限定名：命名空间+类名
		iocContainer.Add(type.FullName, _object);
	}
}

//递归
//1. 在业务逻辑中，找到通用代码
//2. 在通用代码中，找到通用参数
//3. 自己调用自己

//缺陷
//1. 性能偏低
//2. 如果types有1000个对象，使用foreach循环找一个，性能下降
//方案：空间换时间思想。用字典的空间换for循环的时间
public object CreateObject(Type type, Type[] types)
{
	//1.创建对象
	object _object = Activator.CreateInstance(type);
	
	//1.1.对象属性赋值
	PropertyInfo[] propertyInfos = type.GetProperties();
	foreach(var propertyInfo in propertyInfos)
	{
		foreach(var t in types)
		{
			if(propertyInfo.PropertyType.Equals(t))
			{
				//包含依赖嵌套，递归
				//Object _objectValue = Activator.CreateInstance(t);
				Object _objectValue = CreatObject(t,types);
				propertyInfo.SetValue(_object, _objectValue);
			}
		}
	}
}
```