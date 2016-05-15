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


