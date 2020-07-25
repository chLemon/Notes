# 表格初始化

--1.学生表
Student(Sid,Sname,Sage,Ssex) 

--Sid 学生编号,Sname 学生姓名,Sage 出生年月,Ssex 学生性别

--2.课程表 
Course(Cid,Cname,Tid) 

--Cid --课程编号,Cname 课程名称,Tid 教师编号

--3.教师表 
Teacher(Tid,Tname)

 --Tid 教师编号,Tname 教师姓名

--4.成绩表 
SC(Sid,Cid,score)

 --Sid 学生编号,Cid 课程编号,score 分数

## 创建测试数据

学生表 Student

create table Student(Sid varchar(10),Sname nvarchar(10),Sage datetime,Ssex nvarchar(10))
insert into Student values('01' , N'赵雷' , '1990-01-01' , N'男')
insert into Student values('02' , N'钱电' , '1990-12-21' , N'男')
insert into Student values('03' , N'孙风' , '1990-05-20' , N'男')
insert into Student values('04' , N'李云' , '1990-08-06' , N'男')
insert into Student values('05' , N'周梅' , '1991-12-01' , N'女')
insert into Student values('06' , N'吴兰' , '1992-03-01' , N'女')
insert into Student values('07' , N'郑竹' , '1989-07-01' , N'女')
insert into Student values('08' , N'王菊' , '1990-01-20' , N'女')



科目表 Course
create table Course(Cid varchar(10),Cname nvarchar(10),Tid varchar(10))
insert into Course values('01' , N'语文' , '02')
insert into Course values('02' , N'数学' , '01')
insert into Course values('03' , N'英语' , '03')



教师表 Teacher
create table Teacher(Tid varchar(10),Tname nvarchar(10))
insert into Teacher values('01' , N'张三')
insert into Teacher values('02' , N'李四')
insert into Teacher values('03' , N'王五')



成绩表 SC
create table SC(Sid varchar(10),Cid varchar(10),score decimal(18,1))
insert into SC values('01' , '01' , 80)
insert into SC values('01' , '02' , 90)
insert into SC values('01' , '03' , 99)
insert into SC values('02' , '01' , 70)
insert into SC values('02' , '02' , 60)
insert into SC values('02' , '03' , 80)
insert into SC values('03' , '01' , 80)
insert into SC values('03' , '02' , 80)
insert into SC values('03' , '03' , 80)
insert into SC values('04' , '01' , 50)
insert into SC values('04' , '02' , 30)
insert into SC values('04' , '03' , 20)
insert into SC values('05' , '01' , 76)
insert into SC values('05' , '02' , 87)
insert into SC values('06' , '01' , 31)
insert into SC values('06' , '03' , 34)
insert into SC values('07' , '02' , 89)
insert into SC values('07' , '03' , 98)

# ５０道练习题

1. 查询" 01 "课程比" 02 "课程成绩高的学生的信息及课程分数

```
select       s.* , c1.score, c2.score
from     student as s,
     (select sid,score from sc where cid=01) c1,
     (select sid,score from sc where cid=02) c2
where      s.Sid = c1.Sid and c1.score>c2.score and c1.Sid = c2.Sid
```

1.1 查询同时存在" 01 "课程和" 02 "课程的情况

```
select
       s.*
from
     student s
where s.Sid in (select SC.Sid from sc where sc.Cid='01')
and s.Sid in (select sc.Sid from sc where sc.Cid='02');
```

```
select
    s.*, s1.score,s2.score
from
    student s,
    (select SC.Sid,score from sc where sc.Cid='01') s1,
    (select sc.Sid,score from sc where sc.Cid='02') s2
where s.Sid = s1.Sid
  and s1.Sid=s2.Sid
```

1.2 查询存在" 01 "课程但可能不存在" 02 "课程的情况(不存在时显示为 null )
```
select
    s.*, s1.score, s2.score
from
    (select SC.Sid,score from sc where sc.Cid='01') s1,
    student s
left join (select SC.Sid,score from sc where sc.Cid='02') s2 on s.Sid = s2.Sid
where s.Sid = s1.Sid
```
```
select
    s.*, s1.score, s2.score
from

    student s join (select SC.Sid,score from sc where sc.Cid='01') s1
left join (select SC.Sid,score from sc where sc.Cid='02') s2 on s.Sid = s2.Sid
where s.Sid = s1.Sid
```

