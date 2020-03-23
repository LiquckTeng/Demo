## 接口描述
更新组织岗位信息
## 请求URL    
/openapi/fnd/v1/organization/position/modify
## 请求方式
POST
## 接口参数
### 接口参数说明
| 参数名 | 类型 | 长度 | 是否必输 | 默认值|说明 | 备注 |
| --- | --- | --- | --- | --- | --- |---|
|organizations |List  |  | 是 | |组织信息List |  |
|positions|List||是||岗位信息List||

### organizations

| 参数名 | 类型 | 长度 | 是否必输 | 默认值|说明 | 备注 |
| --- | --- | --- | --- | --- | --- |---|
|organizationCode|String||是||组织编号||
|organizationName|String||否||组织名称||
|parentOrganizationCode|String||否||上级组织编号||
|positionCode|String||否||主管岗位编号||
|description|String||否||组织描述||
|isEnabled|String|1|否|Y|是否有效|Y:是(默认),N:否|

### positions

| 参数名 | 类型 | 长度 | 是否必输 | 默认值|说明 | 备注 |
| --- | --- | --- | --- | --- | --- |---|
|positionCode|String||是||岗位编号||
|positionName|String||否||岗位名称||
|organizationCode|String||否||岗位所属组织编号||
|parentPositionCode|String||否||上级岗位编号||
|description|String||否||组织描述||
|isEnabled|String|1|否|Y|是否有效|Y:是(默认),N:否|

### 接口参数说明

```
{
	"organizations": [{
			"organizationCode": "ORG001",
			"organizationName": "组织1",
			"parentOrganizationCode": "ORG000",
			"positionCode": "POS001",
			"description": "测试组织1",
			"isEnabled": "Y"
		},
		{
			"organizationCode": "ORG002",
			"organizationName": "组织2",
			"parentOrganizationCode": "ORG001",
			"positionCode": "POS002",
			"description": "测试组织2",
			"isEnabled": "Y"
		}
	],
	"positions": [{
			"positionCode": "POS001",
			"positionName": "岗位1",
			"organizationCode": "ORG001",
			"parentPositionCode": "POS000",
			"description": "测试岗位1",
			"isEnabled": "Y"
		},
		{
			"positionCode": "POS002",
			"positionName": "岗位2",
			"organizationCode": "ORG002",
			"parentPositionCode": "POS001",
			"description": "测试岗位2",
			"isEnabled": "Y"
		}
	]
}
```
## 返回值
### 返回值参数
| 参数名 | 类型 | 说明 | 备注 |
| --- | --- | --- | --- | 
|success|Boolean|接口执行状态|true:接口执行成功,false:接口执行失败|
|errorCode|String|错误代码|当success为true时为空;当success为false时,显示错误代码|
|errorMsg|String|错误消息|当success为true时为空；当success为false时,显示接口执行异常消息|
|result|ResponseResult|接口返回数据|返回值以一个List和一个Long记录数据列表和总条数|

### 正常返回值说明

| 参数名 | 类型 | 说明 | 备注 |
| --- | --- | --- | --- | 
|success|Boolean|接口执行状态|正常执行为true|
|errorCode|String|错误代码|当success为true时为空|
|errorMsg|String|异常消息|正常执行时,errorMsg为空|
|result|Map|接口返回数据|返回值以一个List和一个Long记录数据列表和(分页)总条数|

result

| 参数名 | 类型 | 说明 | 备注 |
| --- | --- | --- | --- | 
|data|List|更新成功数量的封装对象||
|total|Long|数据条数||

### 正常返回值示例

```
{
    "success": true,
    "errorCode": null,
    "errorMsg": null,
    "result": {
        "data": ["1"],
        "total": 1
    }
}

```
### 错误返回值说明
接口处理出错时的返回值

| 参数名 | 类型 | 说明 | 备注 |
| --- | --- | --- | --- | 
|success|Boolean|接口执行状态|错误执行为false|
|errorCode|String|错误代码|错误代码|
|errorMsg|String|异常消息|错误执行时,errorMsg显示错误内容|
|result|ResponseResult|接口返回数据|为空|

### 错误返回值示例
错误返回值的demo



```
{
    "success": false,
    "errorCode": 200003,
    "errorMsg": "组织编码最多15个字符",
    "result":null
}
```

### 错误返回码说明

|错误代码|错误信息|说明|
| --- | --- | --- |
|200001|当前登录没有租户权限| 租户操作权限|
|200002|组织编码只允许字母或者数字,请检查| 无|
|200003|组织编码最多15个字符| 无|
|200004|组织名称最多15个字符| 无|
|200005|组织描述最多30个字符| 无|
|200006|组织的上层组织不能是自己| 无|
|200007|组织编码不能为空| 无|
|200008|组织名称不能为空| 无|
|200009|该组织下有子组织，无法失效| 无|
|200010|岗位编码只允许字母或者数字，请检查| 无|
|200011|岗位编码最多15个字符| 无|
|200012|岗位名称最多15个字符| 无|
|200013|岗位描述最多30个字符| 无|
|200014|组织名称为必填| 无|
|200015|岗位的上层岗位不能是自己| 无|
|200016|岗位编码不能为空| 无|
|200017|岗位名称不能为空| 无|
|200018|该岗位下有子岗位,无法停用| 无|
|200019|岗位不存在| 无|
|200020|组织不存在| 无|
|300001|跨服务异常| 无|
