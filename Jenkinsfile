pipeline {
  agent any
  stages {
  	stage(' git clone or git pull' ) 
	{
		steps {
  			git url: 'https://github.com/dlgusrb3456/jenkins.git', branch: 'main'
		} 

	}

	stage( 'docker image build and push to p-registry' )
	{
		steps {
			sh '''
			docker build -t 192.168.8.100:5000/testweb:blue .
			doker push 192.168.8.100:5000/testweb:blue
			'''
			}

	}

	stage( 'deployment, svc creation' ) 
	{
		steps{ 
			sh '''
			kubectl create deploy testweb --image=192.168.8.100:5000/testweb:blue
			kubectl expose deploy testweb --type=LoadBalancer --port=80 --target-port=80 --name=testweb-svc
			'''
			}
	}
}
