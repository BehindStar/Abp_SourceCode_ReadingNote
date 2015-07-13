# Abp 框架初始化

ABP 中负责初始化框架的类是 AbpBootstrapper。

# 实例化 ABP 启动程序

AbpBootstrapper 公开了两个构造函数，一个默认构造函数，一个需要参数 IIocManager。

使用默认的构造函数：

```csharp
var bootstrapper = new AbpBootstrapper();
```

使用带参数 IIocManager 的构造函数：

```csharp
var bootstrapper = new AbpBootstrapper(aIocManager);
```

:information_source: 默认构造函数内部使用类 IocManager 的静态实例实例化类。

# 初始化

AbpBootstrapper 公开 Initialize() 方法用于初始化。

```csharp
AbpBootstrapper.Initialize();
```

## 使用 IoC 容器安装 AbpCoreInstaller

在 AbpCoreInstaller 中，向 IoC 容器中注册了配置（工作单元默认选项、导航配置、本地化配置、认证配置、设置配置、模块配置、事件总线配置、多租户配置、审计配置、ABP 启动配置，这些都是单例）、类型查找器（单例）、默认模块查找器（临时）、ABP 模块管理器（单例）、本地化管理器（单例）。[查看详细](abpCoreInstaller.md)

## 解析和初始化 AbpStartupConfiguration

解析了本地化配置、模块配置、导航配置、认证配置、设置配置、工作单元配置、事件总线配置、多租户配置、审计配置。

如果需要访问全局配置，可以在需要的类中注入 IAbpStartupConfiguration。

## 解析和初始化模块管理器

* 获取当前应用程序域已加载的所有程序集中的所有派生自AbpModule的非抽象类型。

* 查找上一步未加载的依赖模块（基于 DependsOnAttribute 属性指定的模块）。

* 将所有模块注册为自身的服务（单例）。

* 从 IoC 容器解析所有模块，并为模块设置属性 IocManager 和 Configuration（ABP 启动配置） 的值。（这样所有模块能访问容器和配置）

* 将 AbpKernelModule 移动到最前面。

* 为所有模块设置依赖。（该模块所在程序集引用或的程序集的内的模块，使用 DependsOnAttribute 指定的模块）

* 根据依赖顺序初始化模块。依次调用模块的以下方法 PreInitialize()，Initialize()，PostInitialize()。所有模块的 PreInitialize() 方法执行完成后，执行 Initialize() 方法，最后是 PostInitialize() 方法。


