
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

    stage('Check Docker') {
      steps {
        script {

          def statusCode = sh script:'dpkg --get-selections | grep doker', returnStatus:true

          if (statusCode == 1) {
            sh(returnStdout: true, script: 'apt update -y && apt upgrade -y')
            sh(returnStdout: true, script: 'apt-get install -y apt-transport-https ca-certificates curl gnupg-agent software-properties-common')
            sh(returnStdout: true, script: 'wget https://download.docker.com/linux/debian/gpg')
            sh(returnStdout: true, script: 'apt-key add gpg')
            sh(returnStdout: true, script: 'echo "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list')
            sh(returnStdout: true, script: 'apt update -y && apt upgrade -y')
            sh(returnStdout: true, script: 'apt install -y docker-ce docker-ce-cli containerd.io')
            sh(returnStdout: true, script: 'systemctl enable docker')

            print ("Docker installed now")
            def dockerNew = sh(returnStdout: true, script: 'docker -v')
            print (dockerNew)
          } else {
            print ("Docker installed")
            def dockerOld = sh(returnStdout: true, script: 'docker -v')
            print (dockerOld)
          }
        }
      }
    }



    //
    // stage('Checkout Source') {
    //   steps {
    //     print ("=== 1. Git Checkout  === ")
    //     checkout(
    //         [
    //             $class : 'GitSCM',
    //             branches : [[ name: REMOTEREPOBRANCH ]],
    //             doGenerateSubmoduleConfigurations: false,
    //             userRemoteConfigs : [[
    //                 url : REMOTEREPO,
    //                 credentialsId: CREDENTIALS
    //             ]]
    //         ]
    //     )
    //     print ("=== OK === ")
    //
    //     script {
    //       //Check local repo path
    //       LOCALREPOPATH = sh (returnStdout: true, script: 'pwd')
    //     }
    //   }
    // }
    //
    // stage('Build image') {
    //   steps{
    //     script {
    //       print ("=== 2.Build image === ")
    //       // Tag for future image
    //       IMAGE = REGISTRYTAG + ":latest"
    //       print ("=== 2.1 Tagging future image ${IMAGE} === ")
    //       //sh (returnStdout: true, script: "docker build -t ${IMAGE} ${LOCALREPOPATH}")
    //       //dockerImage = docker.build registry + ":$BUILD_NUMBER"
    //         print ("=== 2.2 Build image  === ")
    //         docker.build IMAGE
    //         print ("=== OK === ")
    //     }
    //   }
    // }

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
