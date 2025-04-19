IQ] How to change port number and why we need to change the port number?

scenario: I need to install tomcat & Jenkins in the same server.

ANS: tomcat port number is 8080 and Jenkins port number also 8080 --> Then we are getting port conflict . [java.net.BindException we will get] , so that we are changing the port numbers.


step 1: goto conf directory.

    cd /opt/apache-tomcat-9.0.104/conf

step 2: open server.xml
   
    goto line number 71 and change the port.

step 3: stop the tomcat server and start the tomcat server.

step 4: now try to access with different port number.

http://<IP>:<NEW-PORT-NO>


NOTE: please make sure to enable the port in Security groups.






=================================================================



Now i want to deploy application into tomcat server
===================================================

step 1:
-------
copy war file into your local[Downloads]
----------------------------------------

cp target/maven-web-application.war /tmp/

scp -i ~/Downloads/b4devopshyd.pem ec2-user@18.61.75.128:/tmp/maven-web-application.war  /c/Users/gpras/Downloads/maven-web-application.war

step 2: Access that web application from browser.
------

http://13.233.32.177:9090/maven-web-application



web servers                   vs					 app servers
---------------------------------------------------------------------------

1. Handle the static requests                   1. Business logic , dynamic content
2. Apache Httpd server,ngnix                    2.  tomcat, windlfy,
3. Load balancing 				                3.  Businees logic





Apache httpd server [web server]
==================================
stpe 1: check where that service is running or not

user name:apache  

service httpd.service status


step 2: yum install httpd -y
step 3: start the server
    service httpd start

NOTE: default port : 80

http://65.0.182.70

step 4: make to sure to enable inbould rules for port 80


step 5:  


what is the default path? /var/www/html 


/etc/httpd/conf
