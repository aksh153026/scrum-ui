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

def packageJSON = readJSON file: 'cd scrum-ui\package.json'
def packageJSONVersion = packageJSON.version
         def build_version = packageJSONVersion + "."+ env.BRANCH_NAME+"."+env.BUILD_ID
echo build_version
 bat "cd scrum-ui && npm install && npm version minor"
         
        }
      }
    }
}
}
		
