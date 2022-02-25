pipeline 
{
	agent
	{
		label 'ubuntu_jsos'
	}
  //ubuntu_jsos
	tools 
	{
		git 'Default'
		nodejs 'NodeJS'
		maven 'MAVEN_HOME' 
		jdk 'jdk1.8' 
	}
	def i=0
	stages 
	{
		try{
		stage('Checkout SCM') 
		{
			steps 
			{
				script
				{
					i=1
					error("fun")
					def packageJSON = readJSON file: 'scrum-ui\\package.json'
					def packageJSONVersion = packageJSON.version
					def build_version = packageJSONVersion + "."+ env.BRANCH_NAME+"."+env.BUILD_ID
					echo build_version
					sh "cd scrum-ui && export PATH=$PATH:/home/vagrant/node-v12.14.0-linux-x64/bin &&  npm run build"
					lastCommit = sh([script: 'git log -1', returnStdout: true])
				}
				echo lastCommit	
				sh "git add --all -- \":!node_modules/*\" && git config --global user.name \"aksh153026\" && git config --global user.email \"aksh153026@gmail.com\" && git commit -m \"push_version\" && git push git@github.com:aksh153026/scrum-ui.git HEAD:main"

			}
		}
		}
		catch(e){
			if (i==1){
				echo "error"
			}
			throw e
		}
	}
}
// sshagent(['vagrant_ubuntu_json_version']) {		
	 // }
			 
				   	    
	   	
