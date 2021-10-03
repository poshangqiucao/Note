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