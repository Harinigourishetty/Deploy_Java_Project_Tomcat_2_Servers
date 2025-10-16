# Deploying a Java based application in Tomcat and storing artifact in Nexus Repository.
## maven is in one server and tomcat is in one server and nexus is in another server.

I have a Java-based web application that I want to build using Maven, store the generated .war artifact in a Nexus repository, and then deploy it to a Tomcat server.

### Steps to Install Maven, Java, and Build a Java Application

## step-1:- Update System Packages

*     sudo apt update -y

*     sudo apt upgrade -y

## step-2 Install Java (JDK)

    sudo apt install openjdk-17-jdk -y

![preview](Images/1.png)

* Verify Java Installation :-
    
      java -version

![preview](Images/2.png)


## step-3 Install Apache Maven

### Step 3.1: Install Using APT

        
      sudo apt install maven -y

 ![preview](Images/3.png)

### Step 3.2: Verify Maven Installation

    mvn -version

![preview](Images/4.png)

## step-4 Copy the Code from GitHub (Clone Repository)

    git clone https://github.com/akracad/JavaWebCal.git

  ![preview](Images/5.png)  

* After cloning:

      cd project-name

## step-5 Verify the Project Files

* Check the contents:

      ls

You should see a pom.xml file — that means it’s a Maven project.

* Example output:

   pom.xml  src/  README.md

## step-6 validate a code

    mvn validate

![preview](Images/6.png)

## step-6 package a code

    mvn package

![preview](Images/7.png)

After packaging, Maven will create a build file (like .jar or .war) inside the target/ folder.

* Example:

  target/webapp-0.1.war

### Steps to Install Nexus Repository
## Download Nexus Repository

 Use the following command to download the latest version of Nexus Repository Manager:

wget https://download.sonatype.com/nexus/3/latest-unix.tar.gz
 You may receive a redirected URL, which should look something like this:

    wget https://cdn.download.sonatype.com/repository/downloads-prod-group/3/nexus-3.85.0-03-unix.tar.gz


Extract the Tarball

 Once the tarball is downloaded, extract it using the following command:

    tar -xvzf nexus-3.85.0-03-unix.tar.gz
 This will create a directory named nexus-3.85.0-03.

 ![preview](nexusimages/01.png)

 Move the Nexus Directory to a Desired Location

 Move the extracted Nexus directory to a more appropriate location, like /opt/nexus, to keep things organized.

    sudo mv nexus-3.85.0-03 /opt/nexus


Create a Symlink for Easy Access

 Create a symlink to easily access the Nexus installation from anywhere:

    sudo ln -s /opt/nexus/bin/nexus /usr/bin/nexus


### Start Nexus Repository

 To start the Nexus server, navigate to the bin directory and run:

    cd /opt/nexus/bin

    ./nexus start

 Check the Nexus status to ensure it’s running correctly:

      ./nexus status
 You should see a confirmation that Nexus is running.

 ### 3. Configuring Nexus Repository
Accessing Nexus Web Interface
Open Nexus in a Web Browser

 Open your web browser and navigate to:

 ### http:// ip address:8081

 For example, if you're running Nexus on an AWS instance, replace your-server-ip with the actual public IP of your server.


Login to Nexus


Default Username: admin


### Default Password: The password is stored in a file located at /opt/nexus/sonatype-work/nexus3/admin.password.


Retrieve the password using:

    cat /opt/nexus/sonatype-work/nexus3/admin.password


Change the Admin Password

 Upon first login, you will be prompted to change the default admin password for security purposes.

 After login, go to system status it will look like bell icon.

 -> After clicking it you can see the "Repository" option in the left side click on it.

 -> After clicking repository option you can see repositories on the dashboard click on it and you can create a repository.

 ![preview](nexusimages/02.png)

![preview](nexusimages/03.png)


-> copy the URL of the repository

![preview](nexusimages/04.png)

Go to build server open pom.xml there you can see Repository option remove old url and repo name edit it with new one.

![preview](nexusimages/05.png)

-> after editing with our details do mvn clean 

     mvn clean

     mvn validate


  ![preview](nexusimages/06.png)   

  ![preview](nexusimages/07.png)


  -> After packaging come out from javaweb calculator go to 

     cd /etc/maven

     vi setting.xml

there you can see 
 
 ![preview](nexusimages/08.png)

 edit this with your data

 ![preview](nexusimages/09.png)

 Next run a deploy command

    mvn deploy

 ![preview](nexusimages/10.png)

 -> go to nexus repo and click on the repository which you have created and copy the url from that

 ![preview](nexusimages/11.png)

 Copy that url and paste it in tomcat server 

     wget http://admin:admin@13.218.115.126:8081/repository/java-cal-app/com/web/cal/webapp/0.0.1/webapp-0.0.1.war


now you can see it in tomcat

![preview](nexusimages/12.png)



Same like this you have to do with version 2 AND 3

Go to webapps in that we can see index.jsp add a subraction code under the addtion code.

    cd ~/JavaWebCalculator/src/main/webapp

    sudo vi index.jsp

![preview](nexusimages/013.png)

### Then you have to do mvn clean, mvn package, mvn deploy.

-> go to nexus repo and click on the repository which you have created and copy the url from that

 ![preview](nexusimages/0013.png)

 Copy that url and paste it in tomcat server 

     wget http://admin:admin@34.228.62.123:8081/repository/java-cal-app/com/web/cal/webapp/0.0.3/webapp-0.0.3.pom.md5

![preview](nexusimages/13.png)



Go to webapps in that we can see index.jsp add a production code under the subration code.

    cd ~/JavaWebCalculator/src/main/webapp

    sudo vi index.jsp

![preview](nexusimages/014.png)

### Then you have to do mvn clean, mvn package, mvn deploy.

-> go to nexus repo and click on the repository which you have created and copy the url from that

 ![preview](nexusimages/0014.png)

 Copy that url and paste it in tomcat server 

     wget http://admin:admin@34.228.62.123:8081/repository/java-cal-app/com/web/cal/webapp/0.0.3/webapp-0.0.3.pom.md5

![preview](nexusimages/14.png)
