DataNode cannot run:
  1.Stop dfs
  2.rm –r   /usr/hadoop/dfs/data  
  3.Then start dfs again.

DataNode cannot show in webpage:
  1.Use jps check slave’s datanode status
  2.if the datanode is working, then check the network

Permission denied
  1.add hadoop user to root user group
    sudo nano /etc/sudoers
    add "hadoop  ALL=(ALL:ALL) ALL"
  2.sudo chmod 777 /usr/hadoop -R
  
About HIVE version
  recommand to install hive-1.2.1 
  because in our experience there is a problem of starting hiveserver2 
