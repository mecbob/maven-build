#

#   Tomcat installation on EC2 instance

## Prerequisit

### Install Java on an ec2 server. 

        sudo apt update

Add required dependencies for the jenkins package

        sudo apt install fontconfig openjdk-17-jre -y

    or

        sudo apt install fontconfig default-jre -y 

Verify Java Installation 

    java -version 



## Downlowd and Install Tomcat App on the EC2

Download Tomcat v9.0.111 

     sudo wget https://downloads.apache.org/tomcat/tomcat-9/v9.0.111/bin/apache-tomcat-9.0.111.tar.gz

Unzip the downloaded **.tar.gz ** zip file 

    tar -xvzf apache-tomcat-9.0.111.tar.gz

Move the extracted  binaries to desired Tomcat location

    sudo mv apache-tomcat-9.0.111 /opt/tomcat

Make the  Start / Stop scripts executable:

    chmod +x /opt/tomcat/bin/*.sh


Create link files for tomcat startup.sh and shutdown.sh

   sudo ln -s /opt/tomcat/bin/startup.sh /usr/local/bin/tomcatup

    sudo ln -s /opt/tomcat/bin/shutdown.sh /usr/local/bin/tomcatdown

    tomcatup


Access Tomcat Application from brower on default port 8080  **http://`<server-ip>`:8080**


**Note** (
Tomcat by default does not allow browser based login from sever other than that running the tomcat application. Changing the default parameter in context.xml file will resolve this. 

Find the **context.xml** file, and comment **() Value ClassName** field on files which are under webapp directory i.e `/opt/tomcat/webapps/manager/META-INF/context.xml` and  `/opt/tomcat/webapps/host-manager/META-INF/context.xml` 

Restart tomcat services to enable these changes

    sudo find / -name context.xml



In the tomcat home directory **/opt/tomcat/conf** , update users information in the **tomcat-users.xml**

    <role rolename="manager-gui"/>
	<role rolename="manager-script"/>
	<role rolename="manager-jmx"/>
	<role rolename="manager-status"/>
	<user username="admin" password="admin" roles="manager-gui, manager-script, manager-jmx, manager-status"/>
	<user username="deployer" password="deployer" roles="manager-script"/>
	<user username="tomcat" password="s3cret" roles="manager-gui"/>