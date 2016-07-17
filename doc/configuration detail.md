1. without password login node
-------------------------------------
####master node:
    ssh-keygen –t rsa –p
    cat ~/id_rsa.pub  ~/.ssh/authorized_keys
####slave node:
    mkdir .ssh
####copy to all slaves:
    scp /home/hadoop/.ssh/ authorized_keys  hadoop@slave01.node:~/

2. install java environment
-----------------------------------------------
#####Download and unzip jdk-8u91-linux-x64.tar.gz and modify environment variable  

    sudo mkdir /usr/java/jdk1.8  
    sudo mv jdk1.8.0_91/ /usr/java/jdk1.8
    sudo nano /etc/profile
    export JAVA_HOME=/usr/java/jdk1.8
    export CLASSPATH=.:$JAVA_HOME/lib:$JAVA_HOME/jre/lib:$CLASSPATH
    export PATH=$JAVA_HOME/bin:$JAVA_HOME/jre/bin:$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin
    export HADOOP_HOME=/usr/hadoop-2.6.4
    source /etc/profile
    java  –version 
    
3. install Hadoop
-------------------------------------------------------
####    Download and unzip Hadoop-2.6.4.tar.gz
    sudo cp hadoop-2.6.4  /usr
####    Modify hostname, eg.change hostname to slave01
    sudo nano /etc/hostname
####    Modify hosts enter all members ip + hostname,eg. 192.168.0.101 slave01  
    sudo nano /etc/hosts
####    Modify 7 files in hadoop/etc/hadoop
######core-site.xml
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://master:9000</value>
    </property>
    <property>
        <name>io.file.buffer.size</name>
        <value>131072</value>
    </property>
    <property>
        <name>hadoop.tmp.dir</name>
        <value>file:/usr/ hadoop-2.6.4/tmp</value>
        <description>Abase for other temporary directories.</description>
    </property>
    <property>
        <name>hadoop.proxyuser.hduser.hosts</name>
        <value>*</value>
    </property>
    <property>
        <name>hadoop.proxyuser.hduser.groups</name>
        <value>*</value>
    </property>
###### hdfs-site.xml
    <configuration>
        <property>
            <name>dfs.namenode.secondary.http-address</name>
            <value>master:9001</value>
        </property>
        <property>
            <name>dfs.namenode.name.dir</name>
            <value>file:/usr/hadoop-2.6.4/dfs/name</value>
        </property>
        <property>
            <name>dfs.datanode.data.dir</name>
            <value>file:/usr/ hadoop-2.6.4/dfs/data</value>
        </property>
        <property>
            <name>dfs.replication</name>
            <value>3</value>
        </property>
        <property>
            <name>dfs.webhdfs.enabled</name>
            <value>true</value>
        </property>
    </configuration>
######mapred-site.xml
<configuration>
    <property>
        <name>mapreduce.framework.name</name>
        <value>yarn</value>
    </property>
    <property>
        <name>mapreduce.jobhistory.address</name>
        <value>master:10020</value>
    </property>
    <property>
        <name>mapreduce.jobhistory.webapp.address</name>
        <value>master:19888</value>
    </property>

</configuration>

yarn-site.xml
<configuration>
    <property>
        <name>yarn.nodemanager.aux-services</name>
        <value>mapreduce_shuffle</value>
    </property>
    <property>
        <name>yarn.nodemanager.aux-services.mapreduce.shuffle.class</name>
        <value>org.apache.hadoop.mapred.ShuffleHandler</value>
    </property>
    <property>
        <name>yarn.resourcemanager.address</name>
        <value>master:8032</value>
    </property>
    <property>
        <name>yarn.resourcemanager.scheduler.address</name>
        <value>master:8030</value>
    </property>
    <property>
        <name>yarn.resourcemanager.resource-tracker.address</name>
        <value>master:8031</value>
    </property>
    <property>
        <name>yarn.resourcemanager.admin.address</name>
        <value>master:8033</value>
    </property>
    <property>
        <name>yarn.resourcemanager.webapp.address</name>
        <value>master:8088</value>
    </property>

</configuration>
