[MVVM - 深入介绍 MVVM Light Messenger | Microsoft Docs](https://docs.microsoft.com/zh-cn/archive/msdn-magazine/2014/june/mvvm-the-mvvm-light-messenger-in-depth)

Messenger 之类的系统有时称为事件总线或事件聚合器。

问题：在 MVVM Light 创建后，许多消息系统都要求接收端或发送端实施具体的方法。例如，可能存在指定了接收方法的 IReceiver 接口，而为了向消息系统注册，对象就需要实施此接口。这种限制很烦人，因为它限制了消息系统的实际使用者。例如，如果您使用的是第三方程序集，则无法向消息系统注册此库中的实例，因为您无权访问代码，并且无法修改第三方类来实施 IReceiver。

解决方法：MVVM Light Messenger 旨在通过简单的前提来精简此场景：任何对象都可以是接收端；任何对象都可以是发送端；任何对象都可以是消息。

MVVM Light Messenger 是在两个独立对象中使用。

注册实例不会将消息明确发送给 RegisteredUser 实例。相反，它会通过 Messenger 广播消息。任何实例都可以注册此类型的消息，并在消息发送时收到通知。

**发送和接收消息**
```C#
public class Registration 
{ 
	public void SendUpdate() 
	{ 
		var info = new RegistrationInfo { /** ...一些属性 */}; 
		Messenger.Default.Send(info); 
	} 
} 

public class RegisteredUser 
{ 
	public RegisteredUser() 
	{ 
		Messenger.Default.Register<RegistrationInfo>( this, HandleRegistrationInfo); 
	} 
	
	private void HandleRegistrationInfo(RegistrationInfo info) 
	{ 
		/* 更新已注册的用户信息*/ 
	} 
} 

public class RegistrationInfo { // ...一些属性 }
```

**使用命名方法或 Lambda 进行注册**
```C#
public UserControl() { InitializeComponent(); 
// 使用命名方法进行注册 ---- 
Loaded += Figure2ControlLoaded; 
Messenger.Default.Register<AnyMessage>( this, HandleAnyMessage); 
// 使用匿名 Lambda 进行注册 ---- 
Loaded += (s, e) => { /* 执行某操作*/ }; 
Messenger.Default.Register<AnyMessage>( this, message => { /* 执行某操作*/ }); 
					  } 
private void HandleAnyMessage(AnyMessage message) { // 执行某操作 } private void Figure2ControlLoaded (object sender, RoutedEventArgs e) { // 执行某操作 }
```