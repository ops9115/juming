# juming

##### 支付下单接口地址
> 测试环境:    http://apidemo.jumingpay.com.cn/api/payOrder/create

> 正式环境:    http://api.jumingpay.com.cn/api/payOrder/create

###### 支持格式
> JSON

###### HTTP请求方式
> POST

###### 签名算法说明
> sign算法说明：参数按键值+数值的ASCII编码顺序拼接，生成signData。使用RSA私钥，通过SHA1withRSA算法，RSA加密统一私钥加密，公钥解密。

###### signData示列
``` 

amount = 100&memberNo=100&merchantId=10001&merchantOrderNo=20190923162701&model=WECHAT_QR_CODE&notifyUrl=http://www.baidu.com&version=1.0.0

```

###### RSA私钥加密signData示列
``` 
sign -> TREA5bSFn62caXvs5PYGslrJdTWdtcE2iyOVzEcl28+YdxnsazP/gJRrfk0eilVtAcpHhvmUisjGQZRQUZewRd9PM33d2AwJ5waStpTPFxjp2H0lvrtPp234aupQBqISxf8PKdBYqBlFZUXtSujTNmKcXGQD0keZOGUE22lCc9Q=
```

###### 测试商户信息
```
//商户号
merchantId : 1001

//商户私钥
privateKey : MIICdQIBADANBgkqhkiG9w0BAQEFAASCAl8wggJbAgEAAoGBAK0zsS3BIDGbJoQXi1iJHVW935X7LnFomj+NW/+QCq6lA/siN8r28eG0/LonTUlpKK4b6gbuUadp9e3nW6bH5ODSfRGPLlM9OBWaN5Zs9norEVPK6XPPTfe/big6kqzGKU67z3zM8T070PVdnMALqoIq3Avz59k4MCe94osFfl8xAgMBAAECgYAdfbrCdqrbp3ZUcYnZhmdHTTA/4mgTCWOSRKiQiF85Q4G9BiOH3Kps6xtJOx3uzQgPNVOQ4I1ouyMT4hv59vligtw8L1knF5ty4YM8T4Zq+ooNW05H/Ns8lQUxdWnTnekX0THZeRH5BXqtRBGZw0inST0h1jMRJ6TRzpO4Zlr7PQJBANZowaU6M9eCBYozUi3IRhBtoXro1mwLjYXmijlkcPx02fMNY3r/7U6wLYb19HAUm6a2l3ezWHPumpPiglKlP4cCQQDOzKSfP+MXMbomIRWuiv0jWzpYXHy9RncoWh0tIRZsP9pKxfANBGuJeo4Z/J84Ji/iZtvCLX9xUxFu+NS8OOmHAkAK6SPJi6+trNEpWjk5WTKvjVSlU4ntz5yxDq1EBGd3gV7B7pF8Zd+mnHKEpql8tp/BGROWJMtAgwjcs68cE4qrAkA/DWpMG+CTm9fT9FZ2B26zLweVFW37D9cY+JDYx7PcgYN/NObCMUzQeAuHpNyu9AW5k/8BL3oiBV/VZA0I7plVAkByXYQmtWjQPqJ8grFus/QsnpuzB9pwz00H7c+yoI8BgmikHKhBew1LOtK7cRyRspz9/W3oHPQ/c6rdi7WqVKD1

//平台公钥
publicKey : MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQCRwmzgyPl3U7qU6YRRGEvGmW6Mlcb3KNSyo7S01PUAYbbN/iAOmBsuk9tcdCWumMGmSj+QY52X+Co2rdaPrXaBHYvwe9zWs2WmeBxmsMl1xmGviLqCn88a2hYeK2+f4XiMoqx+CeGl3Q9/I/uyTiLqcL/Jw3QgTHngFMQ9LXQYqwIDAQAB

```

