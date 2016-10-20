![深信社 icon](http://www.sxfax.com/images/v2/logo.png)

# 深信社APP

数据统一返回JSON格式：

	正确：{"success": true, "message": "", "model": null}
	错误：{"success": false, "message": "手机号码不存在", "model": null}

如果响应Headers中AppLoginStatus=appLoginTimeOut时，必须登陆

Action约定：

	action		动作
	push		内置Activity打开：LoginActivity、RegistActivity
	inside		内置浏览器打开
	outside		外置浏览器打开
	dial		拨打电话
	app			打开应用

渠道定义

渠道			| 应用商店		| 应用类型	| 名称
-----------	| -------------	| ---------	| ----
百度系      	| 百度手机助手	| 安卓		| baidu101
百度系		| 91手机助手		| 安卓		| baidu102
百度系		| 安卓市场		| 安卓		| baidu103
腾讯系		| 广点通			| 安卓		| qq101
腾讯系		| 应用宝			| 安卓		| qq102
360			| 360手机助手	| 安卓		| 360sj101
360			| 360手机卫士	| 安卓		| 360sj102
华为			| 华为应用市场	| 安卓		| huaw101
小米			| 小米商店		| 安卓		| xiaom101
PP助手		| PP助手			| 安卓、IOS	| pp101、pp201
豌豆荚		| 豌豆荚			| 安卓		| wandou101
应用汇		| 应用汇			| 安卓		| yingy101	

appChannel

#### 6.1.1 APP安装量统计

> 说明：

1. 请求地址：Post `http://sfax.softoptimus.com:8080/app/count/installedCount`

2. 请求参数

	参数				| 名称				| 说明
	---------------	| -----------------	| ---
	appChannel      | 渠道名称			| 	

3. 响应

	参数				| 名称     		| 说明
	---------------	| -------------	| ---
	success        	| 是否成功 		|


#### 6.1.2 APP系统公告

> 说明：

1. 请求地址：Post `http://sfax.softoptimus.com:8080/app/notices`

2. 请求参数

	参数				| 名称				| 说明
	---------------	| -----------------	| ---
	

3. 响应


	参数				| 名称     		| 说明
	---------------	| -------------	| ---
	success        	| 是否成功 		|    
	message      	| 提示信息     	| 如果success为false，就会有提示信息
	notice			| 公告数组		| 存放具体数据
	title 			| 公告标题     	|
	url 			| 公告链接     	|
	more 			| 公告更多链接    |


数据格式：
	notice{
  	"list": [
    {
      "title": "标题1",
      "url": "详情链接1"
    },
    {
      "title": "标题2",
      "url": "详情链接2"
    },
    {
      "title": "标题3",
      "url": "详情链接3"
    }
  	],
  	"more": "更多H5链接"
	}
	



## 1 首页

### 1.1 广告轮播图    `专业扩展版无法显示，因为文档到这里已经超长了导致。`

> 说明：
>  
>	1. 广告图后台传参数，控制点击动作：
>	
>		注册：{"action": "push", "url": "RegistActivity"}
>		
>		跳转到H5页面：{"action": "inside", "url"www.baidu.com"}
>		
>	2. CMS新建栏目：中文名称＝APP轮播图	，英文名称＝APP_CAROUSEL
>
>	3. APP轮播图栏目添加文章：
>		内容需要添加action：push/inside



1. 请求地址：Post `http://sfax.softoptimus.com:8080/app/banners`

2. 请求参数

	参数				| 名称				| 说明
	---------------	| -----------------	| ---
	imei           	| 手机串号			| 		

3. 响应

	参数				| 名称     		| 说明
	---------------	| -------------	| ---
	success        	| 是否成功 		|    
	message      	| 提示信息     	| 如果success为false，就会有提示信息
	model			| 				| 存放具体数据
	recordsTotal 	| 总共记录数     	|                               
	data			| 广告轮播图数组	|
	title			| 活动标题		|
	parent			| 图片地址		| 图片地址
	url				| 跳转链接		| 
	publishDate		| 发布时间		|
	recordTime		| 创建记录时间	| 


### 1.2 新手标

> 说明：
> 
> 1. 字段testLoan为false，不可投，按钮显示为禁用
> 
> 2. 字段status=OPEN，按钮显示`立即投标`；status=SCHEDULED, 按钮显示`倒计时`，倒计时的算法根据开标时间和服务器时间计算。
> 
> 3. status字典：PROPOSED待审核,REJECTED未通过,APPROVED已存档,SCHEDULED即将发布,OPEN立即投标,FAILED已截止,FINISHED已满标,CANCELED已取消,LOANED还款中,CLEARED已还清,OVERDUE: 已逾期。
> 
> 4. 还款方式repayMethod字典：
> 	INTEREST: "先息后本",
    EQUAL_INSTALLMENT: "等额本息",
    EQUAL_PRINCIPAL: "等额本金",
    BULLET_REPAYMENT: "一次性还款"
>
> 5. newbeeTime新手标可投次数如果等于-1，不显示`可投次数`    


1. 请求地址：Post `http://sfax.softoptimus.com:8080/app/newbee`

2. 请求参数

	参数				| 名称				| 说明
	---------------	| -----------------	| ---
	imei           	| 手机串号			| 		

3. 响应

	参数				| 名称     		| 说明
	---------------	| -------------	| ---
	success        	| 是否成功 		|    
	message      	| 提示信息     	| 如果success为false，就会有提示信息
	model			| 				| 存放具体数据
	serverTime	 	| 服务器时间     	|                               
	testLoan		| 新手标是否可投	| 
	newbeeTime		| 新手标可投次数	| 
	newbeeAmount	| 新手标可投金额	| 
	investRule		| 投标规则		| 
	minAmount		| 最小投标金额	| 
	maxAmount		| 最大投标金额	| 
	stepAmount		| 投标递增金额	| 
	openTime		| 开标时间		| 
	timeOut			| 筹款时长		| 
	duration		| 期限			| 期限的算法见`3.10.1`接口
	days			| 天数			| 
	years			| 年				| 
	months			| 月				| 
	title			| 标题			| 
	repayMethod		| 还款方式		| 
	rate			| 利率			| 
	amount			| 标的金额		| 
	status			| 状态			| 


### 1.3 

1. 请求地址：Post `http://sfax.softoptimus.com:8080/app/banners`

2. 请求参数

	参数				| 名称				| 说明
	---------------	| -----------------	| ---
	imei           	| 手机串号			| 		

3. 响应

	参数				| 名称     		| 说明
	---------------	| -------------	| ---
	success        	| 是否成功 		|    
	message      	| 提示信息     	| 如果success为false，就会有提示信息
	model			| 				| 存放具体数据
	recordsTotal 	| 总共记录数     	|                               
	data			| 广告轮播图数组	|
	title			| 活动标题		|
	parent			| 图片地址		| 图片地址
	url				| 跳转链接		| 
	publishDate		| 发布时间		|
	recordTime		| 创建记录时间	| 


## 2 投资理财

### 2.1 投资列表

> 说明：
> 
> 1. 标的的进度：(amount-leftAmount)/amount,结果小于1%大于0，显示1%；结果大于99%小于100%，显示99%

1. 请求地址：Post `http://sfax.softoptimus.com:8080/app/filterLoans`

2. 请求参数

	参数				| 名称				| 说明
	---------------	| -----------------	| ---
	imei           	| 手机串号			| 
	start			| 分页起始记录		| 
	length			| 每页记录数			| 

3. 响应

	参数				| 名称     		| 说明
	---------------	| -------------	| ---
	success        	| 是否成功 		|    
	message      	| 提示信息     	| 如果success为false，就会有提示信息
	model			| 				| 存放具体数据
	recordsTotal 	| 总共记录数     	|                               
	data			| 交易记录数组	|
	id				| ID			| 2.2、2.3、2.4、2.5、2.6、2.7等接口需要用到
	title			| 标题			| 
	repayMethod		| 还款方式		| 字典见`新手标`
	amount			| 项目金额		| 单位：元
	rate			| 年化利率		| 显示除100
	additionalRate	| 加息			| 显示除100 
	duration		| 期限			| 期限的算法见`3.10.1`接口
	status			| 状态			| 见`新手标`
	timeOut			| 筹款时长		| 
	openTime		| 开标时间		| 倒计时见`新手标`说明
	investRule		| 投标规则		| 
	minAmount		| 最小投标金额	| 
	maxAmount		| 最大投标金额	| 
	stepAmount		| 投标递增金额	| 
	leftAmount		| 标的剩余金额	| 


### 2.2 投资页面

> 说明：

1. 请求地址：Post `http://sfax.softoptimus.com:8080/app/loan`

2. 请求参数

	参数				| 名称				| 说明
	---------------	| -----------------	| ---
	imei           	| 手机串号			| 
	loanId			| 标的ID				| 

3. 响应

	参数				| 名称     		| 说明
	---------------	| -------------	| ---
	success        	| 是否成功 		|    
	message      	| 提示信息     	| 如果success为false，就会有提示信息
	model			| 				| 存放具体数据
	title			| 标题			| 
	repayMethod		| 还款方式		| 字典见`新手标`
	amount			| 项目金额		| 单位：元
	rate			| 年化利率		| 显示除100 
	additionalRate	| 加息			| 显示除100 
	duration		| 期限			| 期限的算法见`3.10.1`接口
	status			| 状态			| 见`新手标`
	timeOut			| 筹款时长		| 
	openTime		| 开标时间		| 倒计时见`新手标`说明
	investRule		| 投标规则		| 
	minAmount		| 最小投标金额	| 
	maxAmount		| 最大投标金额	| 
	stepAmount		| 投标递增金额	| 
	canInvest		| 是否可以投资	| 
	contract		| 合同号			| 查看投资协议需要传这个参数
	

### 2.3 项目详情

1. 请求地址：Get `http://sfax.softoptimus.com:8080/m/loan/info/{loanId}?app=1`

2. 请求参数

	参数				| 名称				| 说明
	---------------	| -----------------	| ---
	imei           	| 手机串号			| 
	loanId			| 标的ID				| 参数放在路径中

3. 响应：html页面


### 2.4 标的投资记录

> 说明：

1. 请求地址：Post `http://sfax.softoptimus.com:8080/app/loan/invests`

2. 请求参数

	参数				| 名称				| 说明
	---------------	| -----------------	| ---
	imei           	| 手机串号			| 
	loanId			| 标的ID				| 

3. 响应

	参数				| 名称     		| 说明
	---------------	| -------------	| ---
	success        	| 是否成功 		|    
	message      	| 提示信息     	| 如果success为false，就会有提示信息
	model			| 				| 存放具体数据
	totalSize		| 记录条数		| 
	result			| 投资记录数组	| 
	investor		| 投资者			| 
	amount			| 金额			| 
	investTime		| 投资时间		| 
	status			| 状态			| 
	

### 2.5 投资协议

> 说明：

1. 请求地址：Get `http://sfax.softoptimus.com:8080/app/loan/contract`

2. 请求参数

	参数				| 名称				| 说明
	---------------	| -----------------	| ---
	imei           	| 手机串号			| 
	template       	| 合同号				| 
			

3. 响应：html页面

### 2.6 新手标项目详情

见`1.2 新手标`


### 2.7 投标

> 说明：跳转到汇付

1. 请求地址：Get `http://sfax.softoptimus.com:8080/app/pnr/invest`

2. 请求参数

	参数				| 名称				| 说明
	---------------	| -----------------	| ---
	imei           	| 手机串号			| 
	loanId			| 标的ID				| 
	amount			| 投标金额			|
	appChannel      | 渠道名称			| 		

3. 响应：html页面


## 3 我的账户

### 3.1 我的资产

> 说明：
> 1. 进入这个视图，就请求这个地址拿到数据 
> 
> 2. 总资产=冻结金额+待收本息+可用余额

1. 请求地址：Post `http://sfax.softoptimus.com:8080/app/user/assets`

2. 请求参数

	参数				| 名称				| 说明
	---------------	| -----------------	| ---
	imei           	| 手机串号			| 

3. 响应

	参数				| 名称     		| 说明
	---------------	| -------------	| ---
	success        	| 是否成功 		|    
	message      	| 提示信息     	| 如果success为false，就会有提示信息
	model			| 				| 存放具体数据
	ticketsCount	| 奖励个数		| 
	level			| 账户安全级别	| 
	bankCards		| 银行卡张数		| 
	refCount		| 一代推广人数	| 
	totalCommission	| 推广收益		| 单位：元
	undueInvestCount	| 待还款笔数	| 
	fund.frozen 	| 冻结金额     	| 单位：元
	fund.receivable	| 待收本息		| 单位：元
	fund.available	| 可用余额		| 单位：元
	account			| 汇付账户		| 如果等于null,显示开通托管账户，否则显示交易记录
	account.usrCustId	| 汇付账号	| 
	user.mobile		| 认证手机		| 
	user.name		| 姓名			| 
	user.refGrade	| 推荐级别		| 理财师
	user.type		| 用户类型		| 业主用户、员工用户、普通用户
	user.refCode	| 推荐码			| 
	

### 3.2 交易记录

> 说明：

1. 请求地址：Post `http://sfax.softoptimus.com:8080/app/user/funds`

2. 请求参数

	参数				| 名称				| 说明
	---------------	| -----------------	| ---
	imei           	| 手机串号			| 
	start			| 分页起始记录		| 
	length			| 每页记录数			| 

3. 响应

	参数				| 名称     		| 说明
	---------------	| -------------	| ---
	success        	| 是否成功 		|    
	message      	| 提示信息     	| 如果success为false，就会有提示信息
	model			| 				| 存放具体数据
	recordsTotal 	| 总共记录数     	|                               
	data			| 交易记录数组	|
	time			| 时间			| 
	desc			| 相关信息		| 
	amount			| 金额			| 单位：元
	type			| 类型			|
	status			| 状态			|  


### 3.3 开户

> 说明：跳转到汇付，在我的账户页面，如果用户没有开户显示开户的链接，没有已开户显示交易记录

1. 请求地址：Get `http://sfax.softoptimus.com:8080/app/pnr/account`

2. 请求参数

	参数				| 名称				| 说明
	---------------	| -----------------	| ---
	imei           	| 手机串号			| 		

3. 响应：html页面


### 3.4 注销

> 说明：

1. 请求地址：Post `http://sfax.softoptimus.com:8080/app/logout`

2. 请求参数

	参数				| 名称				| 说明
	---------------	| -----------------	| ---
	imei           	| 手机串号			| 		

3. 响应

	参数				| 名称     		| 说明
	---------------	| -------------	| ---
	success        	| 是否成功 		|    


### 3.5 充值

> 说明：跳转到汇付

1. 请求地址：Get `http://sfax.softoptimus.com:8080/app/pnr/deposit`

2. 请求参数

	参数				| 名称				| 说明
	---------------	| -----------------	| ---
	imei           	| 手机串号			| 	
	amount			| 充值金额			| 单位：元
	appChannel      | 渠道名称			|	
3. 响应：html页面


### 3.6 提现

> 说明：跳转到汇付

1. 请求地址：Get `http://sfax.softoptimus.com:8080/app/pnr/withdraw`

2. 请求参数

	参数				| 名称				| 说明
	---------------	| -----------------	| ---
	imei           	| 手机串号			| 	
	amount			| 充值金额			| 单位：元
	appChannel      | 渠道名称			|	
3. 响应：html页面


### 3.7 我的银行卡

#### 3.7.1 我的所有银行卡

> 说明：
> 
> 1. 银行代码字典：
> 	ICBC("中国工商银行"),
    ABC("中国农业银行"),
    CMB("招商银行"),
    CCB("建设银行"),
    BCCB("北京银行"),
    BJRCB("北京农村商业银行"),
    BOC("中国银行"),
    BOCOM("交通银行"),
    CMBC("民生银行"),
    BOS("上海银行"),
    CBHB("渤海银行"),
    CEB("光大银行"),
    CIB("兴业银行"),
    CITIC("中信银行"),
    CZB("浙商银行"),
    GDB("广发银行"),
    HKBEA("东亚银行"),
    HXB("华夏银行"),
    HZCB("杭州银行"),
    NJCB("南京银行"),
    PINGAN("平安银行"),
    PSBC("邮政储蓄银行"),
    SDB("深发银行"),
    SPDB("浦发银行"),
    SRCB("上海农村商业银行"),
    WZCB("温州银行");

1. 请求地址：Post `http://sfax.softoptimus.com:8080/app/user/bankCards`

2. 请求参数

	参数				| 名称				| 说明
	---------------	| -----------------	| ---
	imei           	| 手机串号			| 		

3. 响应

	参数				| 名称     		| 说明
	---------------	| -------------	| ---
	success        	| 是否成功 		|    
	message      	| 提示信息     	| 如果success为false，就会有提示信息
	model			| 				| 存放具体数据
	account		 	| 银行卡号     	| 
	defaultAccount 	| 默认账户     	| true是，false否      
	name		 	| 持卡人姓名  	| 
	valid		 	| 是否有效     	| 
	bank		 	| 银行代码     	|        
	bankName		| 银行名称		|         
	express			| 是否为快捷卡	|        


#### 3.7.2 添加银行卡

> 说明：跳转到汇付

1. 请求地址：Get `http://sfax.softoptimus.com:8080/app/pnr/bindCard`

2. 请求参数

	参数				| 名称				| 说明
	---------------	| -----------------	| ---
	imei           	| 手机串号			| 		

3. 响应：html页面


#### 3.7.3 解绑银行卡

> 说明：默认取现卡不能解绑

1. 请求地址：Post `http://sfax.softoptimus.com:8080/app/pnr/unbindBankAccount`

2. 请求参数

	参数				| 名称				| 说明
	---------------	| -----------------	| ---
	imei           	| 手机串号			| 
	cardId			| 银行卡号			| 
			

3. 响应

	参数				| 名称     		| 说明
	---------------	| -------------	| ---
	success        	| 是否成功 		|    
	message      	| 提示信息     	| 
	model			| 				| 存放具体数据


### 3.8 我的奖励

#### 3.8.1 我的可提取奖励

> 说明：如果提取金额大于100元，会变成审核中的金额

1. 请求地址：Post `http://sfax.softoptimus.com:8080/app/account/rewards/invoked`

2. 请求参数

	参数				| 名称				| 说明
	---------------	| -----------------	| ---
	imei           	| 手机串号			| 		

3. 响应

	参数				| 名称     		| 说明
	---------------	| -------------	| ---
	success        	| 是否成功 		|    
	message      	| 提示信息     	| 如果success为false，就会有提示信息
	model			| 				| 存放具体数据
	qualified	 	| 可提取奖励金额 	| 单位：元
	invoked			| 审核中的金额	| 单位：元                              


#### 3.8.3 提取奖励

> 说明：点击提取按钮，提示用户`确定申请提现所有红包？`

1. 请求地址：Post `http://sfax.softoptimus.com:8080/app/coupon/invokeCoupons`

2. 请求参数

	参数				| 名称				| 说明
	---------------	| -----------------	| ---
	imei           	| 手机串号			| 		

3. 响应

	参数				| 名称     		| 说明
	---------------	| -------------	| ---
	success        	| 是否成功 		|    
	message      	| 提示信息     	|   



下面4个接口，是同一个接口，只是状态status填不同的值

#### 3.8.4 已激活奖励

> 说明：

1. 请求地址：Post `http://sfax.softoptimus.com:8080/app/coupon/listCoupons`

2. 请求参数

	参数				| 名称				| 说明
	---------------	| -----------------	| ---
	imei           	| 手机串号			| 
	start			| 分页起始记录		| 
	length			| 每页记录数			| 
	status			| 状态				| 填QUALIFIED

3. 响应

	参数				| 名称     		| 说明
	---------------	| -------------	| ---
	success        	| 是否成功 		|    
	message      	| 提示信息     	| 如果success为false，就会有提示信息
	model			| 				| 存放具体数据
	recordsTotal 	| 总共记录数     	|                               
	data			| 红包数组		|
	pack.type		| 红包类型		| CASH现金券，REDBAG投资返现
	originalBonus	| 金额			| 单位：元
	pack.name		| 红包名称		| 如：注册奖励
	allocatedTime	| 激活日期		| pack.type='CASH'使用此字段
	invokedTime		| 激活日期		| pack.type='REDBAG'使用此字段
	target.objectId	| 激活项目		| pack.type='REDBAG'使用此字段

	
#### 3.8.5 未激活奖励

> 说明：

1. 请求地址：Post `http://sfax.softoptimus.com:8080/app/coupon/listCoupons`

2. 请求参数

	参数				| 名称				| 说明
	---------------	| -----------------	| ---
	imei           	| 手机串号			| 
	start			| 分页起始记录		| 
	length			| 每页记录数			| 
	status			| 状态				| 填ALLOCATED

3. 响应

	参数				| 名称     		| 说明
	---------------	| -------------	| ---
	success        	| 是否成功 		|    
	message      	| 提示信息     	| 如果success为false，就会有提示信息
	model			| 				| 存放具体数据
	recordsTotal 	| 总共记录数     	|                               
	data			| 红包数组		|
	pack.type		| 红包类型		| REDBAG投资返现
	originalBonus	| 金额			| 单位：元
	pack.name		| 红包名称		| 如：投资红包
	expiredTime		| 到期日			| 
	actualBonus		| 激活条件		| 单笔投资满X元，X=actualBonus*200	
	
#### 3.8.6 已提取奖励

> 说明：

1. 请求地址：Post `http://sfax.softoptimus.com:8080/app/coupon/listCoupons`

2. 请求参数

	参数				| 名称				| 说明
	---------------	| -----------------	| ---
	imei           	| 手机串号			| 
	start			| 分页起始记录		| 
	length			| 每页记录数			| 
	status			| 状态				| 填PAYING

3. 响应

	参数				| 名称     		| 说明
	---------------	| -------------	| ---
	success        	| 是否成功 		|    
	message      	| 提示信息     	| 如果success为false，就会有提示信息
	model			| 				| 存放具体数据
	recordsTotal 	| 总共记录数     	|                               
	data			| 红包数组		|
	pack.type		| 红包类型		| CASH现金券，REDBAG投资返现
	originalBonus	| 金额			| 单位：元
	pack.name		| 红包名称		| 如：注册奖励
	consumedTime	| 提取日期		| 
	target.objectId	| 激活项目		| pack.type='REDBAG'使用此字段	
				
#### 3.8.7 已过期奖励

> 说明：

1. 请求地址：Post `http://sfax.softoptimus.com:8080/app/coupon/listCoupons`

2. 请求参数

	参数				| 名称				| 说明
	---------------	| -----------------	| ---
	imei           	| 手机串号			| 
	start			| 分页起始记录		| 
	length			| 每页记录数			| 
	status			| 状态				| 填EXPIRED

3. 响应

	参数				| 名称     		| 说明
	---------------	| -------------	| ---
	success        	| 是否成功 		|    
	message      	| 提示信息     	| 如果success为false，就会有提示信息
	model			| 				| 存放具体数据
	recordsTotal 	| 总共记录数     	|                               
	data			| 红包数组		|
	pack.type		| 红包类型		| CASH现金券，REDBAG投资返现
	originalBonus	| 金额			| 单位：元
	pack.name		| 红包名称		| 如：投资红包
	expiredTime		| 过期日			| 	


### 3.9 账户安全

#### 3.9.1 修改登陆密码

> 说明：

1. 请求地址：Post `http://sfax.softoptimus.com:8080/app/changePassword`

2. 请求参数

	参数				| 名称				| 说明
	---------------	| -----------------	| ---
	imei           	| 手机串号			| 	
	oldPwd			| 旧密码				| 
	newPwd			| 新密码				| 

3. 响应

	参数				| 名称     		| 说明
	---------------	| -------------	| ---
	success        	| 是否成功 		|  


### 3.10 我的投资

下面3个接口，其实是一个接口，只是参数状态status不同

#### 3.10.1 投标中

> 说明：
> 
> 1. 期限的算法：
> 	loan.duration.days != 0 --> 取 loan.duration.totalDays天
> 	loan.duration.days == 0 --> 取 loan.duration.totalMonths个月

1. 请求地址：Post `http://sfax.softoptimus.com:8080/app/user/invests`

2. 请求参数

	参数				| 名称				| 说明
	---------------	| -----------------	| ---
	imei           	| 手机串号			| 
	start			| 分页起始记录		| 
	length			| 每页记录数			| 
	status			| 状态				| 填FROZEN

3. 响应

	参数				| 名称     		| 说明
	---------------	| -------------	| ---
	success        	| 是否成功 		|    
	message      	| 提示信息     	| 如果success为false，就会有提示信息
	model			| 				| 存放具体数据
	recordsTotal 	| 总共记录数     	|                               
	data			| 投资数组		|
	loan.title		| 标的名称		| 
	loan.rate		| 年化利率		| 
	loan.duration.totalDays		| 期限-天	| 
	loan.duration.totalMonths	| 期限-个月	|
	loan.duration.days	| 期限-天数	| 
	invest.amount	| 投标金额		| 单位：元
	invest.investTime	| 投资时间	| 
	loan.repayMethod	| 还款方式	| 字典见`新手标`
	

#### 3.10.2 还款中

> 说明：
> 
> 1. 期限的算法：
> 	loan.duration.days != 0 --> 取 loan.duration.totalDays天
> 	loan.duration.days == 0 --> 取 loan.duration.totalMonths个月
>
> 2. status == 'LOANED'	时，还款中的投资显示：`还款计划`的链接

1. 请求地址：Post `http://sfax.softoptimus.com:8080/app/user/invests`

2. 请求参数

	参数				| 名称				| 说明
	---------------	| -----------------	| ---
	imei           	| 手机串号			| 
	start			| 分页起始记录		| 
	length			| 每页记录数			| 
	status			| 状态				| 填LOANED

3. 响应

	参数				| 名称     		| 说明
	---------------	| -------------	| ---
	success        	| 是否成功 		|    
	message      	| 提示信息     	| 如果success为false，就会有提示信息
	model			| 				| 存放具体数据
	recordsTotal 	| 总共记录数     	|                               
	data			| 投资数组		|
	loan.title		| 标的名称		| 
	loan.rate		| 年化利率		| 
	loan.duration.totalDays		| 期限-天	| 
	loan.duration.totalMonths	| 期限-个月	|
	loan.duration.days	| 期限-天数	| 
	invest.amount	| 投标金额		| 单位：元
	invest.investTime	| 投资时间	| 
	loan.repayMethod	| 还款方式	| 字典见`新手标`
	invest.id		| 投资id			| 查看还款计划需要传这个参数
			
#### 3.10.3 已还清

> 说明：
> 
> 1. 期限的算法：
> 	loan.duration.days != 0 --> 取 loan.duration.totalDays天
> 	loan.duration.days == 0 --> 取 loan.duration.totalMonths个月

1. 请求地址：Post `http://sfax.softoptimus.com:8080/app/user/invests`

2. 请求参数

	参数				| 名称				| 说明
	---------------	| -----------------	| ---
	imei           	| 手机串号			| 
	start			| 分页起始记录		| 
	length			| 每页记录数			| 
	status			| 状态				| 填CLEARED

3. 响应

	参数				| 名称     		| 说明
	---------------	| -------------	| ---
	success        	| 是否成功 		|    
	message      	| 提示信息     	| 如果success为false，就会有提示信息
	model			| 				| 存放具体数据
	recordsTotal 	| 总共记录数     	|                               
	data			| 投资数组		|
	loan.title		| 标的名称		| 
	loan.rate		| 年化利率		| 
	loan.duration.totalDays		| 期限-天	| 
	loan.duration.totalMonths	| 期限-个月	|
	loan.duration.days	| 期限-天数	| 
	invest.amount	| 投标金额		| 单位：元
	invest.investTime	| 投资时间	| 
	loan.repayMethod	| 还款方式	| 字典见`新手标`


#### 3.10.4 还款计划

> 说明：

1. 请求地址：Post `http://sfax.softoptimus.com:8080/app/invest/repays`

2. 请求参数

	参数				| 名称				| 说明
	---------------	| -----------------	| ---
	imei           	| 手机串号			| 
	id				| 投资ID				| 从我的投资-还款中返回的数据中获取

3. 响应

	参数				| 名称     		| 说明
	---------------	| -------------	| ---
	success        	| 是否成功 		|    
	message      	| 提示信息     	| 如果success为false，就会有提示信息
	model			| 				| 存放具体数据
	loanTitle	 	| 标的标题     	|                               
	data			| 投资数组		|
	period			| 期数			| 
	repayProfit		| 收益			| 
	status			| 状态			| 
	repayPrincipal	| 应收本金		| 
	dueDate.year	| 还款日期-年 	| 
	dueDate.monthValue	| 还款日期-月	| 
	dueDate.dayOfMonth	| 还款日期-日	|  


### 3.11 我的推广

#### 3.11.1 我的推广数据

> 说明：

1. 请求地址：Post `http://sfax.softoptimus.com:8080/app/account/promote`

2. 请求参数

	参数				| 名称				| 说明
	---------------	| -----------------	| ---
	imei           	| 手机串号			| 

3. 响应

	参数				| 名称     		| 说明
	---------------	| -------------	| ---
	success        	| 是否成功 		|    
	message      	| 提示信息     	| 如果success为false，就会有提示信息
	model			| 				| 存放具体数据
	confirmedCommission		| 可提取推广收益	| 单位：元
	payedCommission	| 已提取推广收益	| 单位：元
	initCommission	| 结算中推广收益	| 单位：元
	totalCommission	| 累积推广收益	| 单位：元
	invokedCommission	| 审核中的已提取推广收益	| 单位：元
	wxShare.title	| 分享到朋友圈标题	| 
	wxShare.link	| 分享到朋友圈链接	| 
	wxShare.imgUrl	| 分享到朋友圈图片	| 
	wxShare.titleSigle	| 微信发送给朋友标题	| 
	wxShare.descSigle	| 微信发送给朋友描述	| 
	wxShare.linkSigle	| 微信发送给朋友链接	| 
	wxShare.imgUrlSigle	| 微信发送给朋友图片	| 
	qqShare.desc	| 分享QQ标题	| 
	qqShare.link	| 分享QQ链接	| 
	qqShare.imgUrl	| 分享QQ图片	| 
	weiboShare.desc		| 分享微博标题	| 
	weiboShare.link		| 分享微博链接	| 
	weiboShare.imgUrl	| 分享微博图片	| 	


#### 3.11.2 三代推荐统计			

> 说明：直接推荐推广收益=直接推荐开户收益+直接推荐投资收益（二三代类同）

1. 请求地址：Post `http://sfax.softoptimus.com:8080/app/user/commissionStat`

2. 请求参数

	参数				| 名称				| 说明
	---------------	| -----------------	| ---
	imei           	| 手机串号			| 

3. 响应

	参数				| 名称     		| 说明
	---------------	| -------------	| ---
	success        	| 是否成功 		|    
	message      	| 提示信息     	| 如果success为false，就会有提示信息
	model			| 				| 存放具体数据
	r1o				| 直接推荐开户人数	| 
	r2o				| 二代推荐开户人数	| 
	r3o				| 三代推荐开户人数	| 
	r1i				| 直接推荐投资人数	| 
	r2i				| 二代推荐投资人数	| 
	r3i				| 三代推荐投资人数	| 
	r1cr			| 直接推荐开户收益	| 单位：元
	r2cr			| 二代推荐开户收益	| 单位：元
	r3cr			| 三代推荐开户收益	| 单位：元
	r1ci			| 直接推荐投资收益	| 单位：元
	r2ci			| 二代推荐投资收益	| 单位：元
	r3ci			| 三代推荐投资收益	| 单位：元


#### 3.11.3 我的二维码

> 说明

1. 请求地址：Get `http://sfax.softoptimus.com:8080/app/account/myQrcode`

2. 请求参数

	参数				| 名称				| 说明
	---------------	| -----------------	| ---
	imei           	| 手机串号			| 
	
3. 响应：图片	



## 4 其他


### 4.1 注册

#### 4.1.1 Step1: 发送验证码

> 说明：

1. 请求地址：Post `http://sfax.softoptimus.com:8080/app/register/step1`

2. 请求参数

	参数				| 名称				| 说明
	---------------	| -----------------	| ---
	imei           	| 手机串号			| 	
	mobile			| 手机号				|	

3. 响应

	参数				| 名称     		| 说明
	---------------	| -------------	| ---
	success        	| 是否成功 		|    

			
#### 4.1.2 Step2: 验证手机验证码

> 说明：

1. 请求地址：Post `http://sfax.softoptimus.com:8080/app/register/validate`

2. 请求参数

	参数				| 名称				| 说明
	---------------	| -----------------	| ---
	imei           	| 手机串号			| 	
	mobile			| 手机号码			| 
	mobileCaptcha	| 验证码				| 测试环境统一填`666666`	

3. 响应

	参数				| 名称     		| 说明
	---------------	| -------------	| ---
	success        	| 是否成功 		|    


#### 4.1.3 Step3: 输入密码

> 说明：

1. 请求地址：Post `http://sfax.softoptimus.com:8080/app/register/step2`

2. 请求参数

	参数				| 名称				| 说明
	---------------	| -----------------	| ---
	imei           	| 手机串号			| 
	mobile			| 手机号码			| 
	password		| 密码				|
	appChannel      | 渠道名称			| 		

3. 响应

	参数				| 名称     		| 说明
	---------------	| -------------	| ---
	success        	| 是否成功 		|    
		

### 4.2 登陆

> 说明：

1. 请求地址：Post `http://sfax.softoptimus.com:8080/app/login`

2. 请求参数

	参数				| 名称				| 说明
	---------------	| -----------------	| ---
	imei           	| 手机串号			| 
	mobile			| 手机号				| 
	password		| 密码				| 		

3. 响应

	参数				| 名称     		| 说明
	---------------	| -------------	| ---
	success        	| 是否成功 		|    


### 4.3 找回密码

#### 4.3.1 Step1：发送验证码

> 说明：

1. 请求地址：Post `http://sfax.softoptimus.com:8080/app/resetPassword/getCaptcha`

2. 请求参数

	参数				| 名称				| 说明
	---------------	| -----------------	| ---
	imei           	| 手机串号			| 
	mobile			| 手机号				| 	

3. 响应

	参数				| 名称     		| 说明
	---------------	| -------------	| ---
	success        	| 是否成功 		|    


#### 4.3.2 Step2：验证短信验证码

1. 请求地址：Post `http://sfax.softoptimus.com:8080/app/resetPassword/checkCaptcha`

2. 请求参数

	参数				| 名称				| 说明
	---------------	| -----------------	| ---
	imei           	| 手机串号			| 
	mobileCaptcha	| 手机验证码			| 	

3. 响应

	参数				| 名称     		| 说明
	---------------	| -------------	| ---
	success        	| 是否成功 		|    


#### 4.3.3 Step3：重置密码

1. 请求地址：Post `http://sfax.softoptimus.com:8080/app/resetPassword`

2. 请求参数

	参数				| 名称				| 说明
	---------------	| -----------------	| ---
	imei           	| 手机串号			| 
	newPassword		| 新密码			| 	

3. 响应

	参数				| 名称     		| 说明
	---------------	| -------------	| ---
	success        	| 是否成功 		|    


### 4.4 H5页面

#### 4.4.1 关于我们

1. 请求地址：Get `http://sfax.softoptimus.com:8080/m/aboutus?app=1`


#### 4.4.2 安全保障

1. 请求地址：Get `http://sfax.softoptimus.com:8080/m/security?app=1`



#### 4.4.3 红包规则

1. 请求地址：Get `http://sfax.softoptimus.com:8080/m/account/rewards/rules_app?app=1`



#### 4.4.4 理财师

1. 请求地址：Get `http://sfax.softoptimus.com:8080/m/account/promote/financer?app=1`



#### 4.4.5 高级理财师

1. 请求地址：Get `http://sfax.softoptimus.com:8080/m/account/promote/advanced?app=1`



#### 4.4.6 特别说明

1. 请求地址：Get `http://sfax.softoptimus.com:8080/m/account/promote/special?app=1`



#### 4.4.7 晋升规则

> 说明
> 1. 如果用户是理财师，晋升规则链接到`4.4.5高级理财师`
> 
> 2. 如果用户是高级理财师，晋升规则链接到`4.4.10签约理财师`


#### 4.4.8 常见问题

1. 请求地址：Get `http://sfax.softoptimus.com:8080/m/faq?app=1`


#### 4.4.9 推广规则

> 说明
> 1. APP代码中实现
> 
> 2. 根据用户的推荐级别显示不同：身份是签约理财师才显示签约理财师的链接


#### 4.4.10 签约理财师

1. 请求地址：Get `http://sfax.softoptimus.com:8080/m/account/promote/sign?app=1`



# 5 验签接口
> 
> 说明
> 
> 1. app发送来的数据需要用RSA私钥生成签名， 并与数据一起发送
> 
> 2. 签名的param名字应该为 rsa_sign, 如果请求中不带此签名， 拒绝接收
> 
> 3. 签名生成的源字符串为所有参数，除了rsa_sign之外的拼接，如： 参数名1参数1参数名2参数2
> 不带间隔符号，如果验签失败，拒绝接收
> 
>4. 私钥文件将在另外途径提供
 


请求参数

	参数				| 名称				| 说明
	---------------	| -----------------	| ---
    rsa_sign		| rsa签名		    | 必须包含




							



