[WPF star做些什么(Width="100*") - 问答 - 云+社区 - 腾讯云 (tencent.com)](https://cloud.tencent.com/developer/ask/sof/102032)

```xaml
<ColumnDefinition Width="10*"/> <ColumnDefinition Width="*"/>
```
这意味着第一列比第二列宽10倍

```xaml
<Grid.ColumnDefinitions>
    <ColumnDefinition Width="Auto" />  <!-- Auto-fit to content, 'Hi' -->
    <ColumnDefinition Width="50.5" />  <!-- Fixed width: 50.5 device units) -->
    <ColumnDefinition Width="69*" />   <!-- Take 69% of remainder -->
    <ColumnDefinition Width="31*"/>    <!-- Take 31% of remainder -->
</Grid.ColumnDefinitions>
<TextBlock Text="Hi" Grid.Column="0" />
```
![](https://yjh-image.oss-cn-shanghai.aliyuncs.com/img/20220429153803.png)