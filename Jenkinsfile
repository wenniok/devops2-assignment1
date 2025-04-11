pipeline {
    agent any

    environment {
        FIREBASE_TOKEN = credentials('firebase-token')
    }

    stages {
        stage('Build') {
            steps {
                 sh 'npm install'
            }
        }


        stage('Test') {
            steps {
                echo 'Manual testing only for this assignment.'
            }
        }


        stage('Staging') {
            steps {
                sh 'firebase use staging'
                sh 'firebase deploy --token $FIREBASE_TOKEN --only hosting'
            }
        }


        stage('Production') {
            when {
                expression {
                    checkout scm // Faz o checkout do repositório configurado pelo Jenkins
                    echo "Current branch is: ${sh(script: 'git rev-parse --abbrev-ref HEAD', returnStdout: true).trim()}"
                    return sh(script: 'git rev-parse --abbrev-ref HEAD', returnStdout: true).trim() == 'main'
                }
            }
            steps {
                sh 'firebase use production'
                sh 'firebase deploy --token $FIREBASE_TOKEN --only hosting'
            }
        }
    }
}
