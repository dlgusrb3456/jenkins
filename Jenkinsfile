node {
     stage('Clone repository') {
         checkout scm
     }

     stage('Build image') {
         app = docker.build("685766701737.dkr.ecr.ap-northeast-1.amazonaws.com/test")
     }

     stage('Push image') {
         sh 'rm  ~/.dockercfg || true'
         sh 'rm ~/.docker/config.json || true'
          
         docker.withRegistry('https://685766701737.dkr.ecr.ap-northeast-1.amazonaws.com', 'ecr:ap-northeast-1:ecr_credential') {
             app.push("${env.BUILD_NUMBER}")
             app.push("latest")
     }
  }
     
     stage('Deploy Repo2'){
          checkout([$class: 'GitSCM',
                        branches: [[name: '*/main' ]],
                        extensions: scm.extensions,
                        userRemoteConfigs: [[
                            url: 'git@github.com:dlgusrb3456/ArgoCD.git',
                            credentialsId: 'jenkins-ssh-private',
                        ]]
                ])
          sshagent(credentials: ['jenkins-ssh-private']){
               sh("""
                        #!/usr/bin/env bash
                        set +x
                        export GIT_SSH_COMMAND="ssh -oStrictHostKeyChecking=no"
                        git config --global user.email "dlgusrb3456@naver.com"
                        git checkout main
                        #cd env/dev && kustomize edit set image arm7tdmi/node-hello-world:${env.BUILD_NUMBER}
                        echo "test jenkins" >> test1.txt
                        git commit -a -m "updated the image tag"
                        git push
                    """)
          }
          
     }
     
     
}
