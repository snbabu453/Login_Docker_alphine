pipeline {
 agent any
  environment {
    registry = "photosatya2/jmsth30-nodeapp"
    registryCredential = 'dockerhubcredentails'
    dockerImage = ''
  }
  stages {
    stage('get scm') {
      steps {
	  git credentialsId: 'gitcredentails', url: 'https://github.com/snbabu453/web_login_automation.git'
       }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('push image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
    stage('Remove old docker image') {
      steps{
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }
  }
}
