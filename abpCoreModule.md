# ABP 核心模块

## 预初始化（PreInitialize）

### 添加基础约定注册器 BasicConventionalRegistrar

该注册器能够注册所有扩展了 ITransientDependency，ISingletonDependency，IInterceptor 的服务。

* 扩展了 ITransientDependency，ISingletonDependency 的组件注册为自身（Foo 注册为 Foo）和与它名称匹配的接口（如 Foo 和 IFoo）。

* 扩展了 IInterceptor 的组件注册为自身，生命期类型为临时的。

* IApplicationService，IPolicy，IRepository，IDomainService 等接口扩展了 ITransientDependency 接口。所以这些接口会被自动注册。

* 程序集中的非公共类型也会被注册。

核心模块中有许多扩展了上述接口的类，所以它们都会被自动注册。

:information_source: 注意，这里只是添加了约定，还没有开始注册。

### 初始化验证拦截器注册器  ValidationInterceptorRegistrar

为扩展了 IApplicationService 的服务添加验证拦截器（ValidationInterceptor）。

:information_source: 扩展了 IApplicationService 的服务在注册时会被添加一个[验证拦截器](abpValidationInterceptor.md)

### 初始化工作单元注册器 UnitOfWorkRegistrar

为扩展了 IRepository 或 IApplicationService 的服务添加工作单元拦截器（UnitOfWorkInterceptor）。

:information_source: 扩展了 IRepository 或 IApplicationService 的服务在注册时会被添加一个[工作单元拦截器](abpUnitOfWorkInterceptor.md)

为方法或派生类的方法添加了 UnitOfWorkAttribute 标注的类添加工作单元拦截器（UnitOfWorkInterceptor）

:information_source: 如果一个类的公共、非公共、实例方法或派生方法标注了 UnitOfWorkAttribute 特性，那么该类在注册时会被添加一个个[工作单元拦截器](abpUnitOfWorkInterceptor.md)

### 初始化认证拦截器注册器 AuthorizationInterceptorRegistrar

为扩展了 IApplicationService 的服务添加认证拦截器（AuthorizationInterceptor）

:information_source: 如果一个服务 扩展了 IApplicationService，那么该服务被注册时会被添加一个[认证拦截器](abpAuthorizationInterceptor.md)

### 初始化审计拦截器注册器 AuditingInterceptorRegistrar

为满足条件的服务添加审计拦截器（AuditingInterceptor）。

满足任意条件：

* 符合审计选择器的条件（参考下一条）
	
* 类标记了 AuditedAttribute
	
* 任意方法或派生类的方法标记了 AuditedAttribute

### 添加审计选择器

在审计的选择器列表中加入一个命名选择器（NamedTypeSelector）。该命名选择器选择扩展了 IApplicationService 的服务。

### 添加本地化资源

添加了一个 DictionaryBasedLocalizationSource 资源。就是 ABP 框架自身的本地化资源。

### 添加 Email 设置提供器 EmailSettingProvider

添加了 Email 设置提供器

### 注册工作单元过滤器

/// 待添加，没明白原理

## 初始化（Initialize）

### 安装事件总线安装器

根据事件总线配置，注册事件总线

* 如果使用默认总线，那么使用工厂方法注册 EventBus.Default 为服务 IEventBus，生命期类型为单例。 EventBus.Default 是 EventBus 的一个静态实例。

* 如果不使用默认总线，那么将 EventBus 注册为服务 IEventBus，生命期类型为单例。

:information_source: 似乎并没有什么区别，唯一的区别是使用默认总线的话可以通过 EventBus.Default 访问到总线。 

为所有派生自 IEventHandler 的服务添加自动注册到服务总线的功能。

:information_source: 也就是说，只需要将事件处理器注册到容器，就能自动订阅事件。

### 按照约定注册组件

按照约定注册组件。使用添加到 IIocManager 的约定注册器注册核心程序集的组件。

:information_source: 这里除了上文提到的在核心程序集的基础约定注册器之外，还可能有其他注册器。因为其他模块的 PreInitialize() 方法可能添加注册器。

此时不会安装 IoC 容器的安装器。

:information_source: 这里指 IWinsdorContainer 的 IWinsdorInstaller。

## 初始化完成（PostInitialize）

### 注册缺失组件

如果以下服务没有注册，那么将会注入默认组件。

<table>
    <tr>
        <td>服务</td>
		<td>默认组件</td>
    </tr>
    <tr>
        <td>IUnitOfWork</td>
		<td>NullUnitOfWork</td>
    </tr>
    <tr>
        <td>IAuditInfoProvider</td>
		<td>NullAuditInfoProvider</td>
    </tr>
    <tr>
        <td>IAuditingStore</td>
		<td>SimpleLogAuditingStore</td>
    </tr>	
</table>


### 解析本地化管理器并初始化

初始化本地化管理器。

:information_source: 如果在配置中关闭了本地化，那么不会进行初始化。

* 从配置中读取资源列表。

* 将资源添加到管理器。如果有重名的资源，将会抛出异常。

* 初始化资源。[查看详细]()

* 展开词典资源。[查看详细]()

### 解析导航管理器并初始化

* 创建导航提供器上下文。[查看详细]()

* 从配置中读取导航提供器类型列表。

* 从 IoC 解析导航提供器。

* 向导航提供器上下文设置提供器。[查看详细]()

### 解析权限管理器并初始化

* 从配置中读取认证提供器列表。

* 从 IoC中解析认证提供器并为权限管理器设置权限（如果未注册会自动注册）。[查看详细]()

* 添加所有权限。[查看详细]()

### 解析设置定义管理器并初始化

* 创建设置定义提供器上下文

* 从配置中读取设置提供器类型列表

* 从 IoC 中解析提供器。（如果未注册会自动注册）

* 获取设置定义。[查看详细]()
