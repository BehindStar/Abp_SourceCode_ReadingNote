# ABP 默认配置

## UnitOfWorkDefaultOptions

工作单元默认配置。

<table>
    <tr>
        <td>属性</td>
		<td>类型</td>		
		<td>默认值</td>
        <td>备注</td>
    </tr>
    <tr>
        <td>IsTransactional</td>
		<td>bool</td>		
		<td>True</td>
        <td>是否开启全局事务。</td>
    </tr>
    <tr>
        <td>Timeout</td>
		<td>TimeSpan?</td>		
		<td>null</td>
        <td></td>
    </tr>
    <tr>
        <td>IsolationLevel</td>
		<td>IsolationLevel?</td>		
		<td>null</td>
        <td></td>
    </tr>
    <tr>
        <td>Filters</td>
		<td>IReadOnlyList&lt;DataFilterConfiguration&gt;</td>		
		<td>空集</td>
        <td>是否开启全局事务。</td>
    </tr>	
</table>

## NavigationConfiguration

导航配置。

<table>
    <tr>
        <td>属性</td>
		<td>类型</td>		
		<td>默认值</td>
        <td>备注</td>
    </tr>
    <tr>
        <td>Providers</td>
		<td>ITypeList&lt;NavigationProvider&gt;</td>		
		<td>空集</td>
        <td>TypeList 类的集合。</td>
    </tr>	
</table>

## LocalizationConfiguration

本地化配置。

<table>
    <tr>
        <td>属性</td>
		<td>类型</td>		
		<td>默认值</td>
        <td>备注</td>
    </tr>
    <tr>
        <td>Languages</td>
		<td>IList&lt;LanguageInfo&gt;</td>		
		<td>空集</td>
        <td></td>
    </tr>
    <tr>
        <td>Sources</td>
		<td>ILocalizationSourceList</td>		
		<td></td>
        <td></td>
    </tr>
    <tr>
        <td>IsEnabled</td>
		<td>bool</td>		
		<td>True</td>
        <td>是否启用本地化</td>
    </tr>		
</table>

## AuthorizationConfiguration

授权配置。

<table>
    <tr>
        <td>属性</td>
		<td>类型</td>		
		<td>默认值</td>
        <td>备注</td>
    </tr>
    <tr>
        <td>Providers</td>
		<td>ITypeList&lt;AuthorizationProvider&gt;</td>		
		<td>空集</td>
        <td></td>
    </tr>	
</table>

## SettingsConfiguration

设置配置。

<table>
    <tr>
        <td>属性</td>
		<td>类型</td>		
		<td>默认值</td>
        <td>备注</td>
    </tr>
    <tr>
        <td>Providers</td>
		<td>ITypeList&lt;SettingProvider&gt;</td>		
		<td>空集</td>
        <td></td>
    </tr>	
</table>

## ModuleConfigurations

模块配置。

<table>
    <tr>
        <td>属性</td>
		<td>类型</td>		
		<td>默认值</td>
        <td>备注</td>
    </tr>
    <tr>
        <td>AbpConfiguration</td>
		<td>IAbpStartupConfiguration</td>		
		<td></td>
        <td>访问全局模块配置的一个入口</td>
    </tr>	
</table>

## EventBusConfiguration

事件总线配置。

<table>
    <tr>
        <td>属性</td>
		<td>类型</td>		
		<td>默认值</td>
        <td>备注</td>
    </tr>
    <tr>
        <td>UseDefaultEventBus</td>
		<td>bool</td>		
		<td>True</td>
        <td>是否使用默认总线</td>
    </tr>	
</table>

## MultiTenancyConfig

多租户配置。

<table>
    <tr>
        <td>属性</td>
		<td>类型</td>		
		<td>默认值</td>
        <td>备注</td>
    </tr>
    <tr>
        <td>IsEnabled</td>
		<td>bool</td>		
		<td></td>
        <td></td>
    </tr>	
</table>

## AuditingConfiguration

审计配置。

<table>
    <tr>
        <td>属性</td>
		<td>类型</td>		
		<td>默认值</td>
        <td>备注</td>
    </tr>
    <tr>
        <td>IsEnabled</td>
		<td>bool</td>		
		<td>True</td>
        <td>是否启用审计</td>
    </tr>	
    <tr>
        <td>IsEnabledForAnonymousUsers</td>
		<td>bool</td>		
		<td>True</td>
        <td>是否为匿名用户启用审计</td>
    </tr>	
    <tr>
        <td>MvcControllers</td>
		<td>IMvcControllersAuditingConfiguration</td>		
		<td></td>
        <td></td>
    </tr>	
    <tr>
        <td>Selectors</td>
		<td>IAuditingSelectorList</td>		
		<td></td>
        <td></td>
    </tr>	
</table>

## TypeFinder

类型查找器。

## DefaultModuleFinder

默认模块查找器。

## AbpModuleManager

ABP 模块管理器。

## LocalizationManager

本地化管理器。

