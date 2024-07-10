pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Checkout code from Git repository
                git branch: 'main', credentialsId: 'c391c726-fb09-4c59-88ff-4216e34c8f8c', url: 'https://github.com/honeyy02/Jenkins.git'
            }
        }
       stage('Deploy to GitHub Pages') {
    steps {
        script {
            // Ensure Git is installed (only necessary if you're managing Git installations in Jenkins)
            // tool name: 'Git', type: 'git'
            
            // Debug output
            echo 'Starting deployment...'
            echo 'Cloning repository...'
            
            // Set up Git credentials
            withCredentials([usernamePassword(credentialsId: 'c391c726-fb09-4c59-88ff-4216e34c8f8c', usernameVariable: 'honeyy02', passwordVariable: 'Honey@2402')]) {
                // Clone the repository's gh-pages branch
                sh '''
                    git clone --branch=gh-pages https://$honeyy02:$Honey@2402@github.com/honeyy02/Jenkins.git gh-pages
                    cd gh-pages
                    cp ../index.html .
                    git add .
                    git status  // Add this line for debugging
                    git commit -m "Deploying index.html to GitHub Pages"
                    git push
                '''
            }
        }
    }
}

    }
    
    post {
        success {
            echo 'Pipeline completed successfully!'
            // Additional actions for success
        }
        failure {
            echo 'Pipeline failed!'
            // Additional actions for failure
        }
        always {
            echo 'Pipeline execution completed.'
            // Cleanup tasks, notifications, etc.
        }
    }
}
