pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Checkout code from Git repository
                git branch: 'main', url: 'https://github.com/honeyy02/Jenkins.git'
            }
        }
        
        stage('Lint HTML') {
            steps {
                script {
                    try {
                        // Install htmlhint globally (assuming Node.js/npm is available)
                        sh 'npm install -g htmlhint'
                        // Run htmlhint on index.html file
                        sh 'htmlhint index.html'
                    } catch (Exception e) {
                        echo 'Linting failed'
                        error 'Linting HTML failed. Check the console output for details.'
                    }
                }
            }
        }
        
        stage('Deploy to GitHub Pages') {
            steps {
                script {
                    // Ensure Git is installed
                    tool name: 'Git', type: 'git'
                    
                    // Set up Git credentials (GitHub SSH key or username/password)
                    withCredentials([usernamePassword(credentialsId: 'c391c726-fb09-4c59-88ff-4216e34c8f8c', usernameVariable: 'honeyy02', passwordVariable: 'Honey@2402')]) {
                        // Clone the repository's gh-pages branch
                        sh '''
                            git clone --branch=gh-pages https://$honeyy02:$Honey@2402@github.com/honeyy02/Jenkins.git gh-pages
                            cd gh-pages
                            cp ../index.html .
                            git add .
                            git config user.email "honeysharma0224@gmail.com"
                            git config user.name "honeyy02"
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