1.3 查询不存在" 01 "课程但存在" 02 "课程的情况

```
select
    s.*, s2.score as s2_score
from
    student s ,
     (select SC.Sid,score from sc where sc.Cid='02') s2
where s.Sid = s2.Sid and s.Sid not in (select SC.Sid from sc where sc.Cid='01')
```

2. 查询平均成绩大于等于 60 分的同学的学生编号和学生姓名和平均成绩

考几门除几门
```
select
    s.Sid,s.Sname,avg(score)
from
    student as s,sc
where s.Sid=sc.Sid
group by s.Sid
having avg(score)>60
```
全部除以3？
```
select
    s.Sid,s.Sname,(sum(score)/3) as aver
from
    student as s,sc
where s.Sid=sc.Sid
group by s.Sid
having aver>60
```
3. 查询在 SC 表存在成绩的学生信息
```
select
    distinct s.*
from
    student s,sc
where s.Sid = sc.Sid
```

```
select * from student where sid in (select sid from sc where score is not null)
```
4. 查询所有同学的学生编号、学生姓名、选课总数、所有课程的总成绩(没成绩的显示为 null )
```
select s.Sid,s.Sname,count(sc.Cid),sum(sc.score)
from student s left join sc on s.Sid=sc.Sid
group by s.Sid, s.Sname
```
4.1 查有成绩的学生信息
```
select s.Sid,s.Sname,count(sc.Cid),sum(sc.score)
from student s ,sc
where      s.Sid=sc.Sid
group by s.Sid, s.Sname
```
5. 查询「李」姓老师的数量 
```
select count(teacher.Tname)
from teacher
where teacher.Tname like '李%'
```
6. 查询学过「张三」老师授课的同学的信息 
```
select *
from student,sc,teacher,course
where teacher.Tname='张三'
  and teacher.Tid=course.Tid
  and course.Cid=sc.Cid
  and sc.Sid=student.Sid
```
7. 查询没有学全所有课程的同学的信息 
```
select s.*
from student s,
(select sc.Sid, count(sc.Cid) m from sc group by sc.Sid) A,
(select count(course.Cid) n from course) B
where A.m <> B.n and A.Sid = s.Sid
```
这样查不到一门课都没选的人
8. 查询至少有一门课与学号为" 01 "的同学所学相同的同学的信息 
```
select * from student where  Sid in (select distinct Sid from sc where Cid in (select Cid from sc where sc.Sid='01'))
```

```
select *
from student s ,
     (select Cid from sc where sc.Sid='01') cid01,
     sc
where
     sc.Cid=cid01.Cid
and sc.Sid=s.Sid
group by s.Sid
```
9. 查询和" 01 "号的同学学习的课程完全相同的其他同学的信息 
这道题答案有个问题啊，你怎么知道就三门课【做这个案例的时候发现之前一直把is null 写成了= null，我就说为啥结果一直不对……】

