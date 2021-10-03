# SpringBoot部署文档

* 打包

  * mvn clean package
  * idea自带maven插件打包

* 使用jar包直接运行

  * 命令 java -jar xxx.jar

  * 注意事项

    * 阿里云服务器设置安全组配置打开对应服务端口

    * 服务器防火墙端口放开

      * 查看防火墙开放端口

        * firewall-cmd --list-ports

      * 放开端口

        * firewall-cmd --zone=public --add-port=8080/tcp --permanent 

          命令含义:
          –zone #作用域
          –add-port=8080/tcp #添加端口，格式为：端口/通讯协议
          –permanent #永久生效，没有此参数重启后失效　

      * 重启防火墙

        * firewall-cmd --reload
  
* 使用jenkins进行CI/CD

  * jenkins配置jdk,maven，配置远程部署机器的连接信息，安装maven,git，ssh相关插件

  * 如果是私有仓库则需要配置私钥允许jenkins拉取仓库

  * 新建maven构建项目

  * 构建后动作配置如下，也就是把构建包复制到远程机器目录，执行相关运行命令：

    * ![image-20211003173217728](.\img\image-20211003173217728.png)

    * ```bash
      cd /root/visitor
      rm -rf app.jar
      mv *.jar app.jar
      netstat -ntlp | grep 9091 | awk '{print $7}' | cut -d '/' -f 1 | xargs kill -s 9
      nohup java -jar app.jar >> /dev/null 2>&1 &
      ```

    * 