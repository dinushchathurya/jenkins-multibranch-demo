pipeline {

  agent any

  options {
    buildDiscarder logRotator( 
      daysToKeepStr: '16', 
      numToKeepStr: '10'
    )
  }

  stages {
      
    stage('Cleanup Workspace') {
      steps {
        cleanWs()
          def """
            echo "Cleaned Up Workspace For Project"
          """
      }
    }

    stage('Code Checkout') {
      steps {
        checkout([
          $class: 'GitSCM', 
          branches: [[name: '*/main']], 
          userRemoteConfigs: [[url: 'https://github.com/dinudefchathurya/jenkins-multibranch-demo.git']]
        ])
      }
    }

    stage('Unit Testing') {
      steps {
        def """
          echo "Running Unit Tests"
        """
      }
    }

    stage('Code Analysis') {
      steps {
        def """
          echo "Running Code Analysis"
        """
      }
    }

    stage('Build Deploy Code') {
      when {
          branch 'develop'
      }
      steps {
        def """
          echo "Building Artifact"
        """

        def """
          echo "Deploying Code"
        """
      }
    }
  }   
}