做了半天没做出来，发现有个思路很巧妙：
先获取01的课程列表
然后把所有选了不在这个列表里的课的人都剔除掉
这样比较数量就可以了
```
# 查询和" 01 "号的同学学习的课程完全相同的其他同学的信息

# 拿到了01同学的课程代码
select Cid from sc where sc.Sid='01';

# 去掉选了其他课的人
select Sid from sc where sc.Cid not in (select Cid from sc where sc.Sid='01')

# 然后在这些人里计数判等即可
## 01同学选课数
select count(Cid) from sc where sc.Sid='01'
## 其他同学的选课数
select count(Cid) from sc where sc.Sid not in (select Sid from sc where sc.Cid not in (select Cid from sc where sc.Sid='01')) group by sc.Sid
## 把不等的和01直接去掉，剩下的就是结果
select *
from
        student s,
        (select Sid,count(Cid) c from sc where sc.Sid not in (select Sid from sc where sc.Cid not in (select Cid from sc where sc.Sid='01')) group by sc.Sid) scid
where s.sid=scid.Sid and scid.c <> (select count(Cid) from sc where sc.Sid='01') and scid.c <>'01'
```
10. 查询没学过"张三"老师讲授的任一门课程的学生姓名 
```
select sname from student
where sname not in (
    select s.sname
    from student as s, course as c, teacher as t, sc
    where s.sid = sc.sid
      and sc.cid = c.cid
      and c.tid = t.tid
      and t.tname = '张三'
)
```
11. 查询两门及其以上不及格课程的同学的学号，姓名及其平均成绩 
```
select student.Sid,Sname,avg(score) a
from student,sc
where student.Sid=sc.Sid
and student.Sid in (
    select sc.Sid
    from sc,
         (select sc.Sid,count(Sid) n from sc where score<60 group by Sid) m
    where m.n>=2 and sc.Sid=m.Sid
    )
group by student.Sid, Sname
```

```
select s.sid, s.sname, avg(score)
from student as s, sc
where s.sid = sc.sid and score<60
group by s.sid
having count(score)>=2
```
12. 检索" 01 "课程分数小于 60，按分数降序排列的学生信息
```
select * from
student s,sc
where
s.Sid =sc.Sid
and sc.Cid='01'
and sc.score<60
order by sc.score desc
```
13. 按平均成绩从高到低显示所有学生的所有课程的成绩以及平均成绩
```

```
14. 查询各科成绩最高分、最低分和平均分：

    以如下形式显示：课程 ID，课程 name，最高分，最低分，平均分，及格率，中等率，优良率，优秀率
    及格为>=60，中等为：70-80，优良为：80-90，优秀为：>=90
    要求输出课程号和选修人数，查询结果按人数降序排列，若人数相同，按课程号升序排列

15. 按各科成绩进行排序，并显示排名， Score 重复时保留名次空缺

15.1 按各科成绩进行排序，并显示排名， Score 重复时合并名次

16.  查询学生的总成绩，并进行排名，总分重复时保留名次空缺

16.1 查询学生的总成绩，并进行排名，总分重复时不保留名次空缺

17. 统计各科成绩各分数段人数：课程编号，课程名称，[100-85]，[85-70]，[70-60]，[60-0] 及所占百分比

18. 查询各科成绩前三名的记录
19. 查询每门课程被选修的学生数 
20. 查询出只选修两门课程的学生学号和姓名 
21. 查询男生、女生人数
22. 查询名字中含有「风」字的学生信息
23. 查询同名同性学生名单，并统计同名人数
24. 查询 1990 年出生的学生名单
25. 查询每门课程的平均成绩，结果按平均成绩降序排列，平均成绩相同时，按课程编号升序排列
26. 查询平均成绩大于等于 85 的所有学生的学号、姓名和平均成绩 
27. 查询课程名称为「数学」，且分数低于 60 的学生姓名和分数 
28. 查询所有学生的课程及分数情况（存在学生没成绩，没选课的情况）
29. 查询任何一门课程成绩在 70 分以上的姓名、课程名称和分数
30. 查询不及格的课程
31. 查询课程编号为 01 且课程成绩在 80 分以上的学生的学号和姓名
32. 求每门课程的学生人数 
33. 成绩不重复，查询选修「张三」老师所授课程的学生中，成绩最高的学生信息及其成绩
34. 成绩有重复的情况下，查询选修「张三」老师所授课程的学生中，成绩最高的学生信息及其成绩
35. 查询不同课程成绩相同的学生的学生编号、课程编号、学生成绩 
36. 查询每门功成绩最好的前两名
37. 统计每门课程的学生选修人数（超过 5 人的课程才统计）。
38. 检索至少选修两门课程的学生学号 
39. 查询选修了全部课程的学生信息
40. 查询各学生的年龄，只按年份来算 
41. 按照出生日期来算，当前月日 < 出生年月的月日则，年龄减一
42. 查询本周过生日的学生
43. 查询下周过生日的学生
44. 查询本月过生日的学生
45. 查询下月过生日的学生

