## 接口描述
批量更新员工账号信息
## 请求URL    
/openapi/fnd/v1/employee/batch
## 请求方式
POST
## 接口参数
### 接口参数说明
| 参数名 | 类型 | 长度 | 是否必输 | 默认值|说明 | 备注 |
| --- | --- | --- | --- | --- | --- |---|
|employeeCode | String | 15 | 是 | | 成员code |  |
|employeeName | String | 30 | 是 | | 成员姓名 |  |
|employeeType | String | 15 | 是 | | 成员类型 | 如：EXTERNAL外部,INTERNAL内部|
|gender | String | 30 | 是 | | 性别 | 如：UNCERTAIN不确定,FEMALE女,MALE男|
|inviteStatus | String | 15 | 是 | | 邀请状态 | 如：JOINED加入,UNINVITED未邀请,INVITATING邀请中,UNBIND已解绑|
|email | String | 15 | 是 | | 邮箱账号 | 经过正则校验|
|mobile | String | 11 | 是 |  | 手机号 | 经过正则校验|
|certificateId | String | 20 | 否 | | 证件号 ||
|certificateType | String | 20 | 否 | | 证件类型 | 如：IDCARD身份证，PASSPORT护照|
|joinDate | String | 15 | 否 | | 入职时间 | |
|bornDate | String | 15 | 否 | | 生日 | |
|departureDate | String | 15 | 否 | | 离职时间 | |
|fromCompany | String | 50 | 否 | | 外部员工公司 | 不是表中维护的公司不能更新导入，抛错误码200039 |
|isEnabled | String | 1 | 否 | | 是否有效 | Y：是（默认），N：否|
|lastName | String | 60 | 否 | | 姓 | |
|firstName | String | 60 | 否 | | 名 | |
|contactPhone | String | 20 | 否 | | 联系电话 | |
|fixPhone | String | 20 | 否 | | 固定电话 | |
|status | String | 15 | 是 | | 状态 | 如：REGULAR在职，QUIT离职，PROBATION试用，INTERNSHIP实习|
|employeeExtValueList | List | | 否 | | 成员扩展字段 | 自定义添加,键值对形式，见下方employeeExtValues解释|

employeeExtValueList

| 参数名 | 类型 | 长度 | 是否必输 | 默认值|说明 | 备注 |
| --- | --- | --- | --- | --- | --- |---|
|fieldCode | String | 255 | 是 | | 字段code |  |
|fieldValue|String|255|||字段值|是否必输取决于扩展字段的配置|

### 接口参数说明

```
[{
	"employeeCode": "43992288",
	"employeeName": "姓名",
	"employeeType": "INTERNAL",
	"gender": "FEMALE",
	"inviteStatus": "JOINED",
	"email": "43992288@qq.com",
	"mobile": "13737457548",
	"certificateId": "3333333333334444",
	"certificateType": "IDCAR",
	"joinDate": "2019-10-29 13:33:22",
	"bornDate": "1995-10-23 21:22:33",
	"departureDate": "2019-10-23 21:22:33",
	"fromCompany": "燕千云内部",
	"isEnabled": "Y",
	"lastName": "姓",
	"firstName": "名",
	"contactPhone": "联系电话",
	"fixPhone": "固定电话",
	"status": "REGULAR",
	"employeeExtValueList": [
	{
	   "fieldCode": "extField1",
	   "fieldValue": "123"
	},
	{
	   "fieldCode": "extField2",
	   "fieldValue": "456"
	}]	
}]
```
## 返回值
### 返回值参数
| 参数名 | 类型 | 说明 | 备注 |
| --- | --- | --- | --- | 
|success|Boolean|接口执行状态|true:接口执行成功，false:接口执行失败|
|errorCode|String|错误代码|当success为true时为空;当success为false时，显示错误代码|
|errorMsg|String|错误消息|当success为true时为空；当success为false时，显示接口执行异常消息|
|result|ResponseResult|接口返回数据|返回值以一个List和一个Long记录数据列表和总条数|

### 正常返回值说明

| 参数名 | 类型 | 说明 | 备注 |
| --- | --- | --- | --- | 
|success|Boolean|接口执行状态|正常执行为true|
|errorCode|String|错误代码|当success为true时为空|
|errorMsg|String|异常消息|正常执行时，errorMsg为空|
|result|Map|接口返回数据|返回值以一个List和一个Long记录数据列表和(分页)总条数|

#### result

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
|errorMsg|String|异常消息|错误执行时，errorMsg显示错误内容|
|result|ResponseResult|接口返回数据|为空|

### 错误返回值示例
错误返回值的demo

```
{
    "success": false,
    "errorCode": 200022,
    "errorMsg": "成员编码为空",
    "result":null
}
```

### 错误码说明

|错误代码|错误信息|说明|
| --- | --- | --- |
|200001|当前登录没有租户权限| 租户操作权限|
|200022|成员编码为空| 无|
|200023|成员姓名为空| 无|
|200024|邮箱与联系电话为空| 无|
|200025|成员状态为空| 无|
|200026|成员类型为空| 无|
|200027|性别为空| 无|
|200028|邮箱格式不正确| 无|
|200029|成员编码不符合规则| 无|
|200030|成员编码已存在| 无|
|200031|联系电话长度不符合| 无|
|200032|登录名已存在| 无|
|200033|手机号在该租户下已存在| 无|
|200034|日期格式不符合要求| 无|
|200035|证件类型不存在| 无|
|200036|性别类型不存在| 无|
|200037|成员类型不存在| 无|
|200038|成员状态不存在| 无|
|200039|公司名称不存在| 无|
|200040|邮箱地址在该租户下已存在| 无|
|200041|扩展字段不存在|无|
|200042|扩展字段重复|无|
|200043|扩展字段不能为空|无|
|300001|跨服务异常| 无|
