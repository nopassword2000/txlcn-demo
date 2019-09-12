txlcn 5.0 demo


使用说明:
0.测试demo默认使用eureka作为注册中心，也可以使用consul作为注册中心
准备：安装mysql redis consul
本人使用docker 直接安装，主要是简单，哈哈
a)mysql 安装
  docker pull mysql:5.7
  docker run -p 3306:3306 --name mymysql -v /home/nopassword/mysql/conf:/etc/mysql/conf.d -v /home/nopassword/mysql/logs:/logs -v /home/nopassword/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 -d mysql:5.7
b)安装redis
   docker pull redis
   docker run -p 6379:6379 -v /home/nopassword/redis/data:/data  -d redis:latest redis-server --appendonly yes
c)安装consul
  docker pull consul   
  docker run -h node1  --name consul -d --restart=always    -p  8400     -p   8500:8500 progrium/consul -server -bootstrap-expect 1 -advertise 127.0.0.1


1. 本Demo基于[txlcn-最新发布](https://github.com/codingapi/tx-lcn)版本
2. 启动Demo前需先启动事务管理器TM（txlcn-demo-tm）。
3. 更多信息见官网 [https://www.txlcn.org](https://www.txlcn.org)   
4. [性能测试报告](https://txlcn.org/zh-cn/docs/test.html)
5.默认配置为eureka的注册与发现
6.运行txlcn-demo-tm后在运行springcloud中的eureka
7.运行txlcn-demo-spring-a/b/c
8.浏览器中输入http://127.0.0.1:12011/txlcn?value=tcc 即可看到测试结果
9.如果使用consul作为注册中心，则需要修改每一个模块的pom文件，引入consul的java包，打开相应的注释，然后把spring的euraka注释掉即可
