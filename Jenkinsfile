pipeline {
    
  agent {
      label 'master'
  }
  
  
    tools {
        git 'Default'
        nodejs 'NodeJS'
		maven 'MAVEN_HOME' 
        jdk 'jdk1.8' 
    }
    stages {
		stage('Checkout SCM') {
            steps {
               checkout([$class: 'GitSCM', branches: [[name: '*/main'], [name: '*/dev'], [name: '*/qa']],  doGenerateSubmoduleConfigurations: false, 
                          extensions: [], 
                          gitTool: 'Default', userRemoteConfigs: [[credentialsId: 'b0e5e069-fefe-4f2e-8cbc-d05703a18d3d', url: 'https://github.com/aksh153026/scrum-ui.git']]])
               
                
            }
        }
        stage('GIT BRANCH NAME') {
            steps {
                
				script {
					 env.GIT_BRANCH_PATH=bat(returnStdout: true, script: "git name-rev --name-only HEAD").trim()
    env.GIT_BRANCH_NAME=GIT_BRANCH_PATH.split('remotes/')[1]
     
				}
				
            }
        }
        stage('GIT BRANCH NAME1') {
            steps {
			echo GIT_BRANCH_NAME
            }
        }
		
        
		stage ('Compile Stage front-end') {
            when {
				expression {   
					env.GIT_BRANCH_NAME=='origin/dev' 
				}
			}
			steps {
                
                bat "cd scrum-ui && npm install && npm audit fix && ng build --prod"
                echo 'Build Compile Successful'
            }
		}
		
		
	   stage ('Code Quality scan front-end')  {
			when {
				expression {   
					env.GIT_BRANCH_NAME=='origin/qa' 
				}
			}
			tools {
				jdk "jh" 
			}
    
			steps {
				script  {
					scannerHome = tool 'sonar2' // the name you have given the Sonar Scanner (Global Tool Configuration)
				}
    
				withSonarQubeEnv('sonar') {
            
					bat "cd scrum-ui && npm install  && npm audit fix &&  npm run sonar"
				}
			}
       }


      
		stage ('Push dev image to sonartype nexus front-end') { 
        
			when {
				expression {   
					env.GIT_BRANCH_NAME=='origin/dev' 
				}
			}
    
			steps {
        
				script {
					docker.withRegistry('http://192.168.29.240:8083/', '1234') {

					bat "cd scrum-ui && docker build -t 192.168.29.240:8083/front-end:${env.BUILD_ID} . && docker push 192.168.29.240:8083/front-end:${env.BUILD_ID}"
       
					}
          
				}
			}
       
		}
		
	
		stage ('Push qa image to sonartype nexus front-end') { 
        
			when {
				expression {   
					env.GIT_BRANCH_NAME=='origin/qa' 
				}
			}
    
			steps {
        
				script {
					docker.withRegistry('http://192.168.29.240:8083/', '1234') {

					bat "cd scrum-ui && docker build -t 192.168.29.240:8083/front-end:${env.BUILD_ID} . && docker push 192.168.29.240:8083/front-end:${env.BUILD_ID}"
       
					}
          
				}
			}
       
		}
		
		
		
		stage ('Push main image to sonartype nexus front-end') { 
        
			when {
				expression {   
					GIT_BRANCH_NAME == 'origin/main' 
				}
			}
    
			steps {
        
				script {
					docker.withRegistry('http://192.168.29.240:8083/', '1234') {

					bat "cd scrum-ui && docker build -t 192.168.29.240:8083/front-end:${env.BUILD_ID} . && docker push 192.168.29.240:8083/front-end:${env.BUILD_ID}"
       
					}
          
				}
			}
       
		}
    
		
		
		stage ('Pull image from sonartype nexus in dev server front-end') { // take that image and push to artifactory
			when {
				expression {   
					env.GIT_BRANCH_NAME=='origin/dev' 
				}
			}
     
			agent {
				label 'v-test'
			}
      
			steps{   

				sh """#!/bin/bash 
				sudo docker login -u admin -p admin http://192.168.29.240:8083/
				sudo docker container rm -f scrum-ui
				sudo docker run -i -p 4200:80 --name scrum-ui --link scrum-app 192.168.29.240:8083/front-end:${env.BUILD_ID} 
				"""

			}
    
          
		}
		
		
		
		stage ('Pull image from sonartype nexus in qa server front-end') { // take that image and push to artifactory
			when {
				expression {   
					env.GIT_BRANCH_NAME=='origin/qa' 
				}
			}
     
			agent {
				label 'v-test'
			}
      
			steps{   

				sh """#!/bin/bash 
				sudo docker login -u admin -p admin http://192.168.29.240:8083/
				sudo docker container rm -f scrum-ui
				sudo docker run -i -p 4200:80 --name scrum-ui --link scrum-app 192.168.29.240:8083/front-end:${env.BUILD_ID} 
				"""

			}
    
          
		}
		
	
		stage ('Pull image from sonartype nexus in main server front-end') { // take that image and push to artifactory
			when {
				expression {   
					env.GIT_BRANCH_NAME=='origin/main' 
				}
			}
     
			agent {
				label 'v-test'
			}
      
			steps{   

				sh """#!/bin/bash 
				sudo docker login -u admin -p admin http://192.168.29.240:8083/
				
				sudo docker container rm -f scrum-ui
				
				sudo docker run -d -p 4200:80 --name scrum-ui --link scrum-app 192.168.29.240:8083/front-end:${env.BUILD_ID}
				"""

			}
    
          
		}
    }
     post {
        always {
            emailext body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}",
                recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']],
                subject: "Jenkins Build ${currentBuild.currentResult}: Job ${env.JOB_NAME}", to: 'aksh152630@gmail.com'
            
        }
    }
}
