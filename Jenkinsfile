
pipeline {

  environment {
    REGISTRYTAG = "116.203.255.57:5000/justme/myweb"
    IMAGE = ""
    LOCALREPOPATH = ""
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

          //Check local repo path
          LOCALREPOPATH = sh (returnStdout: true, script: 'pwd')
          print ("=== 2.2 Local repo path ${LOCALREPOPATH} === ")

          sh (returnStdout: true, script: "ls -la")

          print ("=== 2.3 Build image === ")
          sh (returnStdout: true, script: "docker build -t ${IMAGE} ${LOCALREPOPATH}")
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
