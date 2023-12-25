
pipeline {
    agent any

    environment {
        DOCKER_HUB_CREDENTIALS = credentials('docker-hub-credentials-id')
    }

    stages {
        stage('Build') {
            steps {
                script {
                    // Clone the repository
                    checkout scm

                    // Build Docker image
                    sh 'docker build -t your-web-app:${BUILD_NUMBER} .'
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    // Implement your testing steps here
                    // e.g., sh 'docker run your-web-app:${BUILD_NUMBER} npm test'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Deploy Docker image
                    sh 'docker push your-web-app:${BUILD_NUMBER}'
                }
            }
        }
    }

    post {
        failure {
            // Notify the team on failed deployment
            emailext subject: 'Deployment Failed - ${currentBuild.fullDisplayName}',
                      body: 'Please check the Jenkins build for details.',
                      to: 'team@example.com'
        }
    }
}
