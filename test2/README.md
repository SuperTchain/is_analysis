
# 实验2：图书管理系统用例建模
|     学号     |     班级     | 姓名 |
| :----------: | :----------: | :--: |
| 201710414108 | 软件(本)17-1 | 李兴 |
## 1. 图书管理系统的用例关系图

### 1.1 用例图源码：

``` usecase
@startuml
usecase (预定图书)
usecase (取消预定)
usecase (读者信息管理)
usecase (查询图书)
usecase (借出图书)
usecase (归还图书)
usecase (维护书目)
usecase (查询借阅情况)
usecase (购入图书)
usecase (管理系统)

actor :图书管理员:
actor :读者:
actor :系统管理员:

:图书管理员: --> (检索图书)
:图书管理员: --> (读者信息管理)
:图书管理员: --> (维护书目)
:图书管理员: --> (查询图书)
:图书管理员: --> (查询借阅情况)

:读者: --> (查询图书)
:读者: --> (查询借阅情况)
:读者: --> (预定查询)

:系统管理员: --> (管理系统)

(维护书目) --> (购入图书) : <<include>>
(检索图书) --> (借出图书) : <<include>>
(检索图书) --> (归还图书) : <<include>>
(预定查询) --> (预定图书) : <<include>>
(预定查询) --> (取消预定) : <<include>>

@enduml
```


### 1.2. 用例图如下：

![用例图片](plantuml1.png)	

## 2. 参与者说明：

###     2.1 图书管理员

主要职责是：管理图书馆所有的书籍借出与归还,管理图书，管理读者信息

###     2.2 读者

主要职责是：在图书馆中进行书目的查询，查询借阅情况，预定图书和取消预定图书

###     2.3 系统管理员

主要职责是：管理系统

## 3.用例规约图

### 3.1查询图书用例

用例流程图源码如下:

```puml
@startuml
start
:登陆图书管理系统;
:系统显示搜索界面;
:参与者输入查询图书名字;
if (默认查询方式？) then (yes)
  :按图书名称查询;
else (no)
  :按图书编码查询;
endif
:查询;
if (有查询结果？) then (yes)
  :系统返回查找信息;
else (no)
  :系统返回没有找到书籍信息;
endif
stop
@enduml
```

用例流程图如下:

![流程图](plantuml2.png)	

用例规约如下:

![规约图](img1.png)	

### 3.2预定图书用例

用例流程图源码如下:

```puml
@startuml
start
:登陆图书管理系统;
:系统显示搜索界面;
:参与者查询预定书籍;
if (默认查询方式？) then (yes)
  :按图书名称查询;
else (no)
  :按图书编码查询;
endif
:查询;
if (有查询结果？) then (yes)
  :系统返回查找信息;
else (no)
  :系统返回没有找到书籍信息;
endif
stop
@enduml
```

用例流程图如下:

![流程图](plantuml3.png)	

用例规约如下:

![规约图](img2.png)	

### 3.3取消预定用例

用例流程图源码如下:

```puml
@startuml
start
:登陆图书管理系统;
:系统显示预定界面;
:参与者取消预定图书;
if (取消成功) then (yes)
  :系统返回取消成功;
else (no)
  :系统返回没有预定书籍;
endif
stop
@enduml
```

用例流程图如下:

![流程图](plantuml4.png)	

用例规约如下:

![规约图](img3.png)	

### 3.4查询借阅情况用例

用例流程图源码如下:

```puml
@startuml
start
:登陆图书管理系统;
:系统显示借阅信息界面;
:参与者输入自己ID号;
if (查询成功) then (yes)
  :系统返回借阅信息;
else (no)
  :系统返回没有借阅书籍;
endif
stop
@enduml
```

用例流程图如下:

![流程图](plantuml5.png)	

用例规约如下:

![规约图](img4.png)	

### 3.5购入图书用例

用例流程图源码如下:

```puml
@startuml
start
:登陆图书管理系统;
:系统显示借阅信息界面;
:输入书籍名字、存放地址、数量、存放时间;
if (没有输入名字？) then (yes)
  :提示没有输入名字;
    stop
elseif (没有输入存放地址？) then (yes)
  :提示没有输入存放地址;
  stop
elseif (没有输入数量？) then (yes)
  :提示没有输入数量;
    stop
else (no)
  :系统确认输入信息、
  保存并返回保存结果;
endif
stop
@enduml
```

用例流程图如下:

![流程图](plantuml6.png)	

用例规约如下:

![规约图](img5.png)	

### 3.6借出图书用例

用例流程图源码如下:

```puml
@startuml
start
:选择一本书;
:选择书籍;
if (所选书籍剩余量为0？) then (yes)
  :输出提示：书籍没有库存了;
    stop
elseif (达最大借书量？) then (yes)
  :提示已经到达最大借书量;
  stop

else (no)
  :系统确认;
endif
:请求参与者确认;
if (用户确认？) then (yes)
  :借阅成功;
else (no)
  :取消借阅;
endif
stop
@enduml
```

用例流程图如下:

![流程图](plantuml7.png)	

用例规约如下:

![规约图](img6.png)

### 3.7归还图书用例

用例流程图源码如下:

```puml
@startuml
start
:系统显示归还界面;
:用户选择归还书籍;
:系统获得书籍信息、参与者信息并提示用户;
if (参与者确认？) then (yes)
  :还书成功;
else (no)
  :取消还书;
endif
stop
@enduml
```

用例流程图如下:

![流程图](plantuml8.png)	

用例规约如下:

![规约图](img7.png)		

### 3.8读者信息查询用例

用例流程图源码如下:

```puml
@startuml
start
:系统显示查询界面;
:参与者输入自己ID;
:系统进行查询;
 if (查询成功？) then (yes)
  :返回查询信息;
else (no)
  :查询失败;
endif
stop
@enduml
```

用例流程图如下:

![流程图](plantuml9.png)	

用例规约如下:

![规约图](img8.png)

### 3.9系统管理用例

用例流程图源码如下:

```puml
@startuml
start
:系统显示更新信息;
:参与者选择更新;
:系统更新;
 if (更新成功？) then (yes)
  :提示更新成功;
else (no)
  :提示更新失败;
endif
stop
@enduml
```

用例流程图如下:

![流程图](plantuml10.png)	

用例规约如下:

![规约图](img9.png)
