# 什么是依赖属性
我们使用一个控件，可以看到这个控件有很多的属性，有属性就有字段的内存开销，但实际上对于一个控件，我们大多数只会使用其部分常用属性，比如Button我们最常使用Content，Height等属性，那些不经常使用的属性相当于白白占用着内存。当我们写一个复杂的XAML页面，涉及到很多控件的使用时，这种浪费内存的现象就很严重。

对此，微软在WPF中引入了依赖属性(Dependency Property)，依赖属性允许没有自己的字段，可以通过Binding绑定到其它对象的属性或者说数据源上，从而获得值，这种依赖在其它对象上的属性，就是依赖属性，当明确了它的功能，我想大家就不会对依赖二字产生疑惑了，依赖属性可以没有自己的字段，在使用时可以通过Binding从别的对象身上获取，给自己临时创建内存空间，这样不使用就不会有多余内存消耗，但是要注意一点，如果直接给依赖属性赋值，它依然如属性一样，会占用空间，必须使用Binding才能实现“依赖”。

# 代码
```C#

public class Pikachu : DependencyObject
{
    public static readonly DependencyProperty PikachuNameProperty =
        DependencyProperty.Register("PikachuName",typeof(string),typeof(Pikachu));
}

```
上文说到，使用依赖属性必须要继承DependencyObject类，另外，声明

依赖属性，需要使用public static readonly三个修饰符修饰，实例依赖属性也不是通过new操作符，而是通过DependencyProperty的Register方法来获取。
