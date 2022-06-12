---
title: 牛客网《数据库SQL实战》练习1-10
date: 2020-5-15 5:34:12 
categories: 云笔记
tags:
- MySql
cover: https://cdn.jsdelivr.net/gh/Azao-saya/image-blog@master/20210102/61ec1619gy1g0mbfhhm7pj21c00lqwid_看图王.63pc0rpy2uo0.jpg
---

想找些题sql题目练习一下，发现和之前用java刷pat不一样

那就是我看懂题目有了思路之后，却完全不知道要怎么下笔.....

所以此篇前期就直接看别人的答案学习SQL语句

之后应该会买一个leetcode会员，把leetcode的题目也刷完<!--more-->


## 1.查找最晚入职员工的所有信息

**题目描述：**
查找最晚入职员工的所有信息
CREATE TABLE `employees` (
`emp_no` int(11) NOT NULL,
`birth_date` date NOT NULL,
`first_name` varchar(14) NOT NULL,
`last_name` varchar(16) NOT NULL,
`gender` char(1) NOT NULL,
`hire_date` date NOT NULL,
PRIMARY KEY (`emp_no`));

**输入描述:**

无

**输出描述:**

| emp_no | birth_date | first_name | last_name | gender | hire_date  |
| :----- | :--------- | :--------- | :-------- | :----- | :--------- |
| 10008  | 1958-02-19 | Saniya     | Kalloufi  | M      | 1994-09-15 |

**解题代码：**

> 1>select * from employee order by hire_date desc limit 0,1;
>
> 
>
> 2>select * from employee order by hire_date desc limit 1;
>
> 
>
> 3>select * from employee where hire_date = (select max(hire_date) from employee);

**吐槽：**

>三种写法均能通过测试用例
>
>第三条最为严谨，因为`hire_date`是`data`日期类型，记录的时间只精确到天
>
>如果那天有多个人入职的话无法判断出谁是最晚入职的，应该把当天所有的数据给提取出来。
>
>牛客网的书写规则为：关键字全为小写或者全为大写，不能添加分号，查询内容区别大小写。
>
>`order by` 语句意为根据指定的列对结果进行排序，默认为升序。
>
>`desc` 关键字意为调整`order by`的排序规则为降序
>
>`limit`则是限制要输出多少条内容或~~输出一个区间里的内容~~
>
>此处理解错了，一开始觉得是0≤x≤1。
>
>下面一题依样画葫芦的时候马上暴露了出来问题，
>
>真实意思是检索从第n行开始,获取后面的m条数据
>
>`select max()`是函数返回一列的最大值，null值不包括计算。



## 2.查找入职员工时间排名倒数第三的员工所有信息

**题目描述：**

查找入职员工时间排名倒数第三的员工所有信息
CREATE TABLE `employees` (
`emp_no` int(11) NOT NULL,
`birth_date` date NOT NULL,
`first_name` varchar(14) NOT NULL,
`last_name` varchar(16) NOT NULL,
`gender` char(1) NOT NULL,
`hire_date` date NOT NULL,
PRIMARY KEY (`emp_no`));

**输入描述:**

无

**输出描述:**

| emp_no | birth_date | first_name | last_name | gender | hire_date  |
| :----- | :--------- | :--------- | :-------- | :----- | :--------- |
| 10005  | 1955-01-21 | Kyoichi    | Maliniak  | M      | 1989-09-12 |

**解题代码：**

>1>
>
>select * from employees order by hire_date desc limit 2,1
>
>2>
>
>select *
>from
>employees
>where hire_date=(
>
>​	select distinct hire_date from employees order by hire_date desc limit 2,1
>
>)

**吐槽：**

>两种写法均能通过测试用例
>
>学习了新的写法感觉更清晰了一点
>
>`select distinct`用于返回唯一不同的值
>
>比如得到`hire_date`列的~~所有值~~(唯一不同值)select distinct hire_date from employees
>
>所有不同的入职日期都会显示出来
>
>此处的作用是为了去重，如果像pat的测试用例一样刁难你的话就非常重要了。
>
>因为是`data`类型同一天入职的人区分不出先后，假如有同天入职的将会全部忽略，取出的是倒数第三天的入职信息。
>
>其实是和题意不符了

