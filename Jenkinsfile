pipeline {
    agent any
    
    environment {
        REPO_URL = 'https://github.com/honeyy02/Jenkins.git'
        BRANCH = 'main'
        DEPLOY_DIR = '/var/www/html'  // Directory where the page will be deployed
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: "${env.BRANCH}", url: "${env.REPO_URL}"
            }
        }
        
        stage('Deploy') {
            steps {
                script {
                    def indexHtml = readFile 'index.html'
                    writeFile file: "${env.DEPLOY_DIR}/index.html", text: indexHtml
                }
            }
        }
    }
    
    post {
        always {
            cleanWs()
        }
    }
}
