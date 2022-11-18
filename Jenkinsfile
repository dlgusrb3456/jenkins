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
			  
	stage('Docker Image Build') {
		steps {
		    sh "docker build ."
		}
		post {
			failure {
			  echo 'Docker image build failure !'
			}
			success {
			  echo 'Docker image build success !'
			}
		}
    }
	  
	 stage('========== Push image ==========') {
    		docker.withRegistry('685766701737.dkr.ecr.ap-northeast-1.amazonaws.com/hr-pri-image', 'lackm-ecr') {
			app.push("${env.BUILD_NUMBER}")
			app.push("latest")
    		}
	}

	  
}
}