## 3.查找各个部门当前领导当前薪水详情以及其对应部门编号dept_no

**题目描述:**
查找各个部门当前(to_date='9999-01-01')领导当前薪水详情以及其对应部门编号dept_no
CREATE TABLE `dept_manager` (
`dept_no` char(4) NOT NULL,
`emp_no` int(11) NOT NULL,
`from_date` date NOT NULL,
`to_date` date NOT NULL,
PRIMARY KEY (`emp_no`,`dept_no`));
CREATE TABLE `salaries` (
`emp_no` int(11) NOT NULL,
`salary` int(11) NOT NULL,
`from_date` date NOT NULL,
`to_date` date NOT NULL,
PRIMARY KEY (`emp_no`,`from_date`));

**输入描述:**

无

**输出描述:**

| emp_no | salary | from_date  | to_date   | dept_no |
| :-----: | :-----: | :---------: | :--------: | :------: |
| 10002  | 72527  | 2001-08-02 | 999-01-01 | d001    |
| 10004 | 74057 | 2001-11-27 | 9999-01-01 | d004 |
| 10005 | 94692 | 2001-09-09 | 9999-01-01 | d003 |
| 10006 | 43311 | 2001-08-02 | 9999-01-01 | d002 |
| 10010 | 94409 | 2001-11-23 | 9999-01-01 | d006 |

**解题代码：**

>1>
>
>select s.* ,d.dept_no
>from salaries as s 
>join dept_manager as d 
>on s.emp_no=d.emp_no
>where s.to_date = '9999-01-01'
>and    d.to_date='9999-01-01';
>
>2>
>
>select 
>
>salaries.emp_no,
>
>salaries.salary,
>
>salaries.from_date,
>
>salaries.to_date,
>
>dept_manager.dept_no 
>from salaries inner join dept_manager
>on dept_manager.emp_no = salaries.emp_no
>where dept_manager.to_date = '9999-01-01' 
>and salaries.to_date = '9999-01-01';

**吐槽：**

>不能把整个表格都复制过来，增加le 好多工作量。但当我手动快输入完了的时候，发现他单行其实是用了markdown语法的...
>
>第二条是第一条的完整写法。
>
>最后也可以加上`ORDER BY` salaries.emp_no;
>
>因为（以salaries表为主表进行查询，输出结果以salaries.emp_no升序排序）
>
>不加上的话就不能改变（from salaries inner join dept_manager）这句的salaries和dept_manager的顺序，否则无法通过判例。



## 4.查找所有已经分配部门的员工的last_name和first_name以及dept_no

**题目描述：**

查找所有已经分配部门的员工的last_name和first_name以及dept_no(请注意输出描述里各个列的前后顺序)
CREATE TABLE `dept_emp` (
`emp_no` int(11) NOT NULL,
`dept_no` char(4) NOT NULL,
`from_date` date NOT NULL,
`to_date` date NOT NULL,
PRIMARY KEY (`emp_no`,`dept_no`));
CREATE TABLE `employees` (
`emp_no` int(11) NOT NULL,
`birth_date` date NOT NULL,
`first_name` varchar(14) NOT NULL,
`last_name` varchar(16) NOT NULL,
`gender` char(1) NOT NULL,
`hire_date` date NOT NULL,
PRIMARY KEY (`emp_no`));

**输入描述:**

无

**输出描述:**

| last_name | first_name | dept_no |
| :-------- | :--------- | :------ |
| Facello   | Georgi     | d001    |
| 省略      | 省略       | 省略    |
| Piveteau  | Duangkaew  | d006    |

**解题代码：**

>1>
>
>select employees.last_name, first_name, dept_emp.dept_no
>from dept_emp inner join employees
>on dept_emp.emp_no = employees.emp_no;
>
>2>
>
>SELECT
>    e.last_name,
>    e.first_name,
>    d.dept_no
>
>FROM
>    dept_emp AS d
>INNER JOIN
>    employees AS e
>ON
>    e.emp_no = d.emp_no;

## 5.查找所有员工的last_name和first_name以及对应部门编号dept_no

