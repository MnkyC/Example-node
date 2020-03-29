# log4js
# 简介
## 日志分级
trace, debug, info, warn, error, fatal, 权重从小到大
## 日志分类
category，可以设置一个Logger实例的类型，通过其来规定属于哪个日志级别，更加灵活，提供了第二个区分的维度，如，可以为不同的文件，不同的功能模块设置不同的category
## 日志落地
### appenders 数组形式，用于日志的配置

log4js用到的**文件夹都必须事先创建好**，log4js不会自动创建

单个appender是一个对象，不同appender可以有不同配置，属性如下

* type

		console 输出到控制台
		file 输出到普通文件
		dataFile 根据配置的时间格式进行日志滚动
* filename

	输出日志文件的路径，日志目录加日志文件名，可以是绝对路径，也可以是相对路径(相对工程根目录)

	文件名字会根据type属性进行一定的修改
	
	file，文件名后会增加一个编号标签
	
	dateFile，文件名后会加上时间标签
* maxLogSize

	文件最大容量，不指定就不会发生日志滚动，Byte为单位
* layout

		// type属性
		messagePassThrough, 仅仅输出日志内容
		basic, 日志前面加上时间，级别和类别，默认格式
		colored/coloured, basic基础上给日志加上颜色
* pattern

	用于dataFile模式，确定何时滚动日志，默认-yyyy-MM-dd
	
	生成文件时会在filename文件名尾部追加一个时间字符串
* alwaysIncludePattern

	用于dataFile模式，布尔值
	
	false，dateFile没有时间后缀，也不会滚动文件
* compress 是否压缩
* backups

	日志滚动期间要保留的文件数量，多了就删除旧的，默认5
* category appender标识，使用时通过该属性获取对应Logger

### levels 设置不同category的日志级别
控制着日志的输出级别，调试程序时需要全部的日志，发布程序时一些不重要的日志可以隐去，在这里配置即可

levels下的属性和appender对应，其下面的属性名就是appender中的category
### replaceConsole 是否替换控制台输出，布尔值
配置文件中配置了`"type": "console"`的appender，且设置了`"replaceConsole": true`，console.log和console.error的输出内容就会以log4js的格式输出到控制台中

## how?
npm install log4js

1. 创建log4js.json，进行自定义配置
2. 加载配置文件

		const config = require('./log4js.json')
		const log4js = require('log4js');
		log4js.configure(config);
		const xxLogger = log4js.getLogger('对应category名');

## better?
发送到Logstash