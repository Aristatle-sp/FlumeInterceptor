#Flume Interceptor

Flume out of box agents does not(Not Sure) support sending messages to multiple kafka partitions.

So we need to implement the interceptor to add partition name as part of the Header Message.

Project : Flume-interceptor
File	   : HeaderInterceptor.java

Change the partition name and number of partition as below in HeaderInterceptor.java file

headerKeys.put("key","stream-"+String.valueOf(new Random().nextInt(5)));

Partition Name : stream-
Eg. stream-1
Eg. stream-2

Number of partition : 5

Create Jar::

Terminal

cd project root directory FlumeInterceptor-master
mvn clean
mvn install

place the jar file onto flume Lib directory

/apache-flume-1.6.0-bin/lib

Restart the Flume Agent:

Run command after navigating to the $APACHE_FLUME_HOME_DIRECTORY
bin/flume-ng agent --conf conf --conf-file conf/streaming.conf --name a1 -Dflume.root.logger=INFO,console

Now the Messages will be sent to all random partitions
