[(21条消息) WPF教程（三十二）GridSplitter分割线_seanbei的博客-CSDN博客_wpf 分割线](https://blog.csdn.net/seanbei/article/details/53002237)


控件 [GridSplitter](https://docs.microsoft.com/zh-cn/dotnet/api/system.windows.controls.gridsplitter?view=windowsdesktop-6.0) 在行或列 [Grid](https://docs.microsoft.com/zh-cn/dotnet/api/system.windows.controls.grid?view=windowsdesktop-6.0)之间重新分配空间，而无需更改维度 [Grid](https://docs.microsoft.com/zh-cn/dotnet/api/system.windows.controls.grid?view=windowsdesktop-6.0)。 例如，当重设两列大小时 [GridSplitter](https://docs.microsoft.com/zh-cn/dotnet/api/system.windows.controls.gridsplitter?view=windowsdesktop-6.0) ， [ActualWidth](https://docs.microsoft.com/zh-cn/dotnet/api/system.windows.controls.columndefinition.actualwidth?view=windowsdesktop-6.0) 将增加一列的属性，同时 [ActualWidth](https://docs.microsoft.com/zh-cn/dotnet/api/system.windows.controls.columndefinition.actualwidth?view=windowsdesktop-6.0) 将另一列的属性减小为相同量。

下面的示例演示如何定义一个 [GridSplitter](https://docs.microsoft.com/zh-cn/dotnet/api/system.windows.controls.gridsplitter?view=windowsdesktop-6.0) 调整列 [Grid](https://docs.microsoft.com/zh-cn/dotnet/api/system.windows.controls.grid?view=windowsdesktop-6.0) 大小并占用列中 [Grid](https://docs.microsoft.com/zh-cn/dotnet/api/system.windows.controls.grid?view=windowsdesktop-6.0)的列的大小。

```xml
<Grid.ColumnDefinitions>
  <ColumnDefinition/>
  <ColumnDefinition Width="Auto" />
  <ColumnDefinition/>
</Grid.ColumnDefinitions>
```

```xml
<GridSplitter Grid.Column="1"
              HorizontalAlignment="Center"
              VerticalAlignment="Stretch"
              Background="Black" 
              ShowsPreview="True"
              Width="5"
              />
```