###### 请求参数
> |参数|必选| 参数名称|说明|
> |:-----  | :-------| :-----| :-----                               |
> |merchantId    |ture    |商户id|平台给定商户唯一标识                          |
> |version    |true    |版本号	   |版本号，固定1.0.0|
> |merchantOrderNo    |ture    |商户订单号|商户订单id                        |
> |amount    |true    |金额   |单位：元|
> |model    |ture    |模式|详见末尾模式说明                         |
> |bankCode |false | 银行编码| --当模式是网银支付(E_BANK)时 必填|
> |memberNo    |false    |商户会员号   |注意：会员号“.”是为商户自身预留的特殊会员号，请勿使用于普通会员，如刚好出现会员号为“.”的，请进行替换。模式为银联在线时必填。|
> |notifyUrl    |true    |通知地址   |订单成功后的回调通知地址|
> |sign    |true    |签名   |详见签名说明|

###### 请求参数示例
``` javascript
{
    "amount":"100",
    "memberNo":"100",
    "merchantId":"10001",
    "merchantOrderNo":"20190923162701",
    "model":"UPOP",
    "notifyUrl":"http://www.baidu.com",
    "sign":"LM/ppSKQWh5qRNlvCoCm3d7naiOYBeZ0y4chZlJbCoM+pR4mIAF9Z4ymqn0dOF+Mn7+6fS7FPYC3kg9O7nOftD07OTOR7ul2GB8gm3T+b4rnk5+7qIFSdBlbgieEnCsPuzk2NQ68uCWh+PKbOs0liffai5cIpewX4P7j/THdVAs=",
    "version":"1.0.0"
}
```
###### 响应参数説明
> |参数|必选|参数名称|说明|
>|:-----  |:-------|:-----|-----                               |
>|code    |ture    |响应状态码|0为请求成功                        |
>|message    |true    |响应信息描述	   |例：操作成功|
>|merchantOrderNo    |ture    |商户订单号|商户订单id                        |
>|amount    |true    |金额   |单位：元|
>|merchantId    |true    |商户id   |平台给定商户唯一标识 |
>|url    |true    |支付地址 |跳转支付页面的地址 |
>|sign    |true    |签名   |商户进行验签|

##### 响应参数示例
``` javascript
{
	"amount":"100",
	"code":"0",
	"merchantOrderNo":"20190923162701",
	"msg":"操作成功",
	"sign":"TpmTdOlHiEw/57kQVvRj9MLMZocPUWD45CV71Vz+WGs+LIUH8tWX6W3JQUmbJ2Ohr/LHx3Q7R56butGPgRNGWvEPtx5JVArpNNXj6LG+jS3+HxIvxBgGUzO1N4RuCcLkB8xIZnMVhnQyGmzooiEOkzPYIdfYEKqKPOc9o3RMI3w=",
	"url":"http://120.24.145.9:80/upop-pay?orderNo=202007091247411000096"
}
```

##### 支付查询接口地址
> 测试环境：     http://apidemo.jumingpay.com.cn/api/payOrder/query

> 正式环境：     http://api.jumingpay.com.cn/api/payOrder/query

###### 支持格式
> JSON

###### HTTP请求方式
> POST

###### 请求参数说明
> |参数|必选|参数名称|说明|
>|:-----  |:-------|:-----|-----                               |
>|merchantId    |ture    |商户id|平台给定商户唯一标识                          |
>|version    |true    |版本号	   |版本号，固定1.0.0|
>|merchantOrderNo    |ture    |商户订单号|商户订单id                        |
>|submitTime    |true    |订单提交时间   |格式：yyyyMMddHHmmss(不要求强一致，偏差一小时以内)|
>|sign    |true    |签名   |详见签名说明|
######  请求参数示例
``` javascript
{
    "merchantId":"10001",
    "merchantOrderNo":"20190923162701",
    "sign":"M7i3zi7sHIni4bUchw7DsPfMltaCzUxP9gPeeSTfL0k7uMLL7lsAUz20wxP75+2eMCQ69V7qvk5Wh+O0hGqO42yiN0VbK/A8ucpQbF/Pw/llUi4tCP1bqQYQSa+2rdQuoNJR1rxR8viQw0RulO3wdhgqCBajsBXFg2QMxah9nRs=","submitTime":"20200709125837",
    "version":"1.0.0"
}
```

