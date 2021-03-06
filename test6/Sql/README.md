# 数据库设计 [返回](../README.md)

<div id="users"></div>
### 1.用户表users

| 字段            | 类型              | 主键、外键 | 可以为空 | 默认值 | 约束 | 说明                            |
| :-------------- | :---------------- | :--------- | :------- | :----- | :--- | :------------------------------ |
| user_id         | NUMBER(8,0)       | 主键       | 否       |        |      | 用户id                          |
| name            | VARCHAR2(50BYTE)  |            | 否       |        |      | 用户真实姓名                    |
| github_username | VARCHAR2(50BYTE)  |            | 是       | 空     |      | 用户github账户名                |
| update_date     | DATE              |            | 是       | 空     |      | 用户github账号修改时间          |
| password        | VARCHAR2(512BYTE) |            | 是       | 空     |      | 用户密码                        |
| disable         | VARCHAR2(20BYTE)  |            | 否       | 0      |      | 用户是否禁用（1 禁用;0 不禁用） |

<div id="teachers"></div>
### 2.教师表 teachers

| 字段              | 类型               | 主键、外键 | 可以为空 | 默认值 | 约束 | 说明                            |
| :---------------- | :----------------- | :--------- | :------- | :----- | :--- | :------------------------------ |
| teacher_id        | VARCHAR2(50BYTE)   | 主键       | 否       |        |      | 教师id，为教师入职时职工号      |
| teacher_name      | VARCHAR2(50BYTE)   |            | 否       |        |      | 老师的名字                      |
| department_id     | VARCHAR2(400 BYTE) | 外键       | 否       |        |      | 教师所属部门，部门表外键        |
| user_id           | NUMBER(8,0)        | 外键       | 是       |        |      | 老师的用户id，users表的外键     |
| teacher_course_id | VARCHAR2(50BYTE)   | 外键       | 否       |        |      | 老师选择的课程id,course表的外键 |

<div id="department"></div>
### 3.部门表 department

| 字段            | 类型              | 主键、外键 | 可以为空 | 默认值 | 约束 | 说明     |
| :-------------- | :---------------- | :--------- | :------- | :----- | :--- | :------- |
| department_id   | VARCHAR2(50 BYTE) | 主键       | 否       |        |      | 部门id   |
| department_name | VARCHAR2(50BYTE)  |            | 否       |        |      | 部门名称 |

<div id="students"></div>
### 4.学生表 students

| 字段       | 类型               | 主键、外键 | 可以为空 | 默认值 | 约束 | 说明                                                         |
| :--------- | :----------------- | :--------- | :------- | :----- | :--- | :----------------------------------------------------------- |
| student_id | VARCHAR2(50 BYTE)  | 主键       | 否       |        |      | 学生id,是学生的学号                                          |
| user_id    | NUMBER(8,0)        | 外键       | 是       |        | 空   | 学生的用户id，users表的外键，为空表示还没有建立用户          |
| major_id   | NUMBER(8,0)        | 外键       | 否       |        |      | 学生的专业id，major表外键                                    |
| class_id   | NUMBER(8,0)        | 外键       | 否       |        |      | 学生年级id,class表外键                                       |
| result_sum | VARCHAR2(400 BYTE) | 外键       | 是       | 空     |      | 成绩汇总（来自grades表），以逗号分开，第一个成绩是平均成绩,后面是每次实验的成绩，N表示未批改，平均分只计算已批改的。比如：“81.25,70,80,85,90,N”表示一共批改了4次，第5次未批改，4次的成绩分别是81.25,70,80,85,90,N，4次的平均分是81.25 |
| web_sum    | VARCHAR2(400 BYTE) |            | 是       | 空     |      | GitHub网址是否正确，用逗号分开，Y代表正确，N代表不正确。第1位代表总的GitHUB地址是否正确，第2位表示第1次实验的地址，第3位表示第2位实验地址，依此类推。比如：“Y,Y,Y,Y,Y,N”表示第5次实验地址不正确，其他地址正确 |
| term_id    | NUMBER(8,0)        | 外键       |          |        |      | 学期id，term表外键                                           |

<div id="major"></div>
### 5.专业表major

