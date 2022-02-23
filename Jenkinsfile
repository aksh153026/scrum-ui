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
		      
                
		    withCredentials([gitUsernamePassword(credentialsId: 'github_json',
                 gitToolName: 'Default')]) {
			    echo GIT_ASKPASS
				   bat "git add --all -- \":!node_modules/*\" && git commit -c user.name=\"aksh153026\" -c user.email=\"aksh153026@gmail.com\" -m \"push version\" && git push origin HEAD:main"
				   }
      }
    }
}
}
		
