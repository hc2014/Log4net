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
唯一值得留意的地方就是file节点，他的值是空，这样才可以以日期为文件名来存日志
![](/img/1.png)

如果file节点是绝对路径,那么文件就会存放在指定的路径上面,
![](/img/2.png)
