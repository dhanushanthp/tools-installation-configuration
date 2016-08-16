# Directory creation for custom applications
```sh
sudo mkdir -p /usr/local/app
cd /usr/local
sudo chown $USER app
```
# Ipython environment setup
### Anaconda package installation for python env
```sh
wget http://repo.continuum.io/archive/Anaconda2-4.1.1-Linux-x86_64.sh
bash Anaconda2-4.1.1-MacOSX-x86_64.sh
source ~/.bashrc
conda -version
```
### Anaconda environment creation
```sh
conda create --name dev_env python
source activate dev_env
source deactivate

# Clone env
conda create --name flowers --clone snowflakes

# List all env
conda info --envs

# Remove env
conda remove --name flowers --all
```
### Jupyter installation
```sh
conda install jupyter
```
### Certificate creation
```sh
openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout spark.pem -out spark.pem
```
### password generation with SHA1
```sh
from IPython.lib import passwd
password = passwd("dhanu@123")
password
```
### Ipython profile creation
```sh
jupyter notebook --generate-config
nano /home/ubuntu/.jupyter/jupyter_notebook_config.py
```
### Ipython profile configuration
```sh
c.IPKernelApp.pylab = 'inline'
c.NotebookApp.certfile = u'/home/ubuntu/spark.pem'
c.NotebookApp.ip = 'ec2-52-221-249-166.ap-southeast-1.compute.amazonaws.com'
c.NotebookApp.open_browser = False
c.NotebookApp.password = u'sha1:f46c610c6c16:59d37b5b93be74c606f3fac3a0f9f2793d435dc3'
c.NotebookApp.port = 8080
c.NotebookApp.notebook_dir = u'/home/ubuntu/projects'
```
# Spark Installations
```sh
wget http://download.nus.edu.sg/mirror/apache/spark/spark-1.6.1/spark-1.6.1-bin-hadoop2.6.tgz   
tar -xzf spark-1.6.1-bin-hadoop2.6.tgz
mv spark-1.6.1-bin-hadoop2.6 spark
mv spark /usr/local/app
```
# Scala installation
```sh
wget http://www.scala-lang.org/files/archive/scala-2.10.4.tgz 
tar -xzf scala-2.10.4.tgz
sudo mv scala-2.10.4 scala
mv scala /usr/local/app
```
# Hadoop Installation
```sh
wget http://download.nus.edu.sg/mirror/apache/hadoop/common/hadoop-2.7.2/hadoop-2.7.2.tar.gz
tar -zxvf hadoop-2.7.2.tar.gz
mv hadoop-2.7.2 hadoop
mv hadoop /usr/local/app
```
## Hadoop Configuration
```sh
su -user ↵
ssh-keygen -t rsa -P "" ↵
cat $HOME/.ssh/id_rsa.pub >> $HOME/.ssh/authorized_keys ↵
ssh localhost ↵
```
### Edit $HADOOP_HOME/etc/hadoop/core-site.xml 
```sh
<configuration>
   <property>
      <name>fs.default.name</name>
      <value>hdfs://localhost:9000</value> 
   </property>
</configuration>
```

### Edit $HADOOP_HOME/etc/hadoop/hdfs-site.xml
Note: The path (```file:///home/hadoop/hadoopinfra/hdfs/namenode```) need to be exist.
```sh
<configuration>
   <property>
      <name>dfs.replication</name>
      <value>1</value>
   </property>
    
   <property>
      <name>dfs.name.dir</name>
      <value>file:///home/hadoop/hadoopinfra/hdfs/namenode</value>
   </property>
    
   <property>
      <name>dfs.data.dir</name> 
      <value>file:///home/hadoop/hadoopinfra/hdfs/datanode</value> 
   </property>
</configuration>
```

# Environment Variables Setup

``` nano ~/.bashrc```
```sh
# spark
export JAVA_HOME=/usr/lib/jvm/java-7-oracle/
export SCALA="/usr/local/app/scala"
export SPARK="/usr/local/app/spark"
export CONDA="/usr/local/app/anaconda"

# ipython
export PYSPARK_DRIVER_PYTHON=jupyter 
export PYSPARK_DRIVER_PYTHON_OPTS="notebook"

# Hadoop
export HADOOP_HOME=/usr/local/hadoop
export HADOOP_OPTS="$HADOOP_OPTS -Djava.library.path=$HADOOP_HOME/lib/native"
export HADOOP_MAPRED_HOME=$HADOOP_HOME 
export HADOOP_COMMON_HOME=$HADOOP_HOME 
export HADOOP_HDFS_HOME=$HADOOP_HOME 
export YARN_HOME=$HADOOP_HOME 
export HADOOP_INSTALL=$HADOOP_HOME
export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native

export PATH=$PATH:$SCALA/bin:$SPARK/bin:$HADOOP_HOME/bin:$HADOOP_HOME/sbin:$CONDA/bin
```

## Run DFS from hadoop
```sh
# Prepare the namenode for HDFS file format
hdfs namenode -format 
start-dfs.sh
```
