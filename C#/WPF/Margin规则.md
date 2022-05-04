[Margin 在WPF中的用法_Stevenzhu18的博客-CSDN博客_wpf中margin](https://blog.csdn.net/Stevenzhu18/article/details/84335357)

Margin="1,2,3,4",1代表到left值，2代表到top值，3代表到right的值，4代表到bottom的值

但margin与 HorizontalAlignment， VerticalAlignment， Height，Width 这4个参数有关：

当HorizontalAlignment设定left时，margin取left的值，right的值就不起作用了。如果定义right，那么margin取right的值，left的值就没有作用了

如果没有声明，如verticalAlignment，这里会有两种情况：A ）控件的大小固定的，优先使用TOP的值并显示到bottom的值；B）控件的大小没有固定时，会取margin设定的值，控件大小会变化