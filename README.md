# git_jenkins_docker_pipeline
# JOB1
  Developer pushes to the development branch  
    i) Jenkins pulls the code from the development branch
      ii) After Successfull pull, docker container is launched with a httpd server
        sudo docker run -d -t -i -p 9090:80 -v /root/Desktop/test_web:/usr/local/apache2/htdocs --name test_web httpd:alpine
      iii) If a server is running, that container is removed first

# JOB2
  Developer pushes to the master branch  
     i) Jenkins pulls the code from the master branch
      ii) After Successfull pull, docker container is launched with a httpd server
       sudo docker run -d -t -i -p 9999:80 -v /root/Desktop/master_web:/usr/local/apache2/htdocs --name master_web httpd:alpine
      iii) If a server is running, that container is removed first
 
 # JOB3
  After giving Green signal to the new development features
    i) A job is triggered by the Jenkins which merges before build
      ii) This job merges the development branch with the master branch
        iii) After merging it pushes the repo back to the github
         iv) After successful build, JOB2 is triggered which launches the docker conatiner after master branch
    
  #NOTE-:
    Currently manual triggered is used, but github webhook is a better choice which can be done by using ngrok on port 8080
    
