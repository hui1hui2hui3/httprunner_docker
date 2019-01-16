# 说明文档
## 基于
HttpRunneManager: https://github.com/hui1hui2hui3/HttpRunnerManager
Docker

## 使用说明
### 一.下载HttprunnerManager项目
### 二.创建数据存储目录，用于存放数据库文件
### 三.修改docker-compose.yml文件
1. 将"your_mysql_data_path"替换为你创建的目录路径；比如：/home/user/mysql_data
2. 将"your_root_password"替换为你想要设置的root密码
3. 将"your_httprunnermanager_path"替换为你的httprunnermanager所在目录 
### 四.修改HttpRunnerManager/HttpRunnerManager/settings.py里DATABASES字典相关配置,具体信息根据docker-compose.yml中的配置
1. 注意修改数据库的HOST为mysql  也就是docker-compose中mysql的镜像名称 
### 五.修改:HttpRunnerManager/HttpRunnerManager/settings.py里BROKER_URL = 'amqp://guest:guest@127.0.0.1:5672//'将127.0.0.1替换为rabbitmq 也就是docker-compose中rabbimq的镜像名称
### 六.第一次启动，完成数据库配置
1. 切换到该项目下，`docker-compose up -d`启动项目
2. `docker ps`查看httprunner项目运行的镜像id
3. `docker exec -it 镜像id /bin/bash` 进入系统镜像
4. 运行`python manage.py makemigrations ApiManager`生成数据库迁移脚本
5. 运行`python manage.py migrate` 生成数据库
6. 运行`python manage.py createsuperuser` 根据提示输入超级用户名，邮箱，密码
7. `docker-compose restart`重启服务
### 七.测试启动情况
1. 打开http://localhost:8000/admin/login/?next=/admin/ 输入管理密码确认管理用户正确性
2. 打开http://localhost:8000 注册普通用户，开始试用
3. 打开http://localhost:5555 访问定时服务
4. 打开http://localhost:15672 访问消息服务页面； 用户名和密码为： guest/guest


