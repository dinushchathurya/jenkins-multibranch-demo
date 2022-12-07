pipeline {

  agent any

  options {
    buildDiscarder logRotator( 
      daysToKeepStr: '16', 
      numToKeepStr: '10'
    )
  }

  stages {
      
    // stage('Cleanup Workspace') {
    //   steps {
    //     cleanWs()
    //       batch """
    //         echo "Cleaned Up Workspace For Project"
    //       """
    //   }
    // }

    stage('Code Checkout') {
      steps {
        checkout([
          $class: 'GitSCM', 
          branches: [[name: '*/main']], 
          userRemoteConfigs: [[url: 'https://github.com/dinubatchchathurya/jenkins-multibranch-demo.git']]
        ])
      }
    }

    stage('Unit Testing') {
      steps {
        batch """
          echo "Running Unit Tests"
        """
      }
    }

    stage('Code Analysis') {
      steps {
        batch """
          echo "Running Code Analysis"
        """
      }
    }

    stage('Build Deploy Code') {
      when {
          branch 'develop'
      }
      steps {
        batch """
          echo "Building Artifact"
        """

        batch """
          echo "Deploying Code"
        """
      }
    }
  }   
}