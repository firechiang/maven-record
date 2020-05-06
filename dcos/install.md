#### 一、下载安装，[官方下载以及安装文档](https://help.sonatype.com/repomanager3/download)（注意：下载可能需要翻墙，可到我的百度云盘下载）
```bash
$ wget -P /home/maven-nexus https://sonatype-download.global.ssl.fastly.net/repository/downloads-prod-group/3/nexus-3.23.0-03-unix.tar.gz
$ tar xvzf nexus-3.23.0-03-unix.tar.gz 
$ cd /home/maven-nexus/nexus-3.23.0-03/bin
```

#### 二、修改 Nexus 服配置相关参数
```bash
$ vi /home/maven-nexus/nexus-3.23.0-03/etc/nexus-default.properties
```

#### 三、修改 Nexus 服务 JVM 相关参数
```bash
$ vi /home/maven-nexus/nexus-3.23.0-03/bin/nexus.vmoptions
```

#### 四、创建[vi /etc/init.d/nexus3]启动脚本（注意：修改nexus的安装目录）
```bash
#!/bin/sh
# nexus服务必须在2，3，4，5运行级下被启动或关闭，启动的优先级是80，关闭的优先级是93
#chkconfig: 2345 80 93
#description: this script to start and stop nexus server
#version: 1.0
#setting variable

# nexus安装目录
NEXUS_HOME=/home/maven-nexus/nexus-3.23.0-03

case "$1" in
    start)
        $NEXUS_HOME/bin/nexus start
        ;;
    stop)
        $NEXUS_HOME/bin/nexus stop
        ;;
    *)
        echo "Please use start or stop as first argument"
        ;;
esac
```

#### 五、给nexus3脚本赋予权限
```bash
$ chmod +x /etc/init.d/nexus3
```

#### 六、启动Nexus（注意：启动时有点慢，因为它要先启动karaf服务）
```bash
$ service nexus3 start                                       # 启动nexus3
$ service nexus3 stop                                        # 停止nexus3
$ sudo chkconfig nexus3 on                                   # 设置nexus3开机启动（建议开启）
$ sudo chkconfig nexus3 off                                  # 关闭nexus3开机启动
```
#### 七、查看Nexus admin用户初始密码和服务日志
```bash
$ more /home/maven-nexus/sonatype-work/nexus3/admin.password # 查看admin用户初始密码（注意：初始密码用完以后文件会自动删除）
$ more /home/maven-nexus/sonatype-work/nexus3/log/nexus.log  # 查看nexus日志
```