**题目描述:**
查找所有员工的last_name和first_name以及对应部门编号dept_no，也包括暂时没有分配具体部门的员工(请注意输出描述里各个列的前后顺序)
CREATE TABLE `dept_emp` (
`emp_no` int(11) NOT NULL,
`dept_no` char(4) NOT NULL,
`from_date` date NOT NULL,
`to_date` date NOT NULL,
PRIMARY KEY (`emp_no`,`dept_no`));
CREATE TABLE `employees` (
`emp_no` int(11) NOT NULL,
`birth_date` date NOT NULL,
`first_name` varchar(14) NOT NULL,
`last_name` varchar(16) NOT NULL,
`gender` char(1) NOT NULL,
`hire_date` date NOT NULL,
PRIMARY KEY (`emp_no`));

**输入描述:**

无

**输出描述:**

| last_name | first_name |               dept_no                |
| :-------: | :--------: | :----------------------------------: |
|  Facello  |   Georgi   |                 d001                 |
|   省略    |    省略    |                 省略                 |
|   Sluis   |    Mary    | NULL(在sqlite中此处为空,MySQL为NULL) |


**解题代码：**

>SELECT e.last_name,e.first_name,d.dept_no
>FROM employees as e LEFT JOIN dept_emp as d
>on e.emp_no = d.emp_no;

**吐槽：**

>题目以及输出描述中给出了信息，表示还有暂时没有分配部门的员工。
>
>INNER JOIN 两边表同时有对应的数据，即任何一边缺失数据就不显示。
>便无法按照题目要求取出数据。
>
>Ps：这个牛客网SQL编译器不支持RIGHT/FULL JOIN，所以用LEFT JOIN可以通过，只要把原来的表位置从右换到左即可。

## 6.查找所有员工入职时候的薪水情况

**题目描述:**
查找所有员工入职时候的薪水情况，给出emp_no以及salary， 并按照emp_no进行逆序(请注意，一个员工可能有多次涨薪的情况)
CREATE TABLE `employees` (
`emp_no` int(11) NOT NULL,
`birth_date` date NOT NULL,
`first_name` varchar(14) NOT NULL,
`last_name` varchar(16) NOT NULL,
`gender` char(1) NOT NULL,
`hire_date` date NOT NULL,
PRIMARY KEY (`emp_no`));
CREATE TABLE `salaries` (
`emp_no` int(11) NOT NULL,
`salary` int(11) NOT NULL,
`from_date` date NOT NULL,
`to_date` date NOT NULL,
PRIMARY KEY (`emp_no`,`from_date`));

**输入描述:**

无

**输出描述:**

| emp_no | salary |
| :----: | :----: |
| 10011  | 25828  |
|  省略  |  省略  |
| 10001  | 60117  |


**解题代码：**

>1>
>
>SELECT e.emp_no,s.salary
>FROM employees AS e 
>INNER JOIN salaries AS s
>ON e.emp_no = s.emp_no
>AND e.hire_date = s.from_date
>ORDER BY e.emp_no DESC;
>
>2>
>
>SELECT e.emp_no, s.salary FROM employees AS e, salaries AS s
>WHERE e.emp_no = s.emp_no AND e.hire_date = s.from_date
>ORDER BY e.emp_no DESC

**吐槽：**

>题目要求是要取得入职时的薪水，但一个员工可能有多次涨薪的情况，也就是薪水表中number是不唯一的。
>
>题目中也用了PRIMARY KEY (`emp_no`,`from_date`));应该是叫做组合主键吧，来进一步说明。
>
>所以需要去找hire_date记录的日期所对应的薪水情况。



## 7.查找薪水变动超过15次的员工号emp_no以及其对应的变动次数t

**题目描述:**
查找薪水变动超过15次的员工号emp_no以及其对应的变动次数t
CREATE TABLE `salaries` (
`emp_no` int(11) NOT NULL,
`salary` int(11) NOT NULL,
`from_date` date NOT NULL,
`to_date` date NOT NULL,
PRIMARY KEY (`emp_no`,`from_date`));

**输入描述:**

无

**输出描述:**

| emp_no |  t   |
| :----: | :--: |
| 10001  |  17  |
| 10004  |  16  |
| 10009  |  18  |

**解题代码：**

