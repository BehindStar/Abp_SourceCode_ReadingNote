# ABP 的认证拦截器（AuthorizationInterceptor）

对组件的方法进行权限认证。

* 权限由 AbpAuthorizeAttribute 标记。

* 同时验证定义在类上面和方法上面的 AbpAuthorizeAttribute 特性

* 解析 IAuthorizeAttributeHelper 服务进行验证。

  :information_source: 实现类为 AuthorizeAttributeHelper

* 验证是否登陆

* 解析 IPermissionChecker 服务进行权限检查

  :information_source: 默认实现类为 NullPermissionChecker ，该实现总是返回 True

  :information_source: 需要自定义权限检查。（Model-Zero）好像已经实现了？
