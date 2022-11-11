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
			touch test4.txt
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

	
}
}
