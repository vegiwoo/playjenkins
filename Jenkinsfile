
pipeline {

  environment {
    REGISTRYTAG = "116.203.255.57:5000/justme/myweb"
    IMAGE = ""
  }

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        print ("=== 1.Checkout Source === ")
        git 'https://github.com/justmeandopensource/playjenkins.git'
        print ("=== OK === ")
      }
    }

    stage('Build image') {
      steps{
        script {
          print ("=== 2.Build image === ")
          // Tag for future image
          IMAGE = REGISTRYTAG + ":latest"
          print ("=== 2.1 Tagging future image ${IMAGE} === ")
          // Build image
          docker.build IMAGE
          


          //sh (returnStdout: true, script: "docker build -t ${IMAGE} .")
          print ("=== OK === ")
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
