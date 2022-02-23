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
		    
		    
		           script{

def packageJSON = readJSON file: 'scrum-ui\\package.json'
def packageJSONVersion = packageJSON.version
         def build_version = packageJSONVersion + "."+ env.BRANCH_NAME+"."+env.BUILD_ID
echo build_version
				   
 bat "cd scrum-ui && npm run build"
				   
				     
				           }
		      
                
		   sshagent (credentials: ['1938eb47-e7e8-4fed-b88c-87561e128345']) {
  sh('git config --global user.name "Jenkins"')
  sh('git config --global user.email "jenkins@company.com"')
  sh('git checkout master')
  sh('git pull origin master')
  sh('git checkout HEAD --force')
  lastCommit = sh([script: 'git log -1', returnStdout: true])


				   powershell "git add --all -- \":!node_modules/*\" && git config --global user.name \"aksh153026\" && git config --global user.email \"aksh153026@gmail.com\" && git commit -m \"push version\" && git push origin HEAD:main"
				   }
      }
    }
}
}
		
