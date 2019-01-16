# 说明文档
## 基于
1. HttpRunneManager: https://github.com/hui1hui2hui3/HttpRunnerManager
2. HttpRUnnerManager部署说明：https://testerhome.com/topics/13295
3. Docker

## 使用说明
### 一.下载HttprunnerManager项目
1. `git clone https://github.com/hui1hui2hui3/HttpRunnerManager.git`
2. 进入HttpRunneManager目录，切换分支到dev_huis
3. 进入到static目录，执行`npm install`安装第三方库
### 二.修改HttpRunnerManager/HttpRunnerManager/settings.py里DATABASES字典相关配置
1. NAME为 'HttpRunner' 
2. USER为 'root'
3. PASSWORD为 '1qaz@WSX'
4. HOST为 'mysql'
### 三.修改:HttpRunnerManager/HttpRunnerManager/settings.py里BROKER_URL字段
1. 将BROKER_URL = 'amqp://guest:guest@localhost:5672//'中的localhost替换为rabbitmq
### 四.退回到httprunner_docker目录，创建数据存储目录，用于存放数据库文件
`mkdir mysql_data`
### 五.完善数据库生成
1. `docker-compose up -d`启动项目
2. `docker ps`查看 httprunner 项目运行的镜像id
3. `docker exec -it 镜像id /bin/bash` 进入系统镜像
4. 镜像内输入`python manage.py makemigrations ApiManager`生成数据库迁移脚本
5. 镜像内输入`python manage.py migrate` 生成数据库
6. 镜像内输入`python manage.py createsuperuser` 创建超级用户名，完成后输入`exit`退出镜像
7. `docker-compose restart web`重启服务
### 七.测试启动情况
1. 打开http://localhost:8000/admin/login/?next=/admin/ 输入管理密码确认管理用户正确性
2. 打开http://localhost:8000 注册普通用户，开始试用
3. 打开http://localhost:5555 访问定时服务
4. 打开http://localhost:15672 访问消息服务页面； 用户名和密码为： guest/guest


