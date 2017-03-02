[![GitHub issues](https://img.shields.io/github/issues/PacktPublishing/DevOps-for-Web-Development.svg)](https://github.com/PacktPublishing/DevOps-for-Web-Development/issues)   [![GitHub forks](https://img.shields.io/github/forks/PacktPublishing/DevOps-for-Web-Development.svg)](https://github.com/PacktPublishing/DevOps-for-Web-Development/network)   [![GitHub stars](https://img.shields.io/github/stars/PacktPublishing/DevOps-for-Web-Development.svg)](https://github.com/PacktPublishing/DevOps-for-Web-Development/stargazers)   [![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/PacktPublishing/DevOps-for-Web-Development/master/LICENSE)

# DevOps for Web Development
This is the code repository for [DevOps for Web Development](https://www.packtpub.com/networking-and-servers/devops-web-development?utm_source=github&utm_medium=repository&utm_content=9781786465702), published by Packt. It contains all the supporting project files necessary to work through the book from start to finish.

## Instructions and Navigation

All of the code is organized into folders. Each folder starts with a number followed by the application name. For example, `Chapter02`. 

Code Snippet:
```
 <properties>
        <jpa.database>MYSQL</jpa.database>
        <jdbc.driverClassName>com.mysql.jdbc.Driver</jdbc.driverClassName>
        <jdbc.url>jdbc:mysql://localhost:3306/petclinic?useUnicode=true</jdbc.url>
        <jdbc.username>root</jdbc.username>
        <jdbc.password>petclinic</jdbc.password>
    </properties>
```
### Chapter 1:
You can find all the necessary code **[here](https://github.com/spring-projects/spring-petclinic)** for the chapter 1.

### Chapter 2:

```
java -jar jenkins.war --httpPort=9999
java -jar jenkins.war --httpsPort=8888
java -jar slave.jar -jnlpUrl http://192.168.1.34:8080/computer/TestServer/slave-agent.jnlp -secret 65464e02c58c85b192883f7848ad2758408220bed2f3af715c01c9b01cb72f9b
```

**Sonar.properties**
*Required metadata *
```
sonar.projectKey=java-sonar-runner-simple 
sonar.projectName=Simple Java project analyzed with the SonarQube Runner 
sonar.projectVersion=1.0
```
**Comma-separated paths to directories with sources (required)**
`onar.sources=src`

**Language**
`sonar.language=java`
**Encoding of the source files **
`sonar.sourceEncoding=UTF-8`

### Chapter 3:
```
echo 'Hello from Pipeline Demo'
stage 'Compile'
build 'PetClinic-Compile'
stage 'Test'
build 'PetClinic-Test'
```
---------------

```
echo 'Hello from Pipeline Demo'
stage 'Compile'
node {
  git url: 'https://github.com/mitesh51/spring-petclinic.git'
  def mvnHome = tool 'Maven3.3.1'
  sh "${mvnHome}/bin/mvn -B compile"
}
stage 'Test'
node('WindowsNode') {
  git url: 'https://github.com/mitesh51/spring-petclinic.git'
  def mvnHome = tool 'WindowsMaven'
  bat "${mvnHome}\\bin\\mvn -B verify"
  step([$class: 'ArtifactArchiver', artifacts: '**/target/*.war', fingerprint: true])  
  step([$class: 'JUnitResultArchiver', testResults: '**/target/surefire-reports/TEST-*.xml'])
}
```
----------------
```
Create a user with name admin and assign password and roles as below. 
<role rolename="manager-gui"/>
<role rolename="manager-script"/>
<user username="admin" password="cloud@123" roles="manager-script" />
Now, we need to add Tomcat's admin user that we created in the Maven setting file.
<servers>
<server>
  <id>tomcat-development-server</id>
  <username>admin</username>
  <password>password</password>
</server>
</servers>
```
-----------------

Find *Tomcat* Plugin block in `Pom.xml` and add following details. Make sure that **Server Name** is same that we provided in `settings.xml` of Maven as **Id**:
```
<plugin>
                <groupId>org.apache.tomcat.maven</groupId>
                <artifactId>tomcat7-maven-plugin</artifactId>
                <version>2.2</version>
                <configuration>
                    <server>tomcat-development-server</server>
			<url>http://192.168.1.35:9999/manager/text</url>
			<warFile>target\petclinic.war</warFile>
			<path>/petclinic</path>
                </configuration>
 </plugin>
```

### Chapter 4:
```
rpm -ivh chef-12.9.41-1.el6.x86_64.rpm 
knife bootstrap 192.168.1.37 -x root -P cloud@123 -N tomcatserver
knife node run_list add tomcatserver"role[vtomcat]"
```

### Chapter 5:
`docker run -p 8180:8080 -d --name devopstomcat1devopstomcatnew`

### Chapter 6:
```
knife ec2 server create -I ami-1ecae776 -f t2.micro -N DevOpsVMonAWS --aws-access-key-id '< Your Access Key ID >' --aws-secret-access-key '< Your Secret Access Key >' -S book --identity-file book.pem --ssh-user ec2-user -r role[v-tomcat]
```
--------------
```
knife azure server create --azure-dns-name 'distechnodemo' --azure-vm-name 'dtserver02' --azure-vm-size 'Small' -N DevOpsVMonAzure2 --azure-storage-account 'classicstorage9883' --bootstrap-protocol 'cloud-api' --azure-source-image '5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-67-20160310' --azure-service-location 'Central US' --ssh-user 'dtechno' --ssh-password 'cloud@321' -r role[v-tomcat] --ssh-port 22
```

### Chapter 7:
***FROM tomcat:8.0***

**MAINTAINER** ``` Mitesh<YourEmailID@domain.com>```

**COPY**  ```tomcat-users.xml /usr/local/tomcat/conf/tomcat-users.xml```

### Chapter 8:
`java -jar newrelic.jar install`

### Chapter 9:

```
ssh -t -t root@192.168.1.36 "ifconfig; rvm use 2.1.0; knife ec2 server create -I ami-1ecae776 -f t2.micro -N DevOpsVMonAWS1 --aws-access-key-id '<YOUR ACCESS KEY ID>' --aws-secret-access-key '<YOUR SECRET ACCESS KEY>' -S book --identity-file book.pem --ssh-user ec2-user -r role[v-tomcat]"
```

-----------
```
ssh -t -t root@192.168.1.36 "ifconfig; rvm use 2.1.0; knife ec2 server create -I ami-1ecae776 -f t2.micro -N DevOpsVMonAWS1 --aws-access-key-id '<YOUR ACCESS KEY ID>' --aws-secret-access-key '<YOUR SECRET ACCESS KEY>' -S book --identity-file book.pem --ssh-user ec2-user -r role[v-tomcat]"
```
-----------
```
java -jar slave.jar -jnlpUrl http://192.168.1.35:8080/computer/TestServer/slave-agent.jnlp -secret 65464e02c58c85b192883f7848ad2758408220bed2f3af715c01c9b01cb72f9b
```
-----------
```
ssh  -i /home/mitesh/book.pem -o StrictHostKeyChecking=no -t -t ec2-user@ec2-52-90-116-36.compute-1.amazonaws.com "sudo usermod -a -G tomcat ec2-user; sudo chmod -R g+w /var/lib/tomcat6/webapps; sudo service tomcat6 stop;" 
scp  -i /home/mitesh/book.pem /home/mitesh/target/*.war ec2-user@ec2-52-90-116-36.compute-1.amazonaws.com:/var/lib/tomcat6/webapps
ssh  -i /home/mitesh/book.pem -o StrictHostKeyChecking=no -t -t ec2-user@ec2-52-90-116-36.compute-1.amazonaws.com "sudo service tomcat6 start"
```
-----------
```
node('Master') {
   // Mark the code checkout 'stage'
   stage 'Checkout'

   // Get code for PetClinic Application from a GitHub repository
   git url: 'https://github.com/mitesh51/spring-petclinic.git'

   // Get the maven tool.
   // This ' Maven3.3.1' maven tool must be configured in the global  configuration.           
   def mvnHome = tool 'Maven3.3.1'

   // Mark the code Compile 'stage'....
   stage 'Compile'
   // Run the maven build
   sh "${mvnHome}/bin/mvn clean compile"

   // Mark the code for Unit test execution and package 'stage'....
   stage 'Test&Package'
   sh "${mvnHome}/bin/mvn clean package"

   // Mark the code Cloud provisioning 'stage' where instance is allocated in Amazon EC2
// Once Instance is available, Chef will be used for Configuration Management
// knife ec2 plugin will be used for instance provisioning in the AWS cloud
   stage 'Cloud Provisioning'
   sh "ssh -t -t root@192.168.1.39 'ifconfig; rvm use 2.1.0; knife ec2 server create -I ami-1ecae776 -f t2.micro -N DevOpsVMonAWS9 --aws-access-key-id xxxxxxxxxxxxxxxxxxxx --aws-secret-access-key xxxxxxxxxxxxxxxxxxxxxxxxxxxxx -S book --identity-file book.pem --ssh-user ec2-user -r role[v-tomcat]'"
}
```

### Related DevOps Products:
* [Learning DevOps: Continuously Deliver Better Software](https://www.packtpub.com/networking-and-servers/learning-devops-continuously-deliver-better-software?utm_source=github&utm_medium=repository&utm_content=9781787126619)
* [Continuous Delivery and DevOps: A Quickstart guide](https://www.packtpub.com/virtualization-and-cloud/continuous-delivery-and-devops-quickstart-guide?utm_source=github&utm_medium=repository&utm_content=9781849693684)
* [Learning Chef](https://www.packtpub.com/networking-and-servers/learning-chef?utm_source=github&utm_medium=repository&utm_content=9781783285211)


### Suggestions and Feedback
[Click here](https://docs.google.com/forms/d/e/1FAIpQLSe5qwunkGf6PUvzPirPDtuy1Du5Rlzew23UBp2S-P3wB-GcwQ/viewform) if you have any feedback or suggestions.
