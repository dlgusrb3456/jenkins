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
		    app = docker.build("685766701737.dkr.ecr.ap-northeast-1.amazonaws.com/hr-pri-image")
		    
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
		 steps{
		 	docker.withRegistry('https://685766701737.dkr.ecr.ap-northeast-1.amazonaws.com/hr-pri-image', 'lackm-ecr') {
			app.push("${env.BUILD_NUMBER}")
			app.push("latest")
    			}
		 }
		 post {
			failure {
			  echo 'Docker image Push failure !'
			}
			success {
			  echo 'Docker image Push success !'
			}
		}
    		
	}

	  
}
}
