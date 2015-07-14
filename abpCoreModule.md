# ABP 核心模块

## 预初始化（PreInitialize）

### 添加基础约定注册器 BasicConventionalRegistrar

注册所有扩展了 ITransientDependency，ISingletonDependency，IInterceptor 的服务。

扩展了 ITransientDependency，ISingletonDependency 的组件注册为自身（Foo 注册为 Foo）和与它名称匹配的接口（如 Foo 和 IFoo）。

扩展了 IInterceptor 的组件注册为自身，生命期类型为临时的。

IApplicationService，IPolicy，IRepository，IDomainService 等接口扩展了 ITransientDependency 接口。所以这些接口会被自动注册。

程序集中的非公共类型也会被注册。

核心模块中有许多扩展了上述接口的类，所以它们都会被自动注册。

:information_source: 注意，这里只是添加了约定，还没有开始注册。

### 初始化验证拦截器注册器  ValidationInterceptorRegistrar

为扩展了 IApplicationService 的服务添加验证拦截器（ValidationInterceptor）。

### 初始化工作单元注册器 UnitOfWorkRegistrar

为扩展了 IRepository 或 IApplicationService 的服务添加工作单元拦截器（UnitOfWorkInterceptor）。

为方法或派生类的方法添加了 UnitOfWorkAttribute 标注的类添加工作单元拦截器（UnitOfWorkInterceptor）

### 初始化认证拦截器注册器 AuthorizationInterceptorRegistrar

为扩展了 IApplicationService 的服务添加认证拦截器（AuthorizationInterceptor）

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



### 按照约定注册组件

## 初始化完成（PostInitialize）

### 注册缺失组件



### 解析本地化管理器并初始化



### 解析导航管理器并初始化



### 解析权限管理器并初始化



### 解析设置定义管理器并初始化


