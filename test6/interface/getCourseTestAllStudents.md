# 接口：getCourseTestAllStudents  [返回](../README.md)
用例： [查看学生信息](../example/查看学生列表.md)

- 功能：
    查看当前课程实验下的全部学生信息
- 权限：
    教师、学生
    
- API请求地址： 
    接口基本地址/v1/api/getCourseTestAllStudents

- 请求方式 ：
    POST

- 请求实例：
    无
    
- 请求参数说明:        

- 返回实例：

        { 
            "code":200,
            "msg":"查询成功",
            "data":[{
            "student_id":"123",
            "student_name":"李兴",
            "grade_class":"2017级1班"
            }]   
        }

- 返回参数说明：    

  |参数名称|说明|
  |:---------:|:--------------------------------------------------------|
  |code|返回结果状态码|
  |msg|返回结果说明信息|
  |data|查询到的相应信息|
