# 20220115
体验  打开网页的速度


以下内容 了解就好

MySQL的数据类型
	数值类型
		整型
		浮点型
			000.00
			5,2
	字符串型
		varchar   可变长度  节省空间 读取速度会变慢 20 + 
		char      固定长度  以空间换时间           20
	时间 日期

主键 和 外键
主键是表的 主要的编号
外键是另一张表的主键


计算机上面 存储 两种状态的情况都是：
	1 0
	真 假
	开 关
	高 低
	亮 灭
	凸 凹


关系：
	1:1
	1:n   就要拆分表
	n:m   要拆两张表  一个实体表（爱好表）  一个是关联表 


MySQL的引擎
	MYISAM  成熟稳定的
	INNODB  具有事务处理功能：多件事情 都成功 才会执行
		银行转账：
			工商银行 有一张表
				王亮   账号  -2000  SQL update -2000 成功了
				林静   账号  +2000  SQL update +2000 成功了
				最后才执行
				否则
				就会 回滚 到 初始状态

	MEMORY  小型数据库（它是存在内存里面的）
		最大的好处：处理数据 特别的快


MySQL的索引：加快我们处理数据的速度
	普通索引：可以重复，可以为空
	唯一索引：不能重复，可以为空
	主索引  ：不能重复，不可以为空
		主键 即 主索引
	全文索引：



所有的命令格式；
	主命令  参数 。。。。。

所有能操作命令的地方，命令都有记忆功能
	你按 上下键 就可以使用历史命令

用什么 什么就是主命令
例如；
msyql msyql 

我们的电脑需要操作什么命令，你要告诉计算机 你要操作的命令在哪里
所以你要给计算机去配置 命令的路径
	这个操作是：配置环境变量
	1 找到环境变量的配置。
	2 把MySQL的命令路径给到它就好了。

SQL命令是重点----------------
命令行的操作 数据库 的流程
0 连接数据库
	mysql -u root -p
	passwd:****
1 查看数据库
	SHOW DATABASES;  (书写格式：关键词 都是大写，自定义的都是小写)
2 选择数据库
	USE emp01;
3 查看数据表
	SHOW TABLES;


开始学习 SQL命令 ： 增 删 查 改


合理性

sql 命令 其实是 死公式：
	它可以套公式


SQL命令  的学习
查  技术含量 最高的  （查 和 运算 结合）
------------------查询---------------------------------
查： 简单的查询
	SELECT   *    FROM   emp;
	查询    全部   来自   表名
	查询    列名   来自   表名；
		变化就是列名  和  表名


	*全部代表什么意思：代表 字段名 ==  列名


	题：我要看公司员工的年龄。
	SELECT e_name,e_age FROM emp;

	题：我要看公司员工的年龄和性别。
	SELECT e_name,e_age,e_sex FROM emp;


统计 函数  count();  统计 记录数
	题：我要看公司有多少员工
	SELECT COUNT(*) FROM emp;


取别名  原名 AS 别名
	例子：SELECT COUNT(*) AS count FROM emp;

条件查询WHERE：等于= 、 不等于!= 、不等于<>  、  小于< 、 大于> 
	题：我要看公司的员工哪些是 超过20岁的人
	SELECT e_name,e_age FROM emp WHERE e_age>20;

	题：我要公司有哪些女孩子
	SELECT * FROM emp WHERE e_sex=0;



逻辑运算符：与&& AND  或|| OR   非！ NOT

与：并且

或：或者

非：取反


一个女孩  要 择偶 
	男士： 有钱  并且and  帅

年龄大了 一个女孩  要 择偶 
	男士： 有钱  或者or  帅

另外一个女孩 她有一段感情 挫折 要 择偶 
	男士： 有钱  或者  帅 不靠谱 “ 反而 不嫁 ” 取反
	
	题；我要看公司20岁的男孩子有哪些
	SELECT * FROM emp WHERE e_age=20 AND e_sex=1;

	题；我要看公司20多岁的员工有哪些
	SELECT * FROM emp WHERE e_age>=20 AND e_age<30;

	题；我要看公司20多岁的男员工有哪些
	SELECT * FROM emp WHERE e_age>=20 AND e_age<30 AND e_sex=1;

	题；我要看公司编号为1 3 5的员工是谁？
	SELECT * FROM emp WHERE e_id=1 OR e_id=3 OR e_id=5;

IN(1,3,5) 指定谁
	SELECT * FROM emp WHERE e_id IN(1,3,5);


	题；我要看公司除了编号为1 3 5的员工是谁？
	SELECT * FROM emp WHERE e_id NOT IN(1,3,5);


模糊查询：字段 like   %多个模糊字符  _单个模糊字符
	黄江    '黄_'     '黄%'
	黄小雨  '黄__'    '黄%'

	题：我要查询姓 黄 有些员工  黄XX  '黄%'  '黄__'
	SELECT * FROM emp WHERE e_name LIKE '黄%';

	题：我要查询名字里面带 亮 '%亮%'
	SELECT * FROM emp WHERE e_name LIKE '%亮%';


限制查询  LIMIT 开始位置，限制条数

排序  ORDER BY 字段  ASC升序
	题：按照编号 升序
	SELECT * FROM emp ORDER BY e_id ASC;
排序  ORDER BY 字段  DESC降序
	题：按照编号 降序
	SELECT * FROM emp ORDER BY e_id DESC;

联表查询（不是重点，扩展知识点,了解即可）


	左连接  LEFT JOIN

	SELECT * FROM emp LEFT JOIN bumen ON emp.b_id=bumen.b_id;
	查询 全部字段 来自 一张表 左连接 另一张表 通过 一张表里面的字段=另一张表里面的字段

	SELECT * FROM emp LEFT JOIN bumen ON emp.b_id=bumen.b_id;

	SELECT emp.e_name,emp.e_sex,bumen.b_name FROM 
	emp LEFT JOIN bumen 
	ON 
	emp.b_id=bumen.b_id;


	右连接  RIGHT JOIN

	SELECT * FROM emp RIGHT JOIN bumen ON emp.b_id=bumen.b_id;

	内连接 
	SELECT * FROM emp,bumen WHERE emp.b_id=bumen.b_id;

联表查询的取别名
	SELECT * FROM emp AS e RIGHT JOIN bumen AS b ON e.b_id=b.b_id;


联合查询 （SQL注入 - 联合注入）union
	联合查询要具备的条件是： 两张表的 字段要相同
	SELECT * FROM emp UNION select * FROM bumen;




增--------------------------------------------
INSERT INTO emp (e_name,e_sex) VALUES ('aaaa',1);

改----不能少了条件-----就是重新赋值
UPDATE emp SET e_name='aaa' WEHRE e_id=15;

删-----不能少了条件------
DELECT FROM emp WHERE e_id=15;

删库跑路：数据库 做 备份


sql注入 漏洞
	5 - 6 天时间 去学习
