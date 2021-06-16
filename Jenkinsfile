pipeline {
    agent any
    tools {
        git 'Default'
        nodejs 'NodeJS' 
        jdk 'jdk1.8' 
        
    }
    stages {
    


        stage('SCM Checkout'){
            steps {
               git branch: 'main', url: 'https://github.com/aksh153026/scrum-ui.git'

            }
        }
     
        
        stage ('Compile Stage') {
            steps {
                
                bat "cd scrum-ui && npm install && npm audit fix  && ng build --prod "
                echo 'Build Compile Successful'
                }
            }
        stage ('Code Quality scan')  {
        
         tools {
         jdk "jh" 
        }
    
        steps {
         script  {
            scannerHome = tool 'sonar2' // the name you have given the Sonar Scanner (Global Tool Configuration)
        }
    
        withSonarQubeEnv('sonar') {
            
            bat "cd scrum-ui && npm install  && npm audit fix &  npm run sonar"
        }
         }
       
    }
    
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
       
    
