# 实验3：图书管理系统领域对象建模
|     学号     |     班级     | 姓名 |
| :----------: | :----------: | :--: |
| 201710414108 | 软件(本)17-1 | 李兴 |
## 1. 图书管理系统的类图

### 1.1类图PlantUML源码如下：

```puml
@startuml
class 读者{
    -readerid:Long
    -readername:String
    -readeraddress:String
    -readerphone:String
    +borrowBook():Boolean
    +returnBook():Boolean
}

class 图书管理员{
    -bookadminid:Long
    -bookadminname:String
    -bookadminphone:String
    +buyBook()：Boolean
    +retrievalBorrow():Boolean
    +retrievalReturm():Boolean
    +manageReaderMessage():Reader
}

class 系统管理员{
    -adminid:String
    -adminname:String
    -readeraccount:String
    -readerpassword:String
    -bookadminaccoint:String
    -bookadminpassword:String
    +manageSystem():Syetem
    +manageReaderMessage():Reader
    +manageBookAdminMessage():BookAdmin
}

class 查询{
    -queryid:Long
    -queryName:String
    +queryBorrow()：Reader
    +queryBook():Book
}



class 图书{
    -bookid:Long
    -bookname:String
    -bookauthor:String
    -bookstatus:Boolean
    -bookprice:Long
    -booknumber:Long
    -bookborrownumber:Long
    -bookreservenumber:Long
    -bookdata:Date
}
class 预定{
    -reverseid:Long
    -reversename:String
    +reserveBook():Boolean
    -canclereserveid:Long
    -canclereservename:String
    +cancleReserve():Boolean
}

class 购入{
    -booknum:Long
    -bookid:Long
    -bookprice:Long
}

class 借还{
    -bookid:Long
    -bookname:String
    -borrowreaderid:Long
    -borrowtime:Date
    -returntime:Date
    -returnreaderid:Long
}
class 读者管理{
    -readeraccount:Long
    -readerpassword:String
    -readeraddress:String
    -readerphone:String
}

查询  -- "1" 图书
读者 "1" -- "*" 查询
图书管理员 "1" -- "*" 查询
预定 "*" -- 读者:has
图书管理员 "1" -- "*" 购入
图书管理员 "1" -- "*" 借还
借还 "*" -- 读者:has
读者管理 "*" -- "1" 图书管理员
系统管理员 -- "*"图书管理员
系统管理员 -- "*"读者
@enduml
```

### 1.2类图如下:

![类图](./Img/plantuml1.png)	

### 1.3类图说明:

对于一个读者来说他可以多次借书还书，多次预定退订图书；对于一个图书管理员来说他可以购入多本图书，可以多次管理借还书的情况，可以管理多个读者的信息；图书管理员和读者都可以多次查询图书情况，而根据图书名和编号查询的结果一般只对应一种查询结果；系统管理员可以管理多个图书管理员和读者。

## 2.图书管理系统的对象图

### 2.1类读者(Reader)的对象图

#### 2.1.1源码如下：

```puml
@startuml

object Reader
Reader : readerid=123
Reader : readername="Dummy“
Reader : readeraddress="dada"
Reader : readerphone="123141"

@enduml
```

#### 2.1.2对象图如下:

![Reader对象图](./Img/readerpuml.png)	

### 2.2类图书管理员(BookAdmin)的对象图

#### 2.2.1源码如下:

```puml
@startuml

object BookAdmin
BookAdmin : bookadminid=1
BookAdmin : bookadminname="dad"
BookAdmin : bookadminphone="123"
BookAdmin : bookadmiaddress="dading"
@enduml
```



#### 2.2.2对象图如下:

![图书管理员的对象图](./Img/bookadmin.png)	

### 2.3类系统管理员(SystemManager)的对象图

#### 2.3.1源码如下:

```puml
@startuml

object SystemManager
SystemManager : adminid=1
SystemManager : adminname="dad"
SystemManager : readeraccount=1213
SystemManager : readerpassword="adad"
SystemManager : bookadminaccoint=234
SystemManager : bookadminpassword="dadad"
@enduml
```



#### 2.3.2对象图如下:

![图书管理员的对象图](./Img/systemmanager.png)		

### 2.4类查询(Query)的对象图

#### 2.3.1源码如下:

```puml
@startuml

object Query
Query : queryid=1
Query : queryName="dad"

@enduml
```



#### 2.3.2对象图如下:

![图书管理员的对象图](./Img/query.png)			

### 2.5类图书(Book)的对象图

#### 2.5.1源码如下:

```puml
@startuml

object Book
Book : bookid=1
Book : bookname="dad"
Book : bookauthor="dadd"
Book : bookstatus=true
Book : bookprice="213"
Book : booknumber="2123"
Book : bookborrownumber=123
Book : bookreservenumber=3434
Book : bookdata:2021-4-6

@enduml
```



#### 2.5.2对象图如下:

![图书管理员的对象图](./Img/book.png)		

### 2.6类购入(Bought)的对象图

#### 2.6.1源码如下:

```puml
@startuml

object Bought
Bought : booknum=1
Bought : bookid=23
Bought : bookprice=213

@enduml
```



#### 2.6.2对象图如下:

![图书管理员的对象图](./Img/bought.png)			

### 2.7类借还(BorrowReturn)的对象图

#### 2.7.1源码如下:

```puml
@startuml

object BoughtReturn
BoughtReturn : bookid=1
BoughtReturn : bookname="dad"
BoughtReturn : borrowreaderid=2
BoughtReturn : borrowtime=2020-4-6
BoughtReturn : returntime=2020-4-6
BoughtReturn : returnreaderid=2

@enduml
```



#### 2.7.2对象图如下:

![图书管理员的对象图](./Img/borrowreturn.png)	

### 2.8类预定(Reverse)的对象图

#### 2.8.1源码如下:

```puml
@startuml

object Reverse
Reverse : reverseid=1
Reverse : reversename="dad"
Reverse : canclereserveid=23
Reverse : canclereservename="dad"

@enduml
```



#### 2.8.2对象图如下:

![图书管理员的对象图](./Img/reverse.png)	