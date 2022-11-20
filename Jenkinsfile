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
}
