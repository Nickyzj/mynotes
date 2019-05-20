# Jenkins Tutorials

## Tutorial 1

### download

* download war file
* `java -jar jenkins.war`
* get admin password `4e3a1ab62cde46c8992a681f93b933ab`
* http://localhost:8080
* put in password
* install plugin. Plugin folders at ~/.jenkins
* change port `java -jar jenkins.war --httpPort=9090`



## Tutorial 2 - Setup Jenkins on Tomcat

* download tomcat zip
* goto tomcat/bin
* chmod +x *.sh
* copy jenkins.war inside tomcat/webapp folder
* startup tomcat `./startup.sh`  `./shudown.sh`
* http://localhost:8080/jenkins



## Tutorial 3 - Change Home Directory

### Jenkins home directory

* All configurations
* Plugins
* Job details
* Logs

Manage Jenkins - Configuration - Home Directory

* create a new folder
* copy all data from old dir to new dir
* change env variable - JENKINS_HOME set to new dir
* linux: change .bash_profile`export JENKINS_HOME=<new path>`
* restart jenkins
* http://localhost:8080/systemInfo

## Tutorial 4 - Use CLI

* http://localhost:8080/cli/
* download jenkins cli jar.
* `java -jar jenkins-cli.jar -s http://localhost:8080/ help`
* id_rsa: admin - configuration - SSH Public Keys
* `java -jar jenkins-cli.jar -s http://localhost:8080/ <command> --username <username> --password <password>`

## Tutorial 5 - Manage User

* 系统管理 - 管理用户
* role strategy plugin
* 系统管理 - manage and asign roles

