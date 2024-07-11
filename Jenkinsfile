pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/honeyy02/Jenkins.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                sh 'echo "Building HTML project..."'
            }
        }

        stage('Test') {
            steps {
                sh 'echo "Running tests for HTML project..."'
            }
        }

        stage('Deploy') {
            steps {
                sh 'echo "Deploying HTML project..."'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            deleteDir()
        }
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
