# Hadoop Single Node

virtualbox version  >>>  4.3.30   ubuntu version  >>>  14.04.3
  
1.$sudo apt-get update  #apt get應用程式取得 update全部linux有更新的都抓
2.$sudo apt-get upgrade  
3.$sudo apt-get install vim  #vim是一個文字編輯器
4.$sudo apt-get install openjdk-7-jdk (http:#openjdk.java.net/install)  
5.$sudo apt-get install openssh-server  #要更新才會有
6.$ssh-keygen -t rsa -P "" (and just press enter)  #key generate""空字串代表不需要密碼
7.$cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys  #>>是寫入，把空字串這個密碼傳進某個文件檔,cat把資料全部顯示
8.$ssh localhost (type "yes")  login without key  
9.$exit  
13.$wget http:#ftp.twaren.net/Unix/Web/apache/hadoop/common/hadoop-2.7.3/hadoop-2.7.3.tar.gz   #wget是外部package
   (Other version : http:#ftp.twaren.net/Unix/Web/apache/hadoop/common/)  
14.$tar xfz hadoop-2.7.3.tar.gz  #tar是解壓縮
15.$sudo mv hadoop-2.7.3 hadoop  
16.$sudo vim ~/.bashrc  
```
#HADOOP VARIABLES START
export JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64
export HADOOP_INSTALL=/home/XXXXXXXX/hadoop #XXXX地方是使用者的電腦名稱
export PATH=$PATH:$HADOOP_INSTALL/bin
export PATH=$PATH:$HADOOP_INSTALL/sbin
export HADOOP_MAPRED_HOME=$HADOOP_INSTALL
export HADOOP_COMMON_HOME=$HADOOP_INSTALL
export HADOOP_HDFS_HOME=$HADOOP_INSTALL
export YARN_HOME=$HADOOP_INSTALL
export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_INSTALL/lib/native
export HADOOP_OPTS="-Djava.library.path=$HADOOP_INSTALL/lib"
#HADOOP VARIABLES END
```  
17.$source ~/.bashrc  #更改為bashrc設定檔都要跑這行指令才會reload new configuration
18.$cd hadoop/etc/hadoop  
19.$sudo vim hadoop-env.sh  
```  
#export JAVA_HOME={JAVA_HOME}
export JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64 
```  
20.$sudo vim core-site.xml  
```
<configuration>
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs:#localhost:9000</value>
    </property>
</configuration>
```
21.$sudo vim hdfs-site.xml  
```
<configuration>
    <property>
        <name>dfs.replication</name>
        <value>1</value>
    </property>
</configuration>
```  
22.$cp mapred-site.xml.template mapred-site.xml  
23.$sudo vim mapred-site.xml  
```
<configuration>
    <property>
        <name>mapreduce.framwork.name</name>
        <value>yarn</value>
    </property>
</configuration>
```
24.$sudo vim yarn-site.xml  
```
<configuration>
    <property>
        <name>yarn.nodmanager.aux-services</name>
        <value>mapreduce_shuffle</value>
    </property>
</configuration>
```  
25.$cd
26.$hadoop namenode -format  #namenode = master node
27.$start-dfs.sh (type “yes”)  #dfs: distributed file system
28.$start-yarn.sh   #yarn: cluster manager
29.$jps  #list out services
 

If it returns ResourceManager、Jps、DataNode、SecondaryNameNode、NodeManager and NameNode, then you are done.
30.$stop-dfs.sh  
31.$stop-yarn.sh 
