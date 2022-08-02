[C# 读写App.config配置文件的方法 - 腾讯云开发者社区-腾讯云 (tencent.com)](https://cloud.tencent.com/developer/article/1054497)

```xml
            <? xml version = "1.0" encoding = "utf-8" ?>
   < configuration >
   
       < appSettings >
   
           < add key = "connectionstring" value = "User Source=.;Password=;Initial Catalog=test;Provider=SQLOLEDB.1;" />
      
              < add key = "TemplatePATH" value = "Template" />
         
             </ appSettings >
         </ configuration >
```

```C#
private void AccessAppSettings()
{
	//获取Configuration对象
	Configuration config = System.Configuration.ConfigurationManager.OpenExeConfiguration(ConfigurationUserLevel.None);
	//根据Key读取<add>元素的Value
	string name = config.AppSettings.Settings["name"].Value;
	//写入<add>元素的Value
	config.AppSettings.Settings["name"].Value = "fx163";
	//增加<add>元素
	config.AppSettings.Settings.Add("url", "http://www.fx163.net");
	//删除<add>元素
	config.AppSettings.Settings.Remove("name");
	//一定要记得保存，写不带参数的config.Save()也可以
	config.Save(ConfigurationSaveMode.Modified);
	//刷新，否则程序读取的还是之前的值（可能已装入内存）
	System.Configuration.ConfigurationManager.RefreshSection("appSettings");
}
```
