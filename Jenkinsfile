pipeline {
  agent any
  stages {
  	stage(' git clone or git pull' ) 
	{
		steps {
			git branch: 'main',
                    	    credentialsId: 'github_access_token',
                            url: 'https://github.com/dlgusrb3456/jenkins.git'
		} 

	}

	stage( 'mktestfile' )
	{
		steps {
			sh '''
			touch test9.txt
			'''
			}
		post {
                	failure {
                  	  echo 'Repository clone failure !'
                	}
                	success {
                  	  echo 'Repository clone success !'
                	}
        	}

	}
			  
	stage('Docker Image Build') 
	{
		app = docker.build("685766701737.dkr.ecr.ap-northeast-1.amazonaws.com/hr-pri-image")

    	}
	  
	stage('========== Push image ==========') {
		docker.withRegistry('https://685766701737.dkr.ecr.ap-northeast-1.amazonaws.com/hr-pri-image', 'lackm-ecr') {
		app.push("${env.BUILD_NUMBER}")
		app.push("latest")
	}

	  
}
}
