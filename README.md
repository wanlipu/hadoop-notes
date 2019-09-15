# Hadoop Notes

## CSE6250 LAB
Please the instructions in the [lab section](http://www.sunlab.org/teaching/cse6250/fall2019/env/) to install docker and download required dock image. 

## Start docker container and all required services
check existing containers info
```
$ docker ps -a
```
To start a container again
```
$ docker start <CONTAINER ID or NAME>
```
Then attach it by
```
$ docker attach <CONTAINER ID or NAME>
```
Every time you restart your container, you are supposed to start all those services again before any HDFS related operations.\
### Start all necessary services
```
# /scripts/start-services.sh
```
Verify Hadoop
```
$ hadoop version
```


## HDFS Operations
First, you will need to switch to the hdfs user via
```
# sudo su - hdfs
```
Then, you can create a directory and change ownership of the newly created folder
```
> hdfs dfs -mkdir -p /user/<username> # username is root
> hdfs dfs -chown <username> /user/<username> # username is root
> exit
```
Similar to creating local directory via linux command mkdir, creating a folder named input in HDFS use
```
> hdfs dfs -mkdir input
```
or
```
> hdfs dfs -mkdir -p /input/events
> hdfs dfs -mkdir -p /input/mortality
```
and
```
> hdfs dfs -chown -R root /input
```
to list hdfs files
```
> hdfs dfs -ls input
> hdfs dfs -ls input/events
```


Suppose you followed previous instructions and created an directory named input, you can then copy data from local file system to HDFS using -put. For example,
```
> cd /bigdata-bootcamp/data
> hdfs dfs -put case.csv input
> hdfs dfs -put control.csv input
```
```
> hdfs dfs -put /mnt/host/Users/{USERNAME}/path/to/file /input/events
```
```
> hdfs dfs -put /mnt/host/home/wanli/cse6250/bigdata4health/homework2/data/events.csv /input/events
> hdfs dfs -put /mnt/host/home/wanli/cse6250/bigdata4health/homework2/data/mortality.csv /input/mortality
```
to remove files from hdfs
```
> hdfs dfs -rm -R /path/to/HDFS/file
```


```
-bash-4.2$ hdfs dfs -mkdir /hw2
-bash-4.2$ hdfs dfs -put /mnt/host/home/wanli/cse6250/bigdata4health/homework2/code/pig/training/ /hw2
-bash-4.2$ hdfs dfs -ls /hw2
```


## Run Hive scripts
```
hive -f sample.hql
```
## Run Pig scripts
[Pig tutorials](https://www.tutorialspoint.com/apache_pig/index.htm)
```
pig -x local sample.pig
```
