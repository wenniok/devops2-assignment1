pipeline {
    agent any


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
                sh 'firebase deploy --only hosting'
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
