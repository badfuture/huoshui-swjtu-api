# 交大瑞士刀api
尽量遵循RESTful风格编写，但有些地方可能仍然不符合标准
### docs
1. 验证用户身份/获得接口权限
```
POST https://api.wangzhe.cloud/login
　　　form={"username":"20132333","password":"123456"}
=>
{
    "statuscode": 0,
    "status": "authorized"
}
```
2. 获取基本信息
```
GET https://api.wangzhe.cloud/info
=>
{
    "statuscode": 0,
    "status": "success",
    "name": "xxx",
    "sex": "男",
    "grade": "2013",//学号除去最后4位
    "major": "软件工程",
    "class": "软件2013-02班"
}
```
3. 获取平均分/排名
```
GET https://api.wangzhe.cloud/rank
=>
{
    "statuscode": 0,
    "status": "success",
    "mean": 100.0,
    "rank": 1,
    "all": 118,
    "validcourses": [
        {
            "name":"线性代数B",
            "score":"100.0"
        },
        ...
     ],
     "invalidcourses": [
        {
            "name":"体育Ⅰ",
            "score":"100.0"
        },
          ...
      ]
}
```
4. 获取自定义有效课程下的平均分/排名
```
POST https://api.wangzhe.cloud/rank
     json=[{"name":"高等数学Ⅰ","score":"100.0"},...]//所有自定义有效课程,由于可能存在重修的情况,故必须带上score
=>
{
    "statuscode": 0,
    "status": "success",
    "mean": 100.0,
    "rank": 1,
    "all": 118,
    "validcourses": [
        {
            "name":"线性代数B",
            "score":"100.0"
        },
        ...
     ],
     "invalidcourses": [
        {
            "name":"体育Ⅰ",
            "score":"100.0"
        },
        ...
    ]
}
```
5. 查询老师给分
```
GET https://api.wangzhe.cloud/courses?name=高等数学
=>
{
    "statuscode": 0,
    "status": "success",
    "courses": [
        {
            "courseid": "6010320",
            "coursename": "高等数学CⅡ",
            "teachers": [
                {
                    "name": "王中宝",
                    "all": "294", //成绩记录总数
                    "E": "27", //60分以下记录数
                    "A": "68", //90分及以上记录数
                    "mean": "76.81",
                    "std": "18.67"
                },
                ...//１到多个老师
            ],
        },
        ...//0到多个课程
    ]
}
```
6. 查询所在专业免研主干课程
```
GET https://api.wangzhe.cloud/majorcourses
=>
{
    "statuscode": 0,
    "status": "success",
    "majors": [
        {
            "majorcode": "0408",
            "majorname": "软件工程",
            "collegecode": "04",
            "collegename": "信息科学与技术学院",
            "courses": [
                {
                    "id": "3244153",
                    "name": "编译原理B",
                    "type": "必",
                    "credit": "4.0",
                    "remark": "" //备注
                },
                ...//1到多个课程
            ],
        },
        ...//0到多个专业
    ]
}
```
### 其他
1. 查询接口列表
```
GET https://api.wangzhe.cloud
=>
```
2. 网页登录表单（手动测试用）
```
GET https://api.wangzhe.cloud/loginform
```

3. 查询登录状态/接口权限
```
GET https://api.wangzhe.cloud/login
已登录=>
{
    "statuscode": 0,
    "status": "authorized"
}
未登录=>
{
    "statuscode": -1,
    "status": "unauthorized"
}
```