
#sudo don't work
apt-get update

#looks similart to unix commands with "hadoop dfs" prefix
hadoop dfs -mkdir /foodir
hadoop dfs -cat /foodir/myfile.txt
hadoop dfs -rm /foodir/myfile.txt

#HDRS admin
hadoop dfsadmin -report
hadoop dfsadmin -decommison [datanodename]

#web interface
http://host:port/dfshealth.jsp


**Map Reduce**
#like unix pipeline
# Input | Map | Shuffle & Sort | Reduce | Output
cat input | grep | sort | uniq -c | cat> output

**running hadoop_base_unsecure**
https://github.com/bigdatafoundation/docker-hadoop
#start name node
docker run -d --name hdfs-namenode -h hdfs-namenode -p 50070:50070 amaskey/hadoop_base_unsecure hdfs namenode && docker logs -f hdfs-namenode
#starting data node
docker run -d --name hdfs-datanode1 -h hdfs-datanode1 -p 50075:50075 --link=hdfs-namenode:hdfs-namenode amaskey/hadoop_base_unsecure hdfs datanode && docker logs -f hdfs-datanode1
#secondary name node
docker run -d --name hdfs-secondarynamenode -h hdfs-secondarynamenode -p 50090:50090 --link=hdfs-namenode:hdfs-namenode amaskey/hadoop_base_unsecure hdfs secondarynamenode && docker logs -f hdfs-secondarynamenode
#starting yarn
docker run -d --name yarn -h yarn -p 8088:8088      -p 8042:8042 --link=hdfs-namenode:hdfs-namenode --link=hdfs-datanode1:hdfs-datanode1 -v $HOME/data/hadoop/hdfs:/data amaskey/hadoop_base_unsecure start-yarn.sh && docker logs -f yarn
#put some data in 
docker run --rm --link=hdfs-namenode:hdfs-namenode --link=hdfs-datanode1:hdfs-datanode1 amaskey/hadoop_base_unsecure hadoop fs -put /usr/local/hadoop/README.txt /README.txt
#start word count
docker run --rm --link yarn:yarn --link=hdfs-namenode:hdfs-namenode amaskey/hadoop_base_unsecure hadoop jar /usr/local/hadoop/share/hadoop/mapreduce/hadoop-mapreduce-examples-2.8.1.jar wordcount  /README.txt /README.result
#check result of word count
docker run --rm --link=hdfs-namenode:hdfs-namenode --link=hdfs-datanode1:hdfs-datanode1 amaskey/hadoop_base_unsecure hadoop fs -cat /README.result/\*
#access web interface
http://10.0.18.109:50070	#NameNode
http://10.0.18.109:50075	#Datanode
http://10.0.18.109:50090	#Secondary NodeName
http://10.0.18.109:8088		#Resource Manager
http://10.0.18.109:8042		#Yarn node manager
