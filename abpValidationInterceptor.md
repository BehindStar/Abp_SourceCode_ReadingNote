# ABP 的验证拦截器（ValidationInterceptor）

* 参数长度和参数值的长度是否一致

* 不可选的非out参数的参数值是否为空

* 自动验证 IEnumerable 集合的所有项目

* 只能验证实现了 IValidate 接口的对象

* 允许实现了 ICustomValidate 接口的对象自己进行验证 

* 通过数据标记进行验证
