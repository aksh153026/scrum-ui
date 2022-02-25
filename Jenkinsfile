pipeline {
    
  agent {
      label 'master'
  }
  //ubuntu_jsos
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
				   
 powershell "cd scrum-ui ; npm run build"
				   
				  //   && export PATH=$PATH:/home/vagrant/node-v12.14.0-linux-x64/bin 
				           }

		

    // some block

    // some block
//sshagent(['vagrant_ubuntu_json_version']) {

			powershell "git add --all -- \":!node_modules/*\" ; git config --global user.name \"aksh153026\" ; git config --global user.email \"aksh153026@gmail.com\" ; git commit -m \"push_version\" ; git push git@github.com:aksh153026/scrum-ui.git HEAD:main"
				   
	//    }
      }
    }
}
}
		
