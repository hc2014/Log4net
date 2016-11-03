# Log4net

#一、按照日期为文件名记录日志的配置方式，
```
<appender name="RollingFileAppender" type="log4net.Appender.RollingFileAppender">
			<!--日志文件名开头-->
			<param name="StaticLogFileName" value="false" />
			<file value=""/>
			<!--多线程时采用最小锁定-->
			<lockingModel type="log4net.Appender.FileAppender+MinimalLock"/>
			<!--日期的格式，每天换一个文件记录，如不设置则永远只记录一天的日志，需设置-->
			<param name="DatePattern" value="yyyyMMdd&quot;.log&quot;" />
			<!--是否追加到文件,默认为true，通常无需设置-->
			<appendToFile value="true"/>
			<!--变换的形式为日期，这种情况下每天只有一个日志-->
			<rollingStyle value="Date"/>
			<layout type="log4net.Layout.PatternLayout">
				<param name="ConversionPattern" value="%d [%t] %-5p %c [%x] - %m%n%n" />
			</layout>
		</appender>
```
###唯一值得留意的地方就是file节点，他的值是空，这样才可以以日期为文件名来存日志
![图片](/img/1.png)


###如果file节点是绝对路径、或者是一个相对路径,该路径不包含文件名称,那么文件就会存放在指定的路径上面,
![图片](/img/3.png)
```
<file value="Logs//"/>
```


###如果file节点是一个文件名,那么文件就会存放在指定的路径上面,
```
<file value="log.txt"/>
```
![图片](/img/2.png)


###测试用的config
```
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
	<configSections>
		<section name="log4net" type="log4net.Config.Log4NetConfigurationSectionHandler,log4net"/>
	</configSections>
	<log4net>
		<root>
			<!--控制级别，由低到高: ALL|DEBUG|INFO|WARN|ERROR|FATAL|OFF-->
			<!--比如定义级别为INFO，则INFO级别向下的级别，比如DEBUG日志将不会被记录-->
			<!--如果没有定义LEVEL的值，则缺省为DEBUG-->
			<level value="ALL"/>
			<appender-ref ref="RollingFileAppender"/>

		</root>
		<appender name="RollingFileAppender" type="log4net.Appender.RollingFileAppender">
			<!--日志文件名开头-->
			<param name="StaticLogFileName" value="false" />
			<file value="Logs//"/>
			<!--多线程时采用最小锁定-->
			<lockingModel type="log4net.Appender.FileAppender+MinimalLock"/>
			<!--日期的格式，每天换一个文件记录，如不设置则永远只记录一天的日志，需设置-->
			<param name="DatePattern" value="yyyyMMdd&quot;.txt&quot;" />
			<!--是否追加到文件,默认为true，通常无需设置-->
			<appendToFile value="true"/>
			<!--变换的形式为日期，这种情况下每天只有一个日志-->
			<rollingStyle value="Date"/>
			<layout type="log4net.Layout.PatternLayout">
				<param name="ConversionPattern" value="%d [%t] %-5p %c [%x] - %m%n%n" />
			</layout>
		</appender>
	</log4net>
</configuration>
```
