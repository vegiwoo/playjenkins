
pipeline {

  environment {
    REMOTEREPO = 'https://github.com/justmeandopensource/playjenkins.git'
    REMOTEREPOBRANCH = 'master'
    CREDENTIALS = 'gitHub_login_password'
    LOCALREPOPATH = ''

    DOCKERHOST = 'tcp://116.203.255.57:5000'
    REGISTRYTAG = "116.203.255.57:5000/justme/myweb"
    IMAGE = ""
  }

  agent any

  stages {
    stage('Docker info') {
      steps {
        script {
          sh script:'docker -info'
        }
      }
    }
    

    // stage('Check Docker on Jenkins Pod') {
    //   steps {
    //     script {
    //       print ("=== 1. Check Docker on Jenkins Pod  === ")
    //       def statusCodeGrep = sh script:'dpkg --get-selections | grep doker', returnStatus:true
    //       def statusCodeDockerV = sh script:'docker -v', returnStatus:true
    //
    //       if (statusCodeDockerV == 127) {
    //         sh(returnStdout: true, script: 'apt update -y && apt upgrade -y')
    //         sh(returnStdout: true, script: 'apt-get install -y apt-transport-https ca-certificates curl gnupg-agent software-properties-common')
    //         sh(returnStdout: true, script: 'wget https://download.docker.com/linux/debian/gpg')
    //         sh(returnStdout: true, script: 'apt-key add gpg')
    //         sh(returnStdout: true, script: 'echo "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list')
    //         sh(returnStdout: true, script: 'apt update -y && apt upgrade -y')
    //         sh(returnStdout: true, script: 'apt install -y docker-ce docker-ce-cli containerd.io')
    //         sh(returnStdout: true, script: 'systemctl enable docker')
    //
    //         print ("=== Docker installed now ===")
    //
    //         print (dockerNew)
    //       } else {
    //         print ("=== Docker installed ===")
    //       }
    //     }
    //   }
    // }
    //
    // stage('Checkout Source') {
    //   steps {
    //     print ("=== 2. Git Repo Checkout  === ")
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
    //
    //     script {
    //       //Check local repo path
    //       LOCALREPOPATH = sh (returnStdout: true, script: 'pwd')
    //       print ("=== Localpath is ${LOCALREPOPATH} === ")
    //       print ("=== OK === ")
    //     }
    //   }
    // }
    //
    // stage('Build image') {
    //   steps{
    //     script {
    //       print ("=== 3.Build image === ")
    //       // Tag for future image
    //       IMAGE = REGISTRYTAG + ":latest"
    //       print ("=== 3.1 Tagging future image ${IMAGE} ===")
    //
    //       // print ("=== 3.2 Hosting Docker ===")
    //       // sh (returnStdout: true, script: "sudo docker -H tcp://116.203.255.57:5000 unix:///var/run/docker.sock")
    //
    //       print ("=== 3.2 Build image  ===")
    //
    //       sh (returnStdout: true, script: "docker build -t ${IMAGE} ${LOCALREPOPATH}")
    //       print ("=== OK === ")
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