###### 响应参数说明
> |参数|必选|参数名称|说明|
>|:-----  |:-------|:-----|-----                               |
>|code    |ture    |响应状态码|0为请求成功                        |
>|message    |true    |响应信息描述	   |例：操作成功|
>|merchantOrderNo    |ture    |商户订单号|商户订单id                        |
>|amount    |true    |金额   |单位：元|
>|merchantId    |true    |商户id   |平台给定商户唯一标识 |
>|sign    |true    |签名   |商户进行验签|
>|status    |true    |订单支付状态   |订单状态：0：处理中，1：成功，2：失败|
###### 响应参数示例
``` javascript
{
	"amount":"100",
	"code":"0",
	"merchantOrderNo":"20190923162701",
	"msg":"操作成功",
	"sign":"U46X6XQ81Kq0POxFmyRmbN+hun//rwbEQfbs/SD5mGUquS+/HJT4JXZx9W4ev/2tvoASsxn8uHoBITXfKK4zs0JdSgtv8h0BItcyL3hSpZoiSZqQqa6hQ2pHjgDjqRjBmqCpzlLFxqdNaz7ET7rp8408VbwlNcXn/SSIZeTdBh8=",
	"status":"0"
}
```
##### 异步回调参数说明
> |参数|必选|参数名称|说明|
>|:-----  |:-------|:-----|-----                               |
>|merchantOrderNo    |ture    |商户订单号|                        |
>|message    |false    |响应信息描述	   |例：操作成功|
>|amount    |true    |金额   |单位：元|
>|sign    |true    |签名   |商户进行验签|
>|status    |true    |订单支付状态   |订单状态：0：处理中，1：成功，2：失败|

>回调验证成功后返回 success 字符串
##### 余额查询
> 测试环境：  http://apidemo.jumingpay.com.cn/api/balance/query

> 正式环境：  http://api.jumingpay.com.cn/api/balance/query

###### 支持格式
> JSON

###### HTTP请求方式
> POST

###### 请求参数说明
> |参数|必选|参数名称|说明|
>|:-----  |:-------|:-----|-----                               |
>|merchantId    |ture    |商户id|平台给定商户唯一标识                          |
>|version    |true    |版本号	   |版本号，固定1.0.0|
>|requestTime    |ture    |请求时间|格式：yyyyMMddHHmmss(不要求强一致，偏差一小时以内)                       |
>|sign    |true    |签名   |详见签名规则说明|
######  请求参数示例
``` javascript
{
   "merchantId":"10001",
   "requestTime":"20200709133614",
   "sign":"gRrNbN7qOE9anwE0ienc6TcBA3qt7PuCYp6oXflrhmxrFad0ga5dFd8oaxKsFtmjQege3EhW3BvJpXHv1pRSCOAE4ZUpcv0908jRKVDuPmMIh1pehLZb9lbyuCmPW2AQvqoA9ROoWySgSmtHURaLBlWGliskk5ezM84Ao/0lov0=",
   "version":"1.0.0"
}
```
###### 响应参数说明
> |参数|必选|参数名称|说明|
>|:-----  |:-------|:-----|-----                               |
>|code    |ture    |响应状态码|0为请求成功                        |
>|msg    |true    |响应信息描述	   |例：操作成功|
>|availableAmount    |ture    |可用余额	|单位：元                      |
>|frozenAmount    |true    |冻结金额	   |单位：元|
>|unsettledAmount    |true    |未结算金额	 |单位：元 |
>|sign    |true    |签名   |商户进行验签|

