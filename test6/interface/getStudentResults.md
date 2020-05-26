# 接口：getStudentResults  [返回](../README.md)

用例： [查看成绩](../example/查看成绩.md)，[评定成绩](../example/评定成绩.md)

- 功能：
  返回一个学生的所有实验成绩和实验评价。

- 权限：
  学生：只能查看自己的成绩，即接口参数student_id必须等于登录学生的student_id
  老师：可以查看所有学生的成绩。

- API请求地址： 
  接口基本地址/v1/api/getOneStudentResults/<student_id>&&<course_teacher_id>

- 请求方式 ：
  GET

- 请求参数说明:        

  |     参数名称      | 说明         |
  | :---------------: | :----------- |
  |    student_id     | 学生的学号   |
  | course_teacher_id | 关联课程编号 |

- 返回实例：

  ```json
  {         
      "code":200,
      "msg":"查询成功",   
      "data":{
          "student_id": "201510315203", 
          "github_username": "chinajuedui", 
          "class": "软件(本)16-4", 
          "name": "李兴", 
          "total": 6,
          "avgresult":90.5,       
          "data": [
                      {
                      "total_score_id":1,
                      "total_score": 80, 
                      "test_name":"实验1",
                      "test_url":"xxxx",
                      "total_memo":"太棒了",
                      "update_date": "2020-05-25 20:20:20",
                      web_exists:"true",
                      }, 
                      {
                      ...其他实验
                      }
          ] 
       }
  }
  ```

- 返回参数说明：    

  |    参数名称     | 说明                           |
  | :-------------: | :----------------------------- |
  |      code       | 返回结果状态码                 |
  |       msg       | 返回结果说明信息               |
  |      data       | 查询到的相应信息               |
  |   student_id    | 学号                           |
  | github_username | 学生的gitHub用户名             |
  |      class      | 专业班级                       |
  |      name       | 真实姓名                       |
  |      total      | 实验总数                       |
  |    avgresult    | 实验平均成绩                   |
  |      data       | 所有实验的成绩和评语           |
  | total_score_id  | 总评分编号                     |
  |    test_name    | 实验名称                       |
  |    test_url     | 实验要求url                    |
  |   web_exists    | 本实验的GitHub网页是否存在     |
  |   total_memo    | 本实验老师的总评价，可以为空   |
  |   update_date   | 本实验老师的批改日期，可以为空 |

