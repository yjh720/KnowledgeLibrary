[ABP应用层——应用服务（Application services） - HackerVirus - 博客园 (cnblogs.com)](https://www.cnblogs.com/Leo_wl/p/4694493.html)

所有应用服务(Application Services)实例的生命周期都是暂时的(Transient)。这意味着在每次使用都会创建新的应用服务(Application Services)实例。ABP坚决地使用依赖注入技术。当一个应用服务(Application Services)类型需要被注入时，该应用服务(Application Services)类型的新实例将会被依赖注入容器自动创建。查看依赖注入(Dependency Injection)文档获取更多信息。