###### 响应参数示例
``` javascript
{
	"availableAmount":"99798",
	"code":"0",
	"frozenAmount":"0",
	"msg":"操作成功",
	"sign":"FMfueuuSr+H+iiwwT/eNlX/NgzgjSykTDEsaRYvmjQDU0rFZtSovgKlWvZJXdxqTt/mmkz+VHjt0q2bLDwqf9xkF1SvvEScEgdlmQjeDJi7yHwMFZ9/0TdttIqSNgmgLAy+/HXtrMEF3mDP9pNZuy3AqIQPTp6IBXyE8Xxt+m7w=",
	"unsettledAmount":"0"
}
```
##### 提现请求接口
> 测试环境:    http://apidemo.jumingpay.com.cn/api/remitOrder/create

> 正式环境:    http://api.jumingpay.com.cn/api/remitOrder/create

###### 支持格式
> JSON

###### HTTP请求方式
> POST

###### 请求参数说明
> |参数|必选|参数名称|说明|
>|:-----  |:-------|:-----|-----                               |
>|merchantId    |ture    |商户id|平台给定商户唯一标识                          |
>|version    |true    |版本号	   |版本号，固定1.0.0|
>|merchantOrderNo    |ture    |商户订单号|商户订单id                        |
>|amount    |true    |金额   |单位：元|
>|bankCode    |true    |银行编码   |详见末尾银行编码说明|
>|bankcardAccountNo    |true    |银行卡号   ||
>|bankcardAccountName    |true    |持卡人姓名   ||
>|notifyUrl    |true    |通知地址	   ||
>|sign    |true    |签名   |详见签名规则说明|
######  请求参数示例
``` javascript
{
   "amount":"100","bankCode":"ICBC",
   "bankcardAccountName":"电风扇",
   "bankcardAccountNo":"123456789123456789",
   "merchantId":"10001",
   "merchantOrderNo":"20190921202001",
   "notifyUrl":"http://www.baidu.com",
   "sign":"WhmHJ40Rwn4QcmbZllcj8wIFWEmdBPyIUof9pPtSzGrtJoGYFCmmnaYoz+3o234vnpGxfhMzF6RujAdfZwlplCfGci1mM9MhZhZHqcOttB1Ob9idbWNOKe0aR9bCtOB/Y1YXozm4X/WDSRoWLjklgvEMEWvGNunx1WAfCO/0a38=",
   "version":"1.0.0"
}
```
###### 响应参数说明
> |参数|必选|参数名称|说明|
>|:-----  |:-------|:-----|-----                               |
>|code    |ture    |响应状态码|0为请求成功                        |
>|message    |true    |响应信息描述	   |例：操作成功|
>|merchantOrderNo    |ture    |商户订单号|商户订单id                        |
>|amount    |true    |金额   |单位：元|
>|merchantId    |true    |商户id   |平台给定商户唯一标识 |
>|sign    |true    |签名   |商户进行验签|
>|status    |true    |订单支付状态   |订单状态：0：处理中，1：成功，2：失败|
###### 响应参数示例
``` javascript
{
	"amount":"100",
	"code":"0",
	"merchantOrderNo":"20190921202001",
	"msg":"操作成功",
	"sign":"Danpl6dGTaYj+rtN1YOVMbsMS2UaCUbzvgsGkZ7mbNkXD4eUleBzSLOB4mUjbOwgwNr/K3aMw9miUYwWHDEmkmWMj/rafJZcF4e8N1hrOHeowOMGnr7uJ2DpzUPoGJfybC/zslAIIHw/yXMwPrdV5DWNZIYzXDJQAB0x1xmiXZI=",
	"status":"0"
}
```

#### 提现订单查询接口
> 测试环境:   http://apidemo.jumingpay.com.cn/api/remitOrder/query

> 正式环境:   http://api.jumingpay.com.cn/api/remitOrder/query

###### 支持格式
> JSON

###### HTTP请求方式
> POST

###### 请求参数说明
> |参数|必选|参数名称|说明|
>|:-----  |:-------|:-----|-----                               |
>|merchantId    |ture    |商户id|平台给定商户唯一标识                          |
>|version    |true    |版本号	   |版本号，固定1.0.0|
>|merchantOrderNo    |ture    |商户订单号|商户订单id                        |
>|submitTime    |true    |订单提交时间   |格式：yyyyMMddHHmmss(不要求强一致，偏差一小时以内)|
>|sign    |true    |签名   |详见签名规则说明|

