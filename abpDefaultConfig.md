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
		<td>IReadOnlyList<DataFilterConfiguration></td>		
		<td>空集</td>
        <td>是否开启全局事务。</td>
    </tr>	
</table>