| 字段       | 类型             | 主键、外键 | 可以为空 | 默认值 | 约束 | 说明     |
| :--------- | :--------------- | :--------- | :------- | :----- | :--- | :------- |
| major_id   | NUMBER(8,0)      | 主键       | 否       |        |      | 专业id   |
| major_name | VARCHAR2(50BYTE) |            | 否       |        |      | 专业名称 |

<div id="course"></div>
### 6.课程表 course

| 字段        | 类型             | 主键、外键 | 可以为空 | 默认值 | 约束 | 说明     |
| :---------- | :--------------- | :--------- | :------- | :----- | :--- | :------- |
| course_id   | NUMBER(8,0)      | 主键       | 否       |        |      | 课程id   |
| course_name | VARCHAR2(50BYTE) |            | 否       |        |      | 课程名称 |

<div id="term"></div>
### 7.学期表 term

| 字段       | 类型             | 主键、外键 | 可以为空 | 默认值 | 约束 | 说明         |
| :--------- | :--------------- | :--------- | :------- | :----- | :--- | :----------- |
| term_id    | NUMBER(8,0)      | 主键       | 否       |        |      | 学期id       |
| term_name  | VARCHAR2(50BYTE) |            | 否       |        |      | 学期名称     |
| start_time | DATE             |            | 否       |        |      | 学期开始时间 |
| end_time   | DATE             |            | 否       |        |      | 学期结束时间 |

<div id="termInformation"></div>
### 8.学期信息表 termInformation

| 字段              | 类型        | 主键、外键 | 可以为空 | 默认值 | 约束 | 说明                                             |
| :---------------- | :---------- | :--------- | :------- | :----- | :--- | :----------------------------------------------- |
| major_id          | NUMBER(8,0) | 主键       | 否       |        |      | 开课课程教师关联id                               |
| term_id           | NUMBER(8,0) | 外键       | 否       |        |      | 课程、专业与学期关联编号，课程专业学期关联表外键 |
| teacher_course_id | NUMBER(8,0) | 外键       | 否       |        |      | 老师选择的课程id,course表外键                    |
| teacher_id        | NUMBER(8,0) | 外键       | 否       |        |      | 老师id,teachers表外键                            |
| class_id          | NUMBER(8,0) | 外键       | 否       |        |      | 学生班级id,class表外键                           |

<div id="tests"></div>
### 9.实验表 tests

| 字段    | 类型             | 主键、外键 | 可以为空 | 默认值 | 约束 | 说明     |
| :------ | :--------------- | :--------- | :------- | :----- | :--- | :------- |
| test_id | NUMBER(8,0)      | 主键       | 否       |        |      | 实验id   |
| title   | VARCHAR2(50BYTE) | 否         |          |        |      | 实验名称 |

<div id="testStandard"></div>
### 10.评分标准表 testStandard

| 字段                | 类型             | 主键、外键 | 可以为空 | 默认值 | 约束 | 说明               |
| :------------------ | :--------------- | :--------- | :------- | :----- | :--- | :----------------- |
| test_id             | NUMBER(8,0)      | 主键       | 否       |        |      | 评分标准id         |
| standard_info       | VARCHAR2(50BYTE) |            | 否       |        |      | 评分标准名称       |
| standard_proportion | NUMBER(8,0)      |            | 否       |        |      | 评分标准占的百分比 |

<div id="grades"></div>
### 11.实验总评分表 grades

| 字段        | 类型             | 主键、外键 | 可以为空 | 默认值 | 约束 | 说明                         |
| :---------- | :--------------- | :--------- | :------- | :----- | :--- | :--------------------------- |
| student_id  | VARCHAR2(50BYTE) | 主键       | 否       |        |      | 总评分id                     |
| result      | VARCHAR2(50BYTE) |            | 是       | 空     |      | 总评分分数，分数为空为未批改 |
| test_id     | NUMBER(8,0)      | 外键       | 否       |        |      | 实验id                       |
| memo        | VARCHAR2(50BYTE) |            | 否       |        |      | 老师评价                     |
| update_date | DATE             |            | 是       | 空     |      | 老师批改时间，为空为未批改   |



