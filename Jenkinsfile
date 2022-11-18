node {
     stage('Clone repository') {
         checkout scm
     }

     stage('Build image') {
         app = docker.build("685766701737.dkr.ecr.ap-northeast-1.amazonaws.com/hr-pri-image")
     }

     stage('Push image') {
         
         docker.withRegistry('https://685766701737.dkr.ecr.ap-northeast-1.amazonaws.com/hr-pri-image', 'lackm-ecr') {
             app.push("${env.BUILD_NUMBER}")
             app.push("latest")
     }
  }
}
