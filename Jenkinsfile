pipeline {
    
  agent {
      label 'master'
  }
  options {
    skipDefaultCheckout true
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

def packageJSON = readJSON file: 'package.json'
def packageJSONVersion = packageJSON.version
         def build_version = packageJSONVersion + "."+ env.BRANCH_NAME+"."+env.BUILD_ID
echo build_version
 bat "cd scrum-ui && npm install && npm version minor"
         
        }
      }
    }
}
}
		
