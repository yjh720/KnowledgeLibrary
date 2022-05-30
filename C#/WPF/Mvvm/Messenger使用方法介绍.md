[利刃 MVVMLight 9：Messenger - Hello-Brand - 博客园 (cnblogs.com)](https://www.cnblogs.com/wzh2010/p/6679025.html)

MVVM Light Messenger 旨在通过简单的设计模式来精简此场景：任何对象都可以是接收端；任何对象都可以是发送端；任何对象都可以是消息。

如图：

![](https://yjh-image.oss-cn-shanghai.aliyuncs.com/img/20220530203759.png)

## **View和ViewModel之间的消息交互**
**消息标志token：ViewAlert**，用于标识只阅读某个或者某些Sender发送的消息，并执行相应的处理，所以Sender那边的token要保持一致。

**执行方法Action：ShowReceiveInfo**，用来执行接收到消息后的后续工作，注意这边是支持泛型能力的，所以传递参数很方便。

View.xaml.cs 代码如下：
```C#
public partial class NessagerForView : Window
    {
        public NessagerForView()
        {
            InitializeComponent();

            //消息标志token：ViewAlert，用于标识只阅读某个或者某些Sender发送的消息，并执行相应的处理，所以Sender那边的token要保持一致
            //执行方法Action：ShowReceiveInfo，用来执行接收到消息后的后续工作，注意这边是支持泛型能力的，所以传递参数很方便。
            Messenger.Default.Register<String>(this, "ViewAlert", ShowReceiveInfo);
            this.DataContext = new MessengerRegisterForVViewModel();
            //卸载当前(this)对象注册的所有MVVMLight消息
            this.Unloaded += (sender, e) => Messenger.Default.Unregister(this);
        }

        /// <summary>
        /// 接收到消息后的后续工作：根据返回来的信息弹出消息框
        /// </summary>
        /// <param name="msg"></param>
        private void ShowReceiveInfo(String msg)
        {
            MessageBox.Show(msg);
        }
    }
```

ViewModel代码：
```C#
public class MessengerRegisterForVViewModel:ViewModelBase
    {

        public MessengerRegisterForVViewModel()
        {

        }

        #region 命令

        private RelayCommand sendCommand;
        /// <summary>
        /// 发送命令
        /// </summary>
        public RelayCommand SendCommand
        {
            get
            {
                if (sendCommand == null)
                    sendCommand = new RelayCommand(() => ExcuteSendCommand());
                return sendCommand;

            }
            set { sendCommand = value; }
        }

        private void ExcuteSendCommand()
        {
            Messenger.Default.Send<String>("ViewModel通知View弹出消息框", "ViewAlert"); //注意：token参数一致
        }

        #endregion
    }
```

## **ViewModel和ViewModel之间的消息交互**
比如我打开了两个视图，一个视图是用户信息列表，一个视图是用户信息添加页面，如果想要达到添加信息之后，用户信息列表视图实时刷新，用消息通知无疑是一个很棒的体验。

我们来模拟一下：
MessengerRegisterViewModel代码：
```C#
public class MessengerRegisterViewModel:ViewModelBase
    {
        public MessengerRegisterViewModel()
        {
            ///Messenger：信使
            ///Recipient：收件人
            Messenger.Default.Register<String>(this,"Message",ShowReceiveInfo);
        }


        #region 属性

        private String receiveInfo;
        /// <summary>
        /// 接收到信使传递过来的值
        /// </summary>
        public String ReceiveInfo
        {
            get { return receiveInfo; }
            set { receiveInfo = value; RaisePropertyChanged(()=>ReceiveInfo); }
        }

        #endregion


        #region 启动新窗口

        private RelayCommand showSenderWindow;

        public RelayCommand ShowSenderWindow
        {
            get {
                if (showSenderWindow == null)
                    showSenderWindow = new RelayCommand(()=>ExcuteShowSenderWindow());
                return showSenderWindow;

            }
            set { showSenderWindow = value; }
        }

        private void ExcuteShowSenderWindow()
        {
            MessengerSenderView sender = new MessengerSenderView();
            sender.Show();
        }

        #endregion


        #region 辅助函数
        /// <summary>
        /// 显示收件的信息
        /// </summary>
        /// <param name="msg"></param>
        private void ShowReceiveInfo(String msg)
        {
            ReceiveInfo += msg+"\n";
        }
        #endregion
    }
```

```C#
public class MessengerSenderViewModel:ViewModelBase
    {
        public MessengerSenderViewModel()
        {

        }

        #region 属性
        private String sendInfo;
        /// <summary>
        /// 发送消息
        /// </summary>
        public String SendInfo
        {
            get { return sendInfo; }
            set { sendInfo = value; RaisePropertyChanged(()=>SendInfo); }
        }

        #endregion

        #region 命令

        private RelayCommand sendCommand;
        /// <summary>
        /// 发送命令
        /// </summary>
        public RelayCommand SendCommand
        {
            get
            {
                if (sendCommand == null)
                    sendCommand = new RelayCommand(() => ExcuteSendCommand());
                return sendCommand;

            }
            set { sendCommand = value; }
        }

        private void ExcuteSendCommand()
        {
            Messenger.Default.Send<String>(SendInfo, "Message");
        }

        #endregion
    }
```