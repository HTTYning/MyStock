# Jenkins

## 环境搭建

**Linux**

1. 下载JDK
2. 下载Jenkins
   1. https://www.jenkins.io/zh/download/
   2. 下载选项: Generic Java package(.war)
   3. 在终端运行java- jar jenkins.war 或者添加到tomcat/webapps下，启动tomcat
   4. 启动并指定端口号: java -jar jenkins.war --httpPort=8081 建议修改，原端口8080可能会与其他端口冲突