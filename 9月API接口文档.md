#<center>**9月API接口文档**</center>  
##用户模块接口
###1.获得验证码
###### URL
> [www.domain/code](www.api.com/index.php)

###### 支持格式
> JSON

###### HTTP请求方式
> GET

###### 请求参数
> |参数|必选|类型|说明|
|:-----  |:-------|:-----|-----                               |
|time   |ture    |int|当前时间戳(用于判断请求是否超时)                          |
|username    |ture    |string|用户手机号或邮箱                          |
|is_exist  |true    |int   |username是否应该存在(1:是 0:否)）|

######tips
>1.md5加密方式 如：token=md5('api_'.md5(username).md5(time).md5(is_exist))'api_'.)
2.用户注册时is_exist = 0，用户找回密码时is_exist = 1；
###### 接口示例
``` javascript
{
    "code": 200,
    "msg": "手机验证码已经发送成功, 每天可以发送5次, 请在一分钟内验证!",
    "data": []
}
``` 
###2.用户注册
###### URL
> [www.domain/user/register]([www.dmomain/user/register)

###### 支持格式
> JSON

###### HTTP请求方式
> POST

###### 请求参数
> |参数|必选|类型|说明|
|:-----  |:-------|:-----|-----                               |
|time   |ture    |int|当前时间戳(用于判断请求是否超时                          |
|username    |ture    |string|用户手机号                          |
|password   |true    |string   |用户密码（暂时MD5加密传输）|
|code   |true    |int   |用户收到的验证码|

###### 接口示例
``` javascript
{
    "code": 200,
    "msg": "注册成功!",
    "data": []
}
``` 
###3.用户登录
###### URL
> [www.domain/user/login]([www.dmomain/user/login)

###### 支持格式
> JSON

###### HTTP请求方式
> POST

###### 请求参数
> |参数|必选|类型|说明|
|:-----  |:-------|:-----|-----                               |
|time   |ture    |int|当前时间戳(用于判断请求是否超时                          |
|username    |ture    |string|用户手机号                          |
|password   |true    |string   |用户密码（暂时MD5加密传输）|
|rember   |false    |int  |用户是否想自动登录,自动登录rember参数存在|


###### 接口示例
``` javascript
{
    "code": "200",
    "msg": "用户登录成功",
    "data": {
        "uid": 1,
        "username": "test",
        "phone": "18888888888",
        "email": "cyrus@ipdle.com",
        "rtime": null,
        "uuid": "M8Cq4iF9s2Eb4Lp3eR6q",
        "token": "a6edb1bb81a203fab35b91b29ef6c03c",
    }
}
``` 
###4.确认用户登录状态（自动登录，判断用户是否登录）
###### URL
> [www.domain/user/check_login]([www.dmomain/user/check_login)

###### 支持格式
> JSON

###### HTTP请求方式
> POST

###### 请求参数
> |参数|必选|类型|说明|
|:-----  |:-------|:-----|-----                               |
|time   |ture    |int|当前时间戳(用于判断请求是否超时                          |
|token   |true    |string  |确定来访者身份|
|uuid   |true    |string  |用户登录表示，若用户第一次登录为空|

######tips
>1.现阶段想法是用户打开网页时判断用户是否登录，登录返回用户已登录
未登录判断用户是否选择自动登录，若cookie信息正确，用户自动登录且返回登录信息，否则返回错误信息
###### 接口示例
``` javascript
{
    "code": 200,
    "msg": "自动登录成功",
    "data": {
        "uid": 1,
        "username": "test",
        "uuid": "M8Cq4iF9s2Eb4Lp3eR6q",
        "email": "cyrus@ipdle.com",
        "phone": "18888888888",
        "certs": null,
        "rtime": null,
        "token": "56993ce3559ee06fc3d6f62627032434"
    }
}
``` 
###5.用户修改密码
###### URL
> [www.domain/user/change_pwd]([www.dmomain/user/change_pwd)

###### 支持格式
> JSON

###### HTTP请求方式
> POST

###### 请求参数
> |参数|必选|类型|说明|
|:-----  |:-------|:-----|-----                               |
|time   |ture    |int|当前时间戳(用于判断请求是否超时                          |
|token   |true    |string  |确定来访者身份|
|username    |ture    |string|用户手机号                          |
|ex_password   |true    |string   |用户原密码（暂时MD5加密传输）|
|password  |true    |string   |用户新密码|
|uuid    |ture    |string|用户编号    |


###### 接口示例
``` javascript
{
    "code": 200,
    "msg": "密码修改成功",
    "data": []
}
``` 
###6.用户找回密码
###### URL
> [www.domain/user/find_pwd]([www.dmomain/user/find_pwd)

###### 支持格式
> JSON

###### HTTP请求方式
> POST

###### 请求参数
> |参数|必选|类型|说明|
|:-----  |:-------|:-----|-----                               |
|time   |ture    |int|当前时间戳(用于判断请求是否超时                          |
|token   |true    |string  |确定来访者身份|
|username    |ture    |string|用户手机号                          |
|password   |true    |string   |用户新密码（暂时MD5加密传输）|
|code  |true    |int  |用户验证码|
|uuid    |ture    |string|用户id标识                      |

###### 接口示例
``` javascript
{
    "code": 200,
    "msg": "密码修改成功",
    "data": []
}
``` 

###7.用户修改昵称
###### URL
> [www.domain/user/nickname]([www.dmomain/user/nickname)

###### 支持格式
> JSON

###### HTTP请求方式
> POST

###### 请求参数
> |参数|必选|类型|说明|
|:-----  |:-------|:-----|-----                               |
|time   |ture    |int|当前时间戳(用于判断请求是否超时                          |
|token   |true    |string  |确定来访者身份|
|uuid    |ture    |string|用户id标识                      |
|nickname  |true    |string  |用户昵称|

###### 接口示例
``` javascript
{
    "code": 200,
    "msg": "昵称修改成功!",
    "data": []
}
``` 


###8.用户绑定邮箱
###### URL
> [www.domain/user/bind_email]([www.dmomain/user/bind_email)

###### 支持格式
> JSON

###### HTTP请求方式
> POST

###### 请求参数
> |参数|必选|类型|说明|
|:-----  |:-------|:-----|-----                               |
|time   |ture    |int|当前时间戳(用于判断请求是否超时                          |
|token   |true    |string  |确定来访者身份|
|uuid   |ture    |string|用户id标识     
|code    |ture    |int|验证码                         |
|email |true    |string  |用户的邮箱|


###### 接口示例
``` javascript
{
    "code": 200,
    "msg": "邮箱绑定成功!",
    "data": []
}
``` 

###9.用户退出登录
###### URL
> [www.domain/user/logout]([www.dmomain/user/logout)

###### 支持格式
> JSON

###### HTTP请求方式
> POST

###### 请求参数
> |参数|必选|类型|说明|
|:-----  |:-------|:-----|-----                               |
|time   |ture    |int|当前时间戳(用于判断请求是否超时                          |
|token   |true    |string  |确定来访者身份|
|uuid    |ture    |string|用户登录标识    |


###### 接口示例
``` javascript
{
    "code": 200,
    "msg": "用户退出登录成功",
    "data": []
}
``` 
###10.app登录接口(获取token)
###### URL
> [www.domain/user/get_app_token]([www.dmomain/user/get_app_token)

###### 支持格式
> JSON

###### HTTP请求方式
> POST

###### 请求参数
> |参数|必选|类型|说明|
|:-----  |:-------|:-----|-----                               |
|time   |ture    |int|当前时间戳(用于判断请求是否超时                          |
|token   |true    |string  |登录认证令牌，第一次登录为空|
|username    |ture    |string|用户手机号                          |
|password   |true    |string   |用户密码（暂时MD5加密传输）|


###### 接口示例
``` javascript
{
    "code": "200",
    "msg": "用户登录成功！",
    "data": {
        "app_token": "b4944ae017b1cd615679e11daeb321ef",
        "expire_in": 1553174465,
        "refresh_token": "17f2b618d67c0f089d32158326aa2214",
        "uuid": "M8Cq4iF9s2Eb4Lp3eR6q",
    }
}
``` 
###11.app刷新token登录令牌
###### URL
> [www.domain/user/refur_app_token]([www.dmomain/user/refur_app_token)

###### 支持格式
> JSON

###### HTTP请求方式
> POST

###### 请求参数
> |参数|必选|类型|说明|
|:-----  |:-------|:-----|-----                               |
|time   |ture    |int|当前时间戳(用于判断请求是否超时                          |
|username    |ture    |string|用户手机号                          |
|refresh_token   |true    |string   |用户刷新token令牌|
|uuid    |ture    |string|用户id标识                      |


###### 接口示例
``` javascript
{
    "code": "200",
    "msg": "自动登录成功",
    "data": {
        "app_token": "b35e3b9e2151de5b7ba6a4138fcebda0",
        "expire_in": 1553174993,
        "refresh_token": "22bc5a50808277c491c2d14b7e01bc53"
    }
}
``` 
###12.token认证接口(自动登录)
###### URL
> [www.domain/user/check_app_token]([www.dmomain/user/check_app_token)

###### 支持格式
> JSON

###### HTTP请求方式
> POST

###### 请求参数
> |参数|必选|类型|说明|
|:-----  |:-------|:-----|-----                               |
|time   |ture    |int|当前时间戳(用于判断请求是否超时                          |
|token   |true    |string  |确定来访者身份|
|username    |ture    |string|用户手机号                          |
|uuid    |ture    |string|用户id标识                      |
######tips
1.app_token为空时跳转到登录界面，过期时跳转到刷新token登录令牌接口，正确则直接登录

###### 接口示例
``` javascript
{
    "code": "200",
    "msg": "自动登录成功",
    "data": []
}
```
###13.搜索接口
###### URL
> [www.domain/user/research]([www.dmomain/user/research)

###### 支持格式
> JSON

###### HTTP请求方式
> POST

###### 请求参数
> |参数|必选|类型|说明|
|:-----  |:-------|:-----|-----                               |
|time   |ture    |int|当前时间戳(用于判断请求是否超时                          |
|token   |true    |string  |确定来访者身份|
|type    |ture    |string|0 昵称 1 科目 2 年级 3 空闲时间 4 地点         |
|subject   |false   |string  |科目|
|grade  |false    |string  |年级|
|restime  |false    |string  |时间|
|location  |false    |string  |地点|

######tips
>当前只有type=0时有效

###### 接口示例
``` javascript
{
    "code": 200,
    "msg": "搜索成功",
    "data": "M8Cq4iF9s2Eb4Lp3eR6q" //用户uuid
}
``` 





