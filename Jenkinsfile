#!groovy
properties([disableConcurrentBuilds()])

pipeline {

  environment {
    // Подготовка пути для сохранения изображения
    REGISTRYPATH = "116.203.255.57:5000/justme/myweb"
    // Подготовка имени будущего образа
    IMAGE = 'myweb:latest'
  }

  options {
      buildDiscarder(logRotator(numToKeepStr: '10', artifactNumToKeepStr: '10'))
  }

  agent {
      label 'master'
      }

  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/vegiwoo/playjenkins.git'
      }
    }

    stage('Build image') {
      steps{
        script {

          sh (returnStdout: true, script: "docker build -t ${IMAGE} ${REGISTRYPATH}")
        }
      }
    }

    stage('Push Image') {
      steps{
        script {
          docker.withRegistry( "" ) {
            IMAGE.push()
          }
        }
      }
    }

    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "myweb.yaml", kubeconfigId: "mykubeconfig")
        }
      }
    }

  }

}
