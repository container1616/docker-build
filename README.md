# docker-build
A simple Docker build life-cycle (github+jenkins) illustration. Here are the steps

1) Developer commits the code into github

2) Github triggers the Jenkins build or Jenkins job is polling github continually for any change

3) One build is trigger in Jenkins

  3.1) Jenkins builds the java code
  
  3.2) Jenkins builds the docker image based on dockerfile
  
  3.3) Jenkins pushes the image to docker image registry ( docker hub or artifactory)
  
  3.4) Jenkins run the Docker container into *test*  machine.  
  
    3.5.1) Jenkins to do "docker run" remotely 
    
    3.5.2) SSH into test machine and do "docker run" 
    

# Steps Details

### Get a machine on DigitalOcean or any other cloud 
### Install Maven
	sudo apt-get update
	sudo apt-get install maven2 -y
	
### install open jdk8
	sudo add-apt-repository ppa:openjdk-r/ppa
	
	sudo apt-get update
	
	sudo apt-get install openjdk-8-jdk -y

	- if java is still pointing to old version, just delete the link and provide new link
		cd /etc/alternatives
		rm java ; ln -s /usr/lib/jvm/java-8-openjdk-amd64/bin/java java

### install jenkins 
  (For more info goto  
    https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu)
	
	wget -q -O - https://jenkins-ci.org/debian/jenkins-ci.org.key | sudo apt-key add -
	sudo sh -c 'echo deb http://pkg.jenkins-ci.org/debian binary/ > /etc/apt/sources.list.d/jenkins.list'
	sudo apt-get update
	sudo apt-get install jenkins

	- adding jenkins user to sudo and docker group
		sudo adduser jenkins sudo
		usermod -G docker jenkins

	- configure /etc/sudoers file, so that jenkins user can execute script without password
		jenkins ALL=(ALL) NOPASSWD: ALL
		paste above line at the end of sudoers file

### create second *Test* machine in cloud 
(Docker container on this machine. Jenkin will do the pull and run)
Make sure the Jenkins machine is able to do SSH into this machine. (Refer this link for more details http://www.linuxproblem.org/art_9.html). 



