pipeline {
    
  agent {
      label 'ubuntu_jsos'
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
				   
 sh "cd scrum-ui && npm run build"
				   
				     
				           }

		

    // some block

echo "hi"
sshagent(['vagrant_ubuntu_json_version']) {
    // some block


			sh "cd /home/vagrant/jen && git add --all -- \":!node_modules/*\" && git config --global user.name \"aksh153026\" && git config --global user.email \"aksh153026@gmail.com\" && git commit -m \"push version\" && git push git@github.com:aksh153026/scrum-ui.git HEAD:main"
				   
}
      }
    }
}
}
		
