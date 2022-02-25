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
	
	stages 
	{
		
		stage('Checkout SCM') 
		{
			steps 
			{
				script
				{
					try
					{
						lastCommit = sh([script: 'git log -1', returnStdout: true])
						echo lastCommit	
						if (lastCommit.contains('push_package.json_version'))
						{
							currentBuild.result = 'ABORTED'
							error('ALread Done')
						}
					}
					catch(e)
					{
						throw e
					}					
				}
			}
		}
		stage('Built') 
		{
			steps 
			{
				script
				{
				
						
						def packageJSON = readJSON file: 'scrum-ui\\package.json'
						def packageJSONVersion = packageJSON.version
						def build_version = packageJSONVersion + "."+ env.BRANCH_NAME+"."+env.BUILD_ID
						echo build_version
						sh "cd scrum-ui && export PATH=$PATH:/home/vagrant/node-v12.14.0-linux-x64/bin &&  npm run build"
						sh "git add --all -- \":!node_modules/*\" && git config --global user.name \"aksh153026\" && git config --global user.email \"aksh153026@gmail.com\" && git commit -m \"push_package.json_version\" && git push git@github.com:aksh153026/scrum-ui.git HEAD:main"
					
								
				}
			}
		}		
	}
}
/* sshagent(['vagrant_ubuntu_json_version']) {		
	 }*/
			 
				   	    
	   	
