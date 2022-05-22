
1. App.xaml中需要添加Startup
```xaml
<Application x:Class="Roboticplus.BevelCutting.OnsiteTest.UI.App"
             xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
             xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
             xmlns:local="clr-namespace:Roboticplus.BevelCutting.OnsiteTest.UI"
             **Startup="App_Startup"** 
             xmlns:d="http://schemas.microsoft.com/expression/blend/2008" 
             d1p1:Ignorable="d"
             xmlns:d1p1="http://schemas.openxmlformats.org/markup-compatibility/2006"
             >
    <Application.Resources>
        <ResourceDictionary>
            <vm:ViewModelLocator x:Key="Locator" d:IsDataSource="True" xmlns:vm="clr-namespace:Roboticplus.BevelCutting.OnsiteTest.UI.ViewModel"/>
        </ResourceDictionary>
    </Application.Resources>
</Application>
```

2. MainWindow.xaml中需要添加OnInitialized，OnClosed，OnLoaded
```xaml
<Window x:Class="Roboticplus.BevelCutting.OnsiteTest.UI.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:Roboticplus.BevelCutting.OnsiteTest.UI"
        xmlns:officeus ="clr-namespace:Roboticplus.BevelCutting.ServiceTest.UserControls;assembly=Roboticplus.BevelCutting.ServiceTest" 
        xmlns:osus="clr-namespace:Roboticplus.BevelCutting.OnsiteTest.UI.UserControls"
        mc:Ignorable="d"
        DataContext="{Binding MainView, Mode=OneWay, Source={StaticResource Locator}}"
        Title="MainWindow" Height="450" Width="800" **Initialized="OnInitialized"  Closed="OnClosed" Loaded="OnLoaded"**>
</Window>
```