# 解答

1. 查询" 01 "课程比" 02 "课程成绩高的学生的信息及课程分数
```

```
1.1 查询同时存在" 01 "课程和" 02 "课程的情况

1.2 查询存在" 01 "课程但可能不存在" 02 "课程的情况(不存在时显示为 null )

1.3 查询不存在" 01 "课程但存在" 02 "课程的情况

2. 查询平均成绩大于等于 60 分的同学的学生编号和学生姓名和平均成绩

3. 查询在 SC 表存在成绩的学生信息

4. 查询所有同学的学生编号、学生姓名、选课总数、所有课程的总成绩(没成绩的显示为 null )

4.1 查有成绩的学生信息

5. 查询「李」姓老师的数量 

6. 查询学过「张三」老师授课的同学的信息 

7. 查询没有学全所有课程的同学的信息 

8. 查询至少有一门课与学号为" 01 "的同学所学相同的同学的信息 

9. 查询和" 01 "号的同学学习的课程完全相同的其他同学的信息 

10. 查询没学过"张三"老师讲授的任一门课程的学生姓名 

11. 查询两门及其以上不及格课程的同学的学号，姓名及其平均成绩 

12. 检索" 01 "课程分数小于 60，按分数降序排列的学生信息

13. 按平均成绩从高到低显示所有学生的所有课程的成绩以及平均成绩

14. 查询各科成绩最高分、最低分和平均分：

    以如下形式显示：课程 ID，课程 name，最高分，最低分，平均分，及格率，中等率，优良率，优秀率
    及格为>=60，中等为：70-80，优良为：80-90，优秀为：>=90
    要求输出课程号和选修人数，查询结果按人数降序排列，若人数相同，按课程号升序排列

15. 按各科成绩进行排序，并显示排名， Score 重复时保留名次空缺

15.1 按各科成绩进行排序，并显示排名， Score 重复时合并名次

16.  查询学生的总成绩，并进行排名，总分重复时保留名次空缺

16.1 查询学生的总成绩，并进行排名，总分重复时不保留名次空缺

17. 统计各科成绩各分数段人数：课程编号，课程名称，[100-85]，[85-70]，[70-60]，[60-0] 及所占百分比
18. 查询各科成绩前三名的记录
19. 查询每门课程被选修的学生数 
20. 查询出只选修两门课程的学生学号和姓名 
21. 查询男生、女生人数
22. 查询名字中含有「风」字的学生信息
23. 查询同名同性学生名单，并统计同名人数
24. 查询 1990 年出生的学生名单
25. 查询每门课程的平均成绩，结果按平均成绩降序排列，平均成绩相同时，按课程编号升序排列
26. 查询平均成绩大于等于 85 的所有学生的学号、姓名和平均成绩 
27. 查询课程名称为「数学」，且分数低于 60 的学生姓名和分数 
28. 查询所有学生的课程及分数情况（存在学生没成绩，没选课的情况）
29. 查询任何一门课程成绩在 70 分以上的姓名、课程名称和分数
30. 查询不及格的课程
31. 查询课程编号为 01 且课程成绩在 80 分以上的学生的学号和姓名
32. 求每门课程的学生人数 
33. 成绩不重复，查询选修「张三」老师所授课程的学生中，成绩最高的学生信息及其成绩
34. 成绩有重复的情况下，查询选修「张三」老师所授课程的学生中，成绩最高的学生信息及其成绩
35. 查询不同课程成绩相同的学生的学生编号、课程编号、学生成绩 
36. 查询每门功成绩最好的前两名
37. 统计每门课程的学生选修人数（超过 5 人的课程才统计）。
38. 检索至少选修两门课程的学生学号 
39. 查询选修了全部课程的学生信息
40. 查询各学生的年龄，只按年份来算 
41. 按照出生日期来算，当前月日 < 出生年月的月日则，年龄减一
42. 查询本周过生日的学生
43. 查询下周过生日的学生
44. 查询本月过生日的学生
45. 查询下月过生日的学生

