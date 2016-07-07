# YARN
***
## 安装OpenJDK 1.7
        apt-get install openjdk-7-jdk
        java -version //检查java版本验证安装成功
## OpenSSH
        apt-get install ssh 
        apt-get install rsync
## 创建hadoop组
        addgroup hadoop
## 创建用户hduser并添加到hadoop组中
        adduser --ingroup hadoop hduser
## 检查hduser是否可以以无密码的方式登录localhost
        ssh localhost	
## 如果需要输入密码，进行如下操作
        ssh-keygen -t dsa 
        cat ~/.ssh/id_dsa.pub >> ~/.ssh/authorized_keys
## 解压缩Hadoop
        gunzip hadoop-2.6.0.tar.gz
        tar -xvf hadoop-2.6.0.tar
## 假设解压缩后的路径是在/hadoop/下在解压后的文件中，找到并编辑Hadoop环境变量文件
        路径：./hadoop-2.6.0/etc/hadoop/hadoop-env.sh
        设置Java Home: export JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64 
        设置hadoop prefix：export HADOOP_PREFIX=/hadoop/hadoop-2.6.0

## 配置xml文件
        路径：/hadoop/hadoop-2.6.0/etc/hadoop路径下
        
        修改core-site.xml文件
        先备份：cp core-site.xml core-site.xml.bak
        vi core-site.xml
        添加如下：
        <configuration>
        <property>
        <name>fs.defaultFS</name>
        <value>hdfs://localhost:9000</value>
        </property>
        </configuration>

        修改hdfs-site.xml文件
        先备份：cp hdfs-site.xml hdfs-site.xml.bak
        vi hdfs-site.xml
        添加如下：
        <configuration>
        <property>
        <name>dfs.replication</name>
        <value>1</value>
        </property>
        </configuration>

        修改mapred-site.xml文件
        将模版文件换成xml文件：cp mapred-site.xml.template mapred-site.xml
        vi mapred-site.xml
        添加如下：
        <configuration>
        <property>
        <name>mapreduce.framework.name</name>
        <value>yarn</value>
        </property>
        </configuration>

        修改yarn-site.xml文件
        先备份：cp yarn-site.xml yarn-site.xml.bak
        vi yarn-site.xml
        添加如下：
        <configuration>
        <property>
        <name>yarn.nodemanager.aux-services</name>
        <value>mapreduce_shuffle</value>
        </property>
        </configuration>

## 启动资源管理器和节点管理器
        $sbin/start-yarn.sh





