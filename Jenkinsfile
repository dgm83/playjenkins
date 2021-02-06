pipeline {

  agent {
   node{label 'master'}
  }

  environment {
    registry = "dgm83/pruebajen:v2"
    registryCredential = 'dockerhub'
  }

  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/dgm83/playjenkins.git'
      }
    }

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build (registry, "-f Dockerfile .")
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
