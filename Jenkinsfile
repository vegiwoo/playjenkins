
pipeline {

  environment {
    REMOTEREPO = 'https://github.com/justmeandopensource/playjenkins.git'
    REMOTEREPOBRANCH = 'master'
    CREDENTIALS = 'github_login_and_password'
    LOCALREPOPATH = ''

    REGISTRYTAG = "116.203.255.57:5000/justme/myweb"
    IMAGE = ""
  }

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        print ("=== 1. Git Checkout  === ")
        checkout(
            [
                $class : 'GitSCM',
                branches : [[ name: REMOTEREPOBRANCH ]],
                doGenerateSubmoduleConfigurations: false,
                userRemoteConfigs : [[
                    url : REMOTEREPO,
                    credentialsId: CREDENTIALS
                ]]
            ]
        )
        print ("=== OK === ")

        script {
          //Check local repo path
          LOCALREPOPATH = sh (returnStdout: true, script: 'pwd')
        }
      }
    }

    stage('Build image') {
      steps{
        script {
          print ("=== 2.Build image === ")
          // Tag for future image
          IMAGE = REGISTRYTAG + ":latest"
          print ("=== 2.1 Tagging future image ${IMAGE} === ")
          //sh (returnStdout: true, script: "docker build -t ${IMAGE} ${LOCALREPOPATH}")
          //dockerImage = docker.build registry + ":$BUILD_NUMBER"
            print ("=== 2.2 Build image  === ")
            docker.build IMAGE
            print ("=== OK === ")
        }
      }
    }

    // stage('Push Image') {
    //   steps{
    //     script {
    //       docker.withRegistry( "" ) {
    //         IMAGE.push()
    //       }
    //     }
    //   }
    // }
    //
    // stage('Deploy App') {
    //   steps {
    //     script {
    //       kubernetesDeploy(configs: "myweb.yaml", kubeconfigId: "mykubeconfig")
    //     }
    //   }
    // }

  }

}
