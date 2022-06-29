# 简介
[ObservableCollection类 - DarJeely - 博客园 (cnblogs.com)](https://www.cnblogs.com/Jeely/p/11076016.html)

在许多情况下，所使用的数据是对象的集合。 例如，数据绑定中的一个常见方案是使用 ItemsControl（如 ListBox、ListView 或 TreeView）来显示记录的集合。`ObservableCollection<T>` 就是一个主要用在WPF的控件和数据源的绑定中的集合，例如，

在xmal文件中，放置一个ListBox控件，名字叫做UserGroupListBox，ItemsSource设置如下：

```XML
<ListBox Name="UserGroupListBox" ItemsSource="{Binding Path=string,Mode=OneWay,UpdateSourceTrigger=PropertyChanged}" Height="214" HorizontalAlignment="Left" Margin="6,64,0,0" VerticalAlignment="Top" Width="173" Loaded="UserGroupListBox_Loaded" SelectionChanged="UserGroupListBox_SelectionChanged" />

```
对应的cs文件中：
```c#
ObservableCollection<string> strlist=new ObservableCollection<string>();

UserGroupListBox.ItemsSource=strlist;
```
这里用`ObservableCollection<T>` ，当strlist发生变化时，UserGroupListBox的界面也会实时更新，而是用`List<T>` 等其他容器是就没有这种效果。

可以枚举实现 IEnumerable 接口的任何集合。 但是，若要设置动态绑定，以便集合中的插入或删除操作可以自动更新 UI，则该集合必须实现 INotifyCollectionChanged 接口。 此接口公开 CollectionChanged 事件，只要基础集合发生更改，都应该引发该事件。

WPF 提供 ObservableCollection 类，它是实现 INotifyCollectionChanged 接口的数据集合的内置实现。

为了完全支持将绑定源对象中的数据值传送到绑定目标，在支持可绑定属性的集合中的每个对象都必须实现适当的属性更改通知机制，如 INotifyPropertyChanged 接口。

# ObservableCollection和List区别
[ObservableCollection和List的区别总结 - 雪~中~狼 - 博客园 (cnblogs.com)](https://www.cnblogs.com/zyj649261718/p/8072679.html)

## ObservableCollection比较简单，继承了Collection, INotifyCollectionChanged, INotifyPropertyChanged
Collection：为泛型集合提供基类。

INotifyCollectionChanged：将集合的动态更改通知给侦听器，例如，何时添加和移除项或者重置整个集合对象。

INotifyPropertyChanged：向客户端发出某一属性值已更改的通知。

所以再ObservableCollection这个类的方法，对数据的操作很少，重点放在了当自己本事变化的时候(不管是属性，还是集合)会调用发出通知的事件。(一般用于更新UI，当然也可以用于写其他的事情。这个以后会写)

## List就比较多了，继承了IList, ICollection, IEnumerable, IList, ICollection, IEnumerable
IList：表示可按照索引单独访问的一组对象。

ICollection：定义操作泛型集合的方法。

IEnumerable：公开枚举器，该枚举器支持在指定类型的集合上进行简单迭代。

IList：表示可按照索引单独访问的对象的非泛型集合。

ICollection：定义所有非泛型集合的大小、枚举器和同步方法。

IEnumerable：公开枚举器，该枚举器支持在非泛型集合上进行简单迭代。
```XML
<ListBox x:Name="listbind" Height="61" HorizontalAlignment="Left" Margin="146,12,0,0" VerticalAlignment="Top" Width="120" >
            <ListBox.ItemTemplate>
                <DataTemplate>
                    <TextBlock Text="{Binding Name}" />
                </DataTemplate>
            </ListBox.ItemTemplate>
        </ListBox>
        <ListBox x:Name="observbind" Height="74" HorizontalAlignment="Left" Margin="146,111,0,0" VerticalAlignment="Top" Width="120" >
            <ListBox.ItemTemplate>
                <DataTemplate>
                    <TextBlock Text="{Binding Name}" />
                </DataTemplate>
            </ListBox.ItemTemplate>
        </ListBox>
        <TextBlock Height="23" HorizontalAlignment="Left" Margin="38,58,0,0" Name="textBlock1" Text="List绑定数据" VerticalAlignment="Top" />
        <TextBlock Height="44" HorizontalAlignment="Left" Margin="12,125,0,0" Name="textBlock2" Text="ObservableCollection绑定数据" VerticalAlignment="Top" Width="112" />
        <Button Content="Button" Height="23" HorizontalAlignment="Left" Margin="77,211,0,0" Name="button1" VerticalAlignment="Top" Width="75" Click="button1_Click" />
```

```c#
public class Person  
{  
	public string Name { get; set; }  
}
```

```c#
private List<Person> person1 = new List<Person>();
private ObservableCollection<Person> person2 = new ObservableCollection<Person>();

public DemoTestDiff()
{
	InitializeComponent();
	person1.Add(new Person() { Name = "张三" });
	person1.Add(new Person() { Name = "李四" });
	listbind.ItemsSource = person1;
	person2.Add(new Person() { Name = "张三" });
	person2.Add(new Person() { Name = "李四" });
	observbind.ItemsSource = person2;
}

private void button1_Click(object sender, RoutedEventArgs e)
{
	person1.Add(new Person() { Name = "王五" });
	person2.Add(new Person() { Name = "王五" });
}
```

运行程序点击button按钮,然后只有ObservableCollection的有添加。

表示当集合对象的集合改变时，只有ObservableCollection会发出通知更新UI。

这只是他们两个区别之一。

综上所述：

ObservableCollection表示一个动态数据集合，在添加项、移除项或刷新整个列表时，此集合将提供通知。

List表示可通过索引访问的对象的强类型列表。提供用于对列表进行搜索、排序和操作的方法。(大部分操作用Linq，很强大也很方便。)
