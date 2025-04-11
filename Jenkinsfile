pipeline {
    agent any

    environment {
        FIREBASE_TOKEN = credentials('firebase-token') // Nome da credencial no Jenkins
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
                branch 'main'
            }
            steps {
                sh 'firebase use production'
                sh 'firebase deploy --only hosting'
            }
        }
    }
}
