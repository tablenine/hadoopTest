### Hadoop 셋팅 

#### ssh key 생성

[참고](https://github.com/tablenine/ETC/blob/master/ssh%20key%20%EC%83%9D%EC%84%B1.md)

#### vi masters

``` bash
hadoop01
```

#### vi slaves

``` bash
hadoop01
hadoop02
hadoop03
hadoop04
```

#### vi core-site.xml

``` bash
    <property>
        <name>fs.default.name</name>
        <value>hdfs://hadoop01:9010</value>
    </property>
```
#### vi hdfs-site.xml (slave)

``` bash
	<property>
		<name>dfs.replication</name>
		<value>2</value>
	</property>
	<property>
		<name>dfs.permissions</name>
		<value>false</value>
	</property>
	<property>
		<name>dfs.datanode.data.dir</name>
		<value>/usr/local/hadoop/datanode</value>
	</property>
```
#### vi hdfs-site.xml (master)

``` bash
    <property>
        <name>dfs.replication</name>
        <value>2</value>
    </property>
    <property>
        <name>dfs.permissions</name>
        <value>false</value>
    </property>
    <property>
        <name>dfs.namenode.name.dir</name>
        <value>/home/deploy/hadoop-2.7.4/namenode</value>
    </property>
    <property>
        <name>dfs.datanode.data.dir</name>
        <value>/home/deploy/hadoop-2.7.4/datanode</value>
    </property>
    <property>
        <name>dfs.namenode.datanode.registration.ip-hostname-check</name>
        <value>false</value>
    </property>
```

#### vi mapred-site.xml

``` bash
	<property>
		<name>mapreduce.framework.name</name>
		<value>yarn</value>
	</property>
```
#### vi yarn-site.xml

``` bash
	<property>
		<name>yarn.nodemanager.aux-services</name>
		<value>mapreduce_shuffle</value>
	</property>
	<property>
		<name>yarn.nodemanager.auxservices.mapreduce.shuffle.class</name>
		<value>org.apache.hadoop.mapred.ShuffleHandler</value>
	</property>
```

#### 확인 

``` bash
/usr/local/hadoop/bin/hadoop namenode -format
/usr/local/hadoop/bin/hadoop datanode -format
/usr/local/hadoop/bin/hdfs namenode -format -clusterId CID-3ba94e43-9dd3-469c-9e90-ba7090e0898e
/usr/local/hadoop/bin/hdfs namenode -format -clusterId  CID-c5d8f1bf-1e44-4e1b-8bbe-ff3d5da024a1
sh /usr/local/hadoop/sbin/start-all.sh
sh /usr/local/hadoop/sbin/stop-all.sh
/usr/local/hadoop/bin/hadoop fs -df -h
```

