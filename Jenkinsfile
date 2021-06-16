pipeline {
    agent any
    tools {
        git 'Default'
        nodejs 'NodeJS' 
        jdk 'jdk1.8' 
    }
    stages {
    

    
 stage ('Push image to sonartype nexus') { // take that image and push to artifactory
        
         
    
        steps {
        
      script {
        docker.withRegistry('http://192.168.29.240:8083/', '1234') {

        bat "cd scrum-app && docker build -t 192.168.29.240:8083/front-end:1.0.1 . && docker push 192.168.29.240:8083/front-end:1.0.1"

       
    }
          
      }
         }
       
    }

}
        
    
}
node("vagrant1"){
    
    stage ('Push image to sonartype nexus') { // take that image and push to artifactory
        
     
        
      
        

        sh """#!/bin/bash 
        sudo docker login -u admin -p admin http://192.168.29.240:8083/
        sudo docker run -p 8080:8080 192.168.29.240:8083/front-end:1.0.1 
        """

       
    
          
      }
         }
       
    
