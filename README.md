# 说明文档
## 基于
1. HttpRunneManager: https://github.com/hui1hui2hui3/HttpRunnerManager
2. HttpRUnnerManager部署说明：https://testerhome.com/topics/13295
3. Docker

## 使用说明
### 一.下载HttprunnerManager项目
`git clone https://github.com/hui1hui2hui3/HttpRunnerManager.git`
### 二.创建数据存储目录，用于存放数据库文件
`mkdir mysql_data`
### 三.修改HttpRunnerManager/HttpRunnerManager/settings.py里DATABASES字典相关配置
1. 修改数据库的 HOST 字段的值为mysql
2. 使用root用户，密码为 1qaz@WSX
### 五.修改:HttpRunnerManager/HttpRunnerManager/settings.py里BROKER_URL字段
1. 将BROKER_URL = 'amqp://guest:guest@127.0.0.1:5672//'中的127.0.0.1替换为rabbitmq
### 六.完成数据库配置
1. `docker-compose up -d`启动项目
2. `docker ps`查看 httprunner 项目运行的镜像id
3. `docker exec -it 镜像id /bin/bash` 进入系统镜像
4. 镜像内输入`python manage.py makemigrations ApiManager`生成数据库迁移脚本
5. 镜像内输入`python manage.py migrate` 生成数据库
6. 镜像内输入`python manage.py createsuperuser` 创建超级用户名，完成后输入`exit`退出镜像
7. `docker-compose restart`重启服务
### 七.测试启动情况
1. 打开http://localhost:8000/admin/login/?next=/admin/ 输入管理密码确认管理用户正确性
2. 打开http://localhost:8000 注册普通用户，开始试用
3. 打开http://localhost:5555 访问定时服务
4. 打开http://localhost:15672 访问消息服务页面； 用户名和密码为： guest/guest


