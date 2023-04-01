pipeline {
    agent { 
        node {
            label 'jenkins-agent-goes-here'
            }
      }
    triggers {
        pollSCM '*/5 * * * *'
    }
    stages {
        stage('Build') {
            steps {
                echo "Building.."
                sh '''
                npm install
                '''
            }
        }
        stage('Test') {
            steps {
                echo "Testing.."
                sh '''
                node index.js
                '''
            }
        }
        stage('Deliver') {
            steps {
                echo 'Deliver..'
                sh '''
                echo "doing delivery stuff.."
                '''
            }
        }
    }
}