>SELECT emp_no, COUNT(emp_no) AS t FROM salaries 
>GROUP BY emp_no HAVING t > 1

**吐槽：**

>变动次数就是看表里emp_no有多少个
>
>COUNT(column_name) 函数返回指定列的值的数目（NULL 不计入）：
>
>
>
>GROUP BY 语句用于结合聚合函数，根据一个或多个列对结果集进行分组。
>
>使用效果就是输出描述那样 emp_no 加上自己命名的
>
>
>
>在 SQL 中增加 HAVING 子句原因是，WHERE 关键字无法与聚合函数一起使用。
>
>HAVING 子句可以让我们筛选分组后的各组数据。
>
>WHERE语句在GROUP BY语句之前；SQL会在分组之前计算WHERE语句。  
>
>HAVING语句在GROUP BY语句之后；SQL会在分组之后计算HAVING语句。

## 8.找出所有员工当前薪水salary情况

**题目描述:**
找出所有员工当前(to_date='9999-01-01')具体的薪水salary情况，对于相同的薪水只显示一次,并按照逆序显示
CREATE TABLE `salaries` (
`emp_no` int(11) NOT NULL,
`salary` int(11) NOT NULL,
`from_date` date NOT NULL,
`to_date` date NOT NULL,
PRIMARY KEY (`emp_no`,`from_date`));

**输入描述:**

无

**输出描述:**

| salary |
| :----: |
| 94692  |
| 94409  |
| 88958  |

**解题代码：**

>1>
>
>SELECT DISTINCT salary FROM salaries
>WHERE to_date = '9999-01-01' ORDER BY salary DESC
>
>2>
>
>select salary from salaries 
>
>where to_date='9999-01-01' group by salary order by salary desc

**吐槽：**

>SELECT DISTINCT 语句用于返回唯一不同的值。
>
>评论说要去重的列数据种类很多时，group by更快，要去重的列数据种类很少时，distinct更快
>
>大表的话是用group by 解决重复问题

## 9.获取所有部门当前manager的当前薪水情况，给出dept_no, emp_no以及salary

**题目描述:**
获取所有部门当前(dept_manager.to_date='9999-01-01')manager的当前(salaries.to_date='9999-01-01')薪水情况，给出dept_no, emp_no以及salary(请注意，同一个人可能有多条薪水情况记录)
CREATE TABLE `dept_manager` (
`dept_no` char(4) NOT NULL,
`emp_no` int(11) NOT NULL,
`from_date` date NOT NULL,
`to_date` date NOT NULL,
PRIMARY KEY (`emp_no`,`dept_no`));
CREATE TABLE `salaries` (
`emp_no` int(11) NOT NULL,
`salary` int(11) NOT NULL,
`from_date` date NOT NULL,
`to_date` date NOT NULL,
PRIMARY KEY (`emp_no`,`from_date`));

**输入描述:**

无

**输出描述:**

| dept_no | emp_no | salary |
| :------ | :----- | :----- |
| d001    | 10002  | 72527  |
| d004    | 10004  | 74057  |
| d003    | 10005  | 94692  |
| d002    | 10006  | 43311  |
| d006    | 10010  | 94409  |

**解题代码：**

>1>
>
>select d.dept_no,d.emp_no,s.salary
> from dept_manager d,salaries s
> where d.emp_no = s.emp_no
> and d.to_date = s.to_date
> and s.to_date='9999-01-01'
>
>2>
>
>select d.dept_no,d.emp_no,s.salary
>from dept_manager as d inner join salaries as s
>on d.emp_no = s.emp_no
>and d.to_date = '9999-01-01' 
>and s.to_date = '9999-01-01'

**吐槽：**

>SELECT DISTINCT 语句用于返回唯一不同的值。
>
>评论说要去重的列数据种类很多时，group by更快，

## 10.获取所有非manager的员工emp_no

**题目描述:**获取所有非manager的员工emp_no
CREATE TABLE `dept_manager` (
`dept_no` char(4) NOT NULL,
`emp_no` int(11) NOT NULL,
`from_date` date NOT NULL,
`to_date` date NOT NULL,
PRIMARY KEY (`emp_no`,`dept_no`));
CREATE TABLE `employees` (
`emp_no` int(11) NOT NULL,
`birth_date` date NOT NULL,
`first_name` varchar(14) NOT NULL,
`last_name` varchar(16) NOT NULL,
`gender` char(1) NOT NULL,
`hire_date` date NOT NULL,

PRIMARY KEY (`emp_no`));

