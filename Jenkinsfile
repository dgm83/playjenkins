pipeline {

  environment {
    registry = "dgm83/pruebajen"
    registryCredential = 'd=8!DFcZ~b@5U&tV'
  }

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/dgm83/playjenkins.git'
      }
    }

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }

    stage('Push Image') {
      steps{
        script {
          docker.withRegistry( "" ) {
            dockerImage.push()
          }
        }
      }
    }

    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "myweb.yaml", kubeconfigId: "my-kubernetes")
        }
      }
    }

  }

}
