# springboot-schedule

#### 介绍

springboot当中，对@Scheduled注解使用进行定时器的配置

其中，最重要的就是进行cron表达式的配置

    首先要去了解cron表达式
    corn从左到右（用空格隔开）：秒 分 小时 月份中的日期 月份 星期中的日期 年份
    第一位，表示秒，取值0-59
    第二位，表示分，取值0-59
    第三位，表示小时，取值0-23
    第四位，日期天/日，取值1-31
    第五位，日期月份，取值1-12
    第六位，星期，取值1-7，1表示星期天，2表示星期一
    第七位，年份，可以留空，取值1970-2099


#### 字段 允许值 允许的特殊字符 

    秒 0-59 , - * / 
    分 0-59 , - * / 
    小时 0-23 , - * / 
    日期 1-31 , - * ? / L W C 
    月份 1-12 或者 JAN-DEC , - * / 
    星期 1-7 或者 SUN-SAT , - * ? / L C # 
    年（可选） 留空, 1970-2099 , - * / 
	
#### 常用表达式

    "0 0 12 * * ?" 每天中午12点触发 
    "0 15 10 ? * *" 每天上午10:15触发 
    "0 15 10 * * ?" 每天上午10:15触发 
    "0 15 10 * * ? *" 每天上午10:15触发 
    "0 15 10 * * ? 2005" 2005年的每天上午10:15触发 
    "0 * 14 * * ?" 在每天下午2点到下午2:59期间的每1分钟触发 
    "0 0/5 14 * * ?" 在每天下午2点到下午2:55期间的每5分钟触发 
    "0 0/5 14,18 * * ?" 在每天下午2点到2:55期间和下午6点到6:55期间的每5分钟触发 
    "0 0-5 14 * * ?" 在每天下午2点到下午2:05期间的每1分钟触发 
    "0 10,44 14 ? 3 WED" 每年三月的星期三的下午2:10和2:44触发 
    "0 15 10 ? * MON-FRI" 周一至周五的上午10:15触发 
    "0 15 10 15 * ?" 每月15日上午10:15触发 
    "0 15 10 L * ?" 每月最后一日的上午10:15触发 
    "0 15 10 ? * 6L" 每月的最后一个星期五上午10:15触发 
    "0 15 10 ? * 6L 2002-2005" 2002年至2005年的每月的最后一个星期五上午10:15触发 
    "0 15 10 ? * 6#3" 每月的第三个星期五上午10:15触发 


####  Cron表达式的时间字段除允许设置数值外，还可使用一些特殊的字符，提供列表、范围、通配符等功能，细说如下：

    ●星号(*)：可用在所有字段中，表示对应时间域的每一个时刻，例如，*在分钟字段时，表示“每分钟”；

    ●问号（?）：该字符只在日期和星期字段中使用，它通常指定为“无意义的值”，相当于点位符；

    ●减号(-)：表达一个范围，如在小时字段中使用“10-12”，则表示从10到12点，即10,11,12；
  
    ●逗号(,)：表达一个列表值，如在星期字段中使用“MON,WED,FRI”，则表示星期一，星期三和星期五；

    ●斜杠(/)：x/y表达一个等步长序列，x为起始值，y为增量步长值。如在分钟字段中使用0/15，则表示为0,15,30和45秒，
	而5/15在分钟字段中表示5,20,35,50，你也可以使用*/y，它等同于0/y；

    ●L：该字符只在日期和星期字段中使用，代表“Last”的意思，但它在两个字段中意思不同。
	L在日期字段中，表示这个月份的最后一天，如一月的 31号，非闰年二月的28号；如果L用在星期中，则表示星期六，等同于7。
	但是，如果L出现在星期字段里，而且在前面有一个数值X，则表示“这个月的最后 X天”，例如，6L表示该月的最后星期五；

    ●W：该字符只能出现在日期字段里，是对前导日期的修饰，表示离该日期最近的工作日。
	例如15W表示离该月15号最近的工作日，如果该月15号是星 期六，则匹配14号星期五；如果15日是星期日，则匹配16号星期一；如果15号是星期二，那结果就是15号星期二。
	但必须注意关联的匹配日期不能够跨 月，如你指定1W，如果1号是星期六，结果匹配的是3号星期一，而非上个月最后的那天。W字符串只能指定单一日期，而不能指定日期范围；

    ●LW组合：在日期字段可以组合使用LW，它的意思是当月的最后一个工作日；

    ●井号(#)：该字符只能在星期字段中使用，表示当月某个工作日。
	如6#3表示当月的第三个星期五(6表示星期五，#3表示当前的第三个)，而4#5表示当月的第五个星期三，假设当月没有第五个星期三，忽略不触发；

    ● C：该字符只在日期和星期字段中使用，代表“Calendar”的意思。
	它的意思是计划所关联的日期，如果日期没有被关联，则相当于日历中所有日期。例如5C在日期字段中就相当于日历5日以后的第一天。
	1C在星期字段中相当于星期日后的第一天。


####  @Scheduled当中initialDelay fixedRate  fixedDelay三个量的使用请查看代码当中的例子
