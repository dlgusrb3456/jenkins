pipeline {
  agent any
  stages {
  	stage(' git clone or git pull' ) 
	{
		steps {
  			git url: 'https://github.com/dlgusrb3456/jenkins.git', branch: 'main'
		} 

	}

	stage( 'mktestfile' )
	{
		steps {
			sh '''
			touch test.txt
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
