#!groovy
properties([disableConcurrentBuilds()])

pipeline {
  options {
      buildDiscarder(logRotator(numToKeepStr: '10', artifactNumToKeepStr: '10'))
  }

  agent {
      label 'master'
  }

  environment
      {
          GITREPO = "https://github.com/vegiwoo/playjenkins.git"
      }
  stages {
    stage('Checkout Source') {
        steps {
          print ("=== STEP 1 - SOURCE GITCODE ===")
          git GITREPO
          print ("Source OK")
        }
    }

    // stage('Build image') {
    //
    //
    //
    //
    // }
    //
    // stage('Push Image') {
    //
    // }
    //
    // stage('Deploy App') {
    //
    // }
  }

}
