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
                sh """
                    echo "Cleaned Up Workspace For Project"
                """
            }
        }

        stage('Code Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM', 
                    branches: [[name: '*/main']], 
                    userRemoteConfigs: [[url: 'https://github.com/dinushchathurya/jenkins-multibranch-demo.git']]
                ])
            }
        }

        stage('Unit Testing') {
            steps {
                sh """
                    echo "Running Unit Tests"
                """
            }
        }

        stage('Code Analysis') {
            steps {
                sh """
                    echo "Running Code Analysis"
                """
            }
        }

        stage('Build Code') {
            when { 
                anyof {
                    branch 'develop'
                    branch 'main'
                }
            }
            steps {
                sh """
                    echo "Building Artifact"
                """
            }
        }

        stage('Deploy Code  to Dev') {
            when { 
                branch 'develop'
            }
            steps {
                sh """
                    echo "Deploy to Dev"
                """
            }
        }

        stage('Deploy Code  to Prod') {
            when { 
                branch 'main'
            }
            steps {
                sh """
                    echo "Deploy to Dev"
                """
            }
        }

    }  

}
