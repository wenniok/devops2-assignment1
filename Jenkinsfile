pipeline {
    agent any

    environment {
        GOOGLE_APPLICATION_CREDENTIALS = credentials('google-application-credentials')
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
                // Copy the credentials file to a temporary location
                sh 'cp $GOOGLE_APPLICATION_CREDENTIALS /tmp/google-application-credentials.json'

                // Set the environment variable for Firebase CLI
                sh 'export GOOGLE_APPLICATION_CREDENTIALS=/tmp/google-application-credentials.json'

                sh 'firebase use staging'
                sh 'firebase deploy --token $FIREBASE_TOKEN --only hosting'
            }
        }


        stage('Production') {
            when {
                branch 'main'
            }
            steps {
                // Copy the credentials file again to the temporary location
                sh 'cp $GOOGLE_APPLICATION_CREDENTIALS /tmp/google-application-credentials.json'

                // Set the environment variable for Firebase CLI
                sh 'export GOOGLE_APPLICATION_CREDENTIALS=/tmp/google-application-credentials.json'

                sh 'firebase use production'
                sh 'firebase deploy --only hosting''
            }
        }
    }
}