如插入为:

INSERT INTO dept_manager VALUES('d001',10002,'1996-08-03','9999-01-01');
INSERT INTO dept_manager VALUES('d002',10006,'1990-08-05','9999-01-01');
INSERT INTO dept_manager VALUES('d003',10005,'1989-09-12','9999-01-01');
INSERT INTO dept_manager VALUES('d004',10004,'1986-12-01','9999-01-01');
INSERT INTO dept_manager VALUES('d005',10010,'1996-11-24','2000-06-26');
INSERT INTO dept_manager VALUES('d006',10010,'2000-06-26','9999-01-01');

INSERT INTO employees VALUES(10001,'1953-09-02','Georgi','Facello','M','1986-06-26');
INSERT INTO employees VALUES(10002,'1964-06-02','Bezalel','Simmel','F','1985-11-21');
INSERT INTO employees VALUES(10003,'1959-12-03','Parto','Bamford','M','1986-08-28');
INSERT INTO employees VALUES(10004,'1954-05-01','Chirstian','Koblick','M','1986-12-01');
INSERT INTO employees VALUES(10005,'1955-01-21','Kyoichi','Maliniak','M','1989-09-12');
INSERT INTO employees VALUES(10006,'1953-04-20','Anneke','Preusig','F','1989-06-02');
INSERT INTO employees VALUES(10007,'1957-05-23','Tzvetan','Zielinski','F','1989-02-10');
INSERT INTO employees VALUES(10008,'1958-02-19','Saniya','Kalloufi','M','1994-09-15');
INSERT INTO employees VALUES(10009,'1952-04-19','Sumant','Peac','F','1985-02-18');
INSERT INTO employees VALUES(10010,'1963-06-01','Duangkaew','Piveteau','F','1989-08-24');
INSERT INTO employees VALUES(10011,'1953-11-07','Mary','Sluis','F','1990-01-22');

**输入描述:**

无

**输出描述:**

| emp_no |
| :----: |
| 10001  |
| 10003  |
| 10007  |
| 10008  |
| 10009  |
| 10011  |

**解题代码：**

>1>
>
>SELECT emp_no FROM employees
>WHERE emp_no NOT IN (SELECT emp_no FROM dept_manager)
>
>2>
>
>SELECT emp_no FROM (SELECT * FROM employees LEFT JOIN dept_manager
>ON employees.emp_no = dept_manager.emp_no)
>WHERE dept_no IS NULL
>
>3>
>
>SELECT employees.emp_no FROM employees LEFT JOIN dept_manager
>ON employees.emp_no = dept_manager.emp_no
>WHERE dept_no IS NULL
>
>4>
>
>select e.emp_no from employees em
>where not exists
>(select distinct d.emp_no from dept_manager d where e.emp_no=d.emp_no)
>
>5>
>
>SELECT 
>    e.emp_no
>FROM 
>    employees e
>WHERE
>    NOT EXISTS (SELECT 1 FROM dept_manager d WHERE e.emp_no = d.emp_no)

**吐槽：**

>NOT IN	IN 运算符的对立面，用于把某个值与不在一系列指定列表的值进行比较。
>
>第二种（SELECT * FROM employees LEFT JOIN dept_manager
>ON employees.emp_no = dept_manager.emp_no）
>
>题目说明是获取第一张表不存的员工信息，left join的定义为
>
>LEFT JOIN 关键字从左表（table1）返回所有的行，即使右表（table2）中没有匹配。如果右表中没有匹配，则结果为 NULL。
>
>![image-20200605105414967](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200605105414967.png)
>
>可以看到右侧是为null的，最后提取出dept_no为null的emp_no即可
>
>第三种为简化
>
>第四种为not exists的解法，其中distinct在本题中并不需要。
>
>第五种为not exists的怪异写法，其中的select 1常用在exists子句中，检测符合条件记录是否存在，返回值永远为1，似乎是用于提升效率。本题中这个1换成任意数字或者 * 都是正确的。

