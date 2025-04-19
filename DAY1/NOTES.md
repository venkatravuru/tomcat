


Linux
Git and github
Shell scripting

Maven 

Tomcat by KK FUNDA
==================

NOTE: How to run jar/war/ear files?

jar: java -jar <filename>
war: tomcat required [application server]
ear: wildfly required [application server]


Tomcat server:[application server]
--------------


Def: Tomcat or apache tomcat is a opensource web container used to deploy and running the java based web applications, It was developed by Apache software foundation [ASF]


Types of application servers
----------------------------
1. Apache tomcat or tomcat  -----> we can deploy only war files not ear files.
2. Jboss/wildfly
    --> 1.x to 7.x [Jboss]
    --> 8.x to till date [wildfly]

3. Web sphere application server ---> IBM
4. WebLogic ---> Oracle
5. Glashfish .......


IQ] why you are going for tomcat app server?
ANS: Now a days most of the projects developed based on the micro service architecture.
  
    In java MS's developed with the help of springboot framework. For springboot default application server is tomcat.

IQ] what is the diff between tomcat and jboss?
   tomcat mainly used for web applicaions, Jboss used for web/enterprise applications.

How to download a tomcat server?
================================

step 1: go to google search apache tomcat download

url : https://tomcat.apache.org/download-90.cgi

stpe 2: 

launch an EC2 machine and connect

switch to root user, go to /opt/ dir

step 3:

yum install unzip tree wget -y

wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.104/bin/apache-tomcat-9.0.104.zip

step 4:
unzip apache-tomcat-9.0.104.zip

step 5: cd apache-tomcat-9.0.104.zip
step 6: tree ---> to see the dir structure.




Tomcat directory structure
==========================

1. bin

  startup.sh  ---> Linux/mac
  startup.bat ---> windows
 
  shutdown.sh
  shutdown.bat

  catalina.sh start/stop/restart
  catalina.bat start/stop/restart

 
2. conf
   
   server.xml
   tomcat-users.xml

3. lib

 It contains all jar files, It will helps while running an application.

4. logs

 NOTE: once we start the server below files will be created.

catalina.log
hostmager.log
manager.log
localhost.log


5. webapps *****

Here we are keeping our .war files.

 By default we have 5 web applications are there.

->ROOT
->manager
->host-manager
->examples
->docs

6. work

Once we deploy application, App related files will be stored here.

7. temp

All temp files are stored here.



Installation of tomcat
======================

prerequisites 
-------------
java 1.8 min required for tomcat 9.x version.

1 GB RAM is enough, because  we are running small web application.

step 1: launch one ec2 m/c for tomcat 

step 2: connect to that server

step 3: sudo su -

step 4: install java
   sudo yum install java-11-openjdk-devel -y
   javac --version

step 5: yum install wget unzip -y

step 6: cd /opt/
   
      wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.91/bin/apache-tomcat-9.0.104.zip
     
step 7: unzip apache-tomcat-9.0.104.zip

 



step 8: goto the bin directory.
     
       cd /opt/apache-tomcat-9.0.104/bin

step 9: chmod u+x *.sh


IQ] How to start/stop the tomcat server?

    step 1: go to bin directory 

    step 2: sh startup.sh    ----> to start
                or
            sh catalina.sh start ---> to start

          sh shutdown.sh  ----> to stop 
               or
          sh catalina.sh stop ----> to stop


NOTE: By default port number of tomcat : 8080


TCP port range: 0 to 65535




IQ] How to check tomcat is running or not?

    sudo yum install lsof
    lsof -i :8080


   ps -ef|grep -i "tomcat"







IQ] I want to start/stop tomcat server from anywhere instead of bin dir?


ln -s /opt/apache-tomcat-9.0.104/bin/startup.sh /usr/bin/startTomcat
ln -s /opt/apache-tomcat-9.0.104/bin/shutdown.sh /usr/bin/stopTomcat

Now you can go and run in any directory.


http://65.0.182.70:8080












IQ] How to access tomcat server from PC?

NOTE: default port number for tomcat server is 8080.

 http://65.2.129.199:8080  ---> directly you can't access without enable that port number in security group.

  select the server --> go to security --> scroll down --> click on security group ---->
  click on edit in-bound rules ---> click on add rule ---> select custom tcp ---> give port 8080 ----> select anywhere ipv4 ---> save the rules.

Then reload this url http://13.233.32.177:8080

click on server Status, Manager App, Host Manager ----> not able to access.


====================================================================


--> we can place our application into "Manager App"
                                       ===========

step 1: cd /opt/apache-tomcat-9.0.104/webapps

step 2: cd manager 

step 3: cd META-INF

step 4: ls ----> context.xml

step 5: vi context.xml
    
      :se nu
      comment 21st and 22nd lines.
     <!--
     -->
step 6: refresh the main page ----> It will ask the credentials.

step 7: cd /opt/apache-tomcat-9.0.104/conf/ 

step 8: vi tomcat-users.xml ---> goto end of the file and add users.

  <user username="kk" password="kkfunda123" roles="manager-gui,admin-gui"/>
  <user username="mahesh" password="mahesh" roles="manager-gui,admin-gui"/>



if you want to login Host-manager do the same process?
                     ============
step 1: cd /opt/apache-tomcat-9.0.104/webapps

step 2: cd host-manager 

step 3: cd META-INF

step 4: ls ----> context.xml

step 6: vi context.xml

step 7: vi context.xml

      comment 21st and 22nd lines.
     <!--
     -->
step 8: refresh the main page ----> It will ask the credentials, give the credentials.

step 9: go and check the logs directory logs are created or not

       cd /opt/apache-tomcat-9.0.104/logs


Assignment 
==========

create a multiple users and try to access.


=======================================================================



Maven  --> .war  ----> deploy into app server(tomcat)







IQ] How to change port number and why we need to change the port number?

scenario: I need to install tomcat & Jenkins in the same server.

ANS: tomcat port number is 8080 and Jenkins port number also 8080 --> Then we are getting port conflict . [java.net.BindException we will get] , so that we are changing the port numbers.


step 1: goto conf directory.

    cd /opt/apache-tomcat-9.0.91/conf

step 2: open server.xml
   
    goto line number 69 and change the port.

step 3: stop the tomcat server and start the tomcat server.

step 4: now try to access with different port number.

NOTE: please make sure to enable the port in Security groups.
