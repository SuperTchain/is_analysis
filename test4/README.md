# 实验4：图书管理系统领域对象建模
|     学号     |     班级     | 姓名 |
| :----------: | :----------: | :--: |
| 201710414108 | 软件(本)17-1 | 李兴 |

## 图书管理系统的顺序图

---

### 1.借书用例

#### 1.1借书用例PlantUML源码

```puml
@startuml
actor ": 图书管理员" as 图书管理员
participant ": 读者" as 读者
participant ": 图书目录" as 图书目录
participant ": 图书信息" as 图书信息
participant ": 借书记录" as 借书记录
skinparam sequenceParticipant underline
图书管理员 -> 读者:验证读者信息
activate 图书管理员
activate 读者
deactivate 读者
图书管理员 -> 读者:获取读者借书数量
activate 读者
opt 超出借书数量
读者-->图书管理员:借书失败
deactivate 读者
图书管理员 -> 图书目录:获取图书目录
activate 图书目录
图书目录 -> 图书信息:查询图书信息
deactivate 图书目录
activate 图书信息
图书信息 -->图书管理员:返回信息
deactivate 图书信息
图书管理员 -> 借书记录:存储借书记录
activate 借书记录
deactivate 借书记录
图书管理员 -> 图书目录:借出图书
activate 图书目录
图书目录 -> 图书信息:减少图书数量
activate 图书信息
deactivate 图书信息
deactivate 图书目录
图书管理员 -> 读者:减少读者可借数量
activate 读者
deactivate 读者
end
deactivate 借书记录
deactivate 图书管理员
@enduml
```

#### 1.2借书用例顺序图

![借书顺序图](./Img/pl1.png)	

#### 1.3借书用例顺序图说明

图书管理员首先查询读者的信息，根据查询的信息获取读者借书数量，然后判断其数量是否超过可借数量，如果超过可借数量则借书失败，没超过则获取图书目录，查询改图书信息，得到信息后创建一条借书记录然后借出图书，之后减少借出图书的数量，减少读者可借书的数量，结束流程。

### 2.还书用例

#### 2.1还书用例PlantUML源码

```puml
@startuml
actor ": 图书管理员" as 图书管理员
participant ": 读者" as 读者
participant ": 图书目录" as 图书目录
participant ": 图书信息" as 图书信息
participant ": 借书记录" as 借书记录
participant ": 逾期记录" as 逾期记录
participant ": 罚款" as 罚款
skinparam sequenceParticipant underline
图书管理员 -> 读者:验证读者信息
activate 读者
deactivate 读者
图书管理员 -> 图书目录:获取图书目录
activate 图书管理员
activate 图书目录
图书目录 -> 图书信息:查询图书信息
deactivate 图书目录
activate 图书信息
图书信息 -->图书管理员:返回信息
deactivate 图书信息
图书管理员 -> 借书记录:查询借书记录
activate 借书记录
借书记录 --> 图书管理员:返回借书记录
deactivate 借书记录
图书管理员 -> 图书目录:归还图书
activate 图书目录
图书目录 -> 图书信息:增加图书数量
activate 图书信息
deactivate 图书信息
deactivate 图书目录
图书管理员 -> 借书记录:记录还书时间
activate 借书记录
deactivate 借书记录
opt 超过期限
图书管理员 -> 逾期记录:记录过期记录
activate 逾期记录
逾期记录->罚款:罚款
activate 罚款
deactivate 罚款
逾期记录 --> 图书管理员:返回过期信息
deactivate 逾期记录
图书管理员->读者:增加借书数量
activate 读者
deactivate 读者
end
deactivate 图书管理员
@enduml
```

#### 2.2还书用例顺序图

![借书顺序图](./Img/pl2.png)	

#### 2.3还书用例顺序图说明

图书管理员首先查询读者的信息，根据查询的信息获取图书目录信息，然后查询图书信息，根据返回信息查询借书记录，得到借书记录后归还图书，增加图书数量，记录换书时间；如果超过还书时间则进行罚款，在还书之后增加读者借书的数量，结束流程。

### 3.购入图书用例

#### 3.1购入图书用例PlantUML源码

```puml
@startuml
actor ": 图书管理员" as 图书管理员
participant ": 图书目录" as 图书目录
participant ": 图书类型" as 图书类型
skinparam sequenceParticipant underline
activate 图书管理员
图书管理员->图书管理员:登录
图书管理员->图书目录:查询图书信息
activate 图书目录
图书目录->图书类型:图书类型查询
activate 图书类型
图书类型-->图书目录:返回图书类型信息
deactivate 图书类型
图书目录-->图书管理员:返回图书信息
deactivate 图书目录
图书管理员->图书目录:添加图书信息
activate 图书目录
图书目录->图书类型:图书类型信息修改
activate 图书类型
deactivate 图书类型
deactivate 图书目录
deactivate 图书管理员
@enduml
```

#### 3.2购入图书用例顺序图