######  请求参数示例
``` javascript
{
    "merchantId":"10001",
    "merchantOrderNo":"20190921202001",
    "sign":"YvyuzpGb7cjC86USCFW4FQosNXUIxAXfPHODpcKEHnvKBQfKvrieBjCT6ZyhXrds6jaxk4R4Eztm76XdUoairrGIhvAfwIFdRpYY7yisdn0BDhbaMZXonYVyyC7m4hXnAajYoFNpT71tWWq6ov2eBN+PJdDbHc0ULKkry8fbess=",
    "submitTime":"20200709133438",
    "version":"1.0.0"
}
```
###### 响应参数说明
> |参数|必选|参数名称|说明|
>|:-----  |:-------|:-----|-----                               |
>|code    |ture    |响应状态码|0为请求成功                        |
>|message    |true    |响应信息描述	   |例：操作成功|
>|merchantOrderNo    |ture    |商户订单号|商户订单id                        |
>|amount    |true    |金额   |单位：元|
>|merchantId    |true    |商户id   |平台给定商户唯一标识 |
>|sign    |true    |签名   |商户进行验签|
>|status    |true    |订单支付状态   |订单状态：0：处理中，1：成功，2：失败|
###### 响应参数示例
``` javascript
{
	"amount":"100",
	"code":"0",
	"merchantOrderNo":"20190921202001",
	"msg":"操作成功",
	"sign":"Danpl6dGTaYj+rtN1YOVMbsMS2UaCUbzvgsGkZ7mbNkXD4eUleBzSLOB4mUjbOwgwNr/K3aMw9miUYwWHDEmkmWMj/rafJZcF4e8N1hrOHeowOMGnr7uJ2DpzUPoGJfybC/zslAIIHw/yXMwPrdV5DWNZIYzXDJQAB0x1xmiXZI=",
	"status":"0"
}
```
#### 代付反查

###### 反查参数说明
> |参数|必选|参数名称|说明|
>|:-----  |:-------|:-----|-----                               |
>|merchantOrderNo    |ture    |商户订单号|商户订单id                        |
>|amount    |true    |金额   |单位：元|
>|merchantId    |true    |商户id   |平台给定商户唯一标识 |
>|sign    |true    |签名   |商户进行验签|
>|bankcardAccountNo    |true    |银行卡号   ||
###### 响应参数说明参数说明
> |参数|必选|参数名称|说明|
>|:-----  |:-------|:-----|-----                               |
>|merchantOrderNo    |ture    |商户订单号|商户订单id                        |
>|code    |true    |操作状态	   |返回0操作成功其它为失败|
>|message    |true    |操作描述   |操作描述 （成功或者失败） |
>|sign    |true    |签名   |商户进行验签|


#### 银行编码说明
````
工商银行	ICBC
建设银行	CCB
农业银行	ABC
邮政储蓄银行	PSBC
中国银行	BOC
交通银行	COMM
招商银行	CMB
光大银行	CEB
兴业银行	CIB
民生银行	CMBC
北京银行	BCCB
中信银行	CITIC
广东发展银行	GDB
深圳发展银行	SDB
浦东发展银行	SPDB
平安银行	PINGANBANK
华夏银行	HXB
上海银行	SHB
渤海银行	CBHB
东亚银行	HKBEA
宁波银行	NBCB
浙商银行	CZB
南京银行	NJCB
杭州银行	HZCB
北京农村商业银行	BJRCB
上海农商银行	SRCB
````

#### 支付模式说明
````
UPOP：银联在线

ALIPAY_QR_CODE:支付宝二维码

ALIPAY_WAP：支付宝wap

WECHAT_QR_CODE：微信二维码

WECHAT_WAP：微信wap

POINT_CARD：点卡

E_BANK：网银支付
````
