Hadoop MapReduce Twitter Dataset follower count
code for Homework1: CS6240
Fall 2020

Current version Code author:
---------------------
Aamod Khatiwada

Original Code author:
-----------
Joe Sackett

Installation
------------
These components are installed:
- JDK 1.8
- Hadoop 3.2.1
- Maven
- AWS CLI (for EMR execution)

Environment
-----------
1) Example ~/.bashrc:

export HADOOP_HOME=/home/forhadoop/hadoop-3.2.1
export HADOOP_INSTALL=$HADOOP_HOME
export HADOOP_MAPRED_HOME=$HADOOP_HOME
export HADOOP_COMMON_HOME=$HADOOP_HOME
export HADOOP_HDFS_HOME=$HADOOP_HOME
export YARN_HOME=$HADOOP_HOME
export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native
export PATH=$PATH:$HADOOP_HOME/sbin:$HADOOP_HOME/bin
export HADOOP_OPTS="-Djava.library.path=$HADOOP_HOME/lib/native"
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64


2) Explicitly set JAVA_HOME and HADOOP_CONF_DIR in $HADOOP_HOME/etc/hadoop/hadoop-env.sh:

export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
export HADOOP_CONF_DIR=${HADOOP_HOME}/etc/hadoop

Execution
---------
All of the build & execution commands are organized in the Makefile.
1) Unzip project file.
2) Open command prompt.
3) Navigate to directory where project files unzipped.
4) Edit the Makefile to customize the environment at the top.
	Sufficient for standalone: hadoop.root, jar.name, local.input
	Other defaults acceptable for running standalone.
5) Standalone Hadoop:
	make switch-standalone		-- set standalone Hadoop environment (execute once)
	make local
6) Pseudo-Distributed Hadoop: (https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-common/SingleCluster.html#Pseudo-Distributed_Operation)
	make switch-pseudo			-- set pseudo-clustered Hadoop environment (execute once)
	make pseudo					-- first execution
	make pseudoq				-- later executions since namenode and datanode already running 
7) AWS EMR Hadoop: (you must configure the emr.* config parameters at top of Makefile)
	make upload-input-aws		-- only before first execution
	make aws					-- check for successful execution with web interface (aws.amazon.com)
	download-output-aws			-- after successful execution & termination
