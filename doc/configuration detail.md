1.without password login node
-------------------------------------
####master node:
    ssh-keygen –t rsa –p
    cat ~/id_rsa.pub  ~/.ssh/authorized_keys
####slave node:
    mkdir .ssh
####copy to all slaves:
    scp /home/hadoop/.ssh/ authorized_keys  hadoop@slave01.node:~/




2.install java environment

*download linux x64 jdk-8u91-linux-x64.tar.gz and export modify environment variable  
sudo mkdir /usr/java/jdk1.8  
sudo mv jdk1.8.0_91/ /usr/java/jdk1.8
sudo nano /etc/profile
export JAVA_HOME=/usr/java/jdk1.8
export CLASSPATH=.:$JAVA_HOME/lib:$JAVA_HOME/jre/lib:$CLASSPATH
export PATH=$JAVA_HOME/bin:$JAVA_HOME/jre/bin:$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin
export HADOOP_HOME=/usr/hadoop-2.6.4
source /etc/profile
java  –version 