![借书顺序图](./Img/pl3.png)		

#### 3.3购入图书用例顺序图说明

图书管理员首先登录自己账号，然后可以先查询图书目录，再根据图书类型进行查询，返回图书类型信息之后在查询信息，得到信息之后就可以添加购入图书的信息，图书信息被修改，借书流程。

### 4.预定图书用例

#### 4.1预定图书用例PlantUML源码

```puml
@startuml
actor ": 读者" as 读者
participant ": 预定记录" as 预定记录
participant ": 图书目录" as 图书目录
participant ": 图书信息" as 图书信息
skinparam sequenceParticipant underline
activate 读者
读者->读者:登录
读者->图书目录:查询图书目录
activate 图书目录
图书目录->图书信息:查询图书信息
activate 图书信息
图书信息-->读者:返回查询信息
deactivate 图书信息
deactivate 图书目录
读者->预定记录:查询可预定图书数量
activate 预定记录
预定记录-->读者:返回查询信息
opt 没有预定记录
读者-->图书目录:预定图书
end
opt 有预定记录
读者->图书信息:查询预定图书信息
deactivate 预定记录
end
@enduml
```

#### 4.2预定图书用例顺序图

![借书顺序图](./Img/pl4.png)			

#### 4.3预定图书用例顺序图说明

读者首先登录自己账号，然后可以查询图书目录，再根据目录查询图书信息，得到查询信息，然后可以查询可预订图书数量，根据返回信息进行判断，如果没有预定记录则可以预定图书，有预定图书信息，可以直接查询已预定图书信息。

### 5.取消预定图书用例

#### 5.1取消预定图书用例PlantUML源码

```puml
@startuml
actor ": 读者" as 读者
participant ": 预定记录" as 预定记录
skinparam sequenceParticipant underline
activate 读者
读者->读者:登录
读者->预定记录:查看预定记录
activate 预定记录
opt 没有预定记录
预定记录-->读者:返回未查询到预定记录
end
opt 有预定记录
读者->预定记录:删除预定记录
end
deactivate 读者
@enduml
```

#### 5.2取消预定图书用例顺序图

![借书顺序图](./Img/pl5.png)				

#### 5.3取消预定图书用例顺序图说明

读者首先登录自己账号，然后查看预定记录，根据返回记录进行选择，没有预定记录就不用管，有预定记录则可以删除预定记录，结束流程。

### 6.查询图书用例

#### 6.1查询图书用例PlantUML源码

```puml
@startuml
actor 读者
actor ": 读者" as 读者
participant ": 图书目录" as 图书目录
participant ": 图书信息" as 图书信息
skinparam sequenceParticipant underline
activate 读者
读者->读者:登录
读者->图书目录:查询图书目录
activate 图书目录
图书目录->图书信息:查询图书信息
activate 图书信息
图书信息->读者:返回查询信息
deactivate 图书信息
deactivate 读者
@enduml
```

#### 6.2查询图书用例顺序图

![借书顺序图](./Img/pl6.png)					

#### 6.3查询图书用例顺序图说明

读者首先登录自己账号，然后可以查看图书目录，根据图书目录查询图书信息，然后得到查询的信息，结束流程。

### 7.读者信息管理用例

#### 7.1读者信息管理用例PlantUML源码

```puml
@startuml
actor ": 图书管理员" as 图书管理员
participant ": 读者" as 读者
skinparam sequenceParticipant underline
activate 图书管理员
图书管理员->图书管理员:登录
图书管理员->读者:查询读者信息
activate 读者
读者-->图书管理员:返回读者信息
deactivate 读者
图书管理员->读者:管理读者信息
activate 读者
deactivate 读者
deactivate 图书管理员
@enduml
```

#### 7.2读者信息管理用例顺序图

![借书顺序图](./Img/pl7.png)					

#### 7.3读者信息管理用例顺序图说明

图书管理员首先登录自己账号，然后可以查询读者信息，根据返回的读者信息可以管理读者信息，结束流程。

### 8.系统管理用例

#### 8.1系统管理用例PlantUML源码

```puml
@startuml
actor ": 系统管理员" as 系统管理员
participant ": 系统" as 系统
skinparam sequenceParticipant underline
activate 系统管理员
系统管理员->系统管理员:登录
系统管理员->系统:查询系统信息
activate 系统
系统-->系统管理员:返回系统信息
deactivate 系统
系统管理员->系统:升级系统
opt 升级成功
activate 系统
系统->系统管理员:升级成功
end
opt 升级失败
系统->系统管理员:返回失败原因
end
deactivate 系统
deactivate 系统管理员
@enduml
```

#### 8.2系统管理用例顺序图

![借书顺序图](./Img/pl8.png)					

#### 8.3系统管理用例顺序图说明

系统管理员首先登录自己账号，然后可以查询系统信息，根据返回系统信息可选择升级系统，如果升级成功，则系统会返回成功消息，若升级失败，系统返回失败原因，结束流程。