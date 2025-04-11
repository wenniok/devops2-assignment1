pipeline {
    agent any

    environment {
        FIREBASE_TOKEN = credentials('firebase-token')
    }

    stages {
        stage('Build') {
            steps {
                 echo 'Build testing only for this assignment.'
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
                    sh 'git status'
                    def branchName = sh(script: 'git rev-parse --abbrev-ref HEAD || echo "not-a-branch"', returnStdout: true).trim()
                    
                    // Imprime o nome da branch
                    echo "Current branch is: ${branchName}"
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
