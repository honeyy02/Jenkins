pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Checkout code from Git repository
                git 'https://github.com/honeyy02/Jenkins.git'
            }
        }
        
        stage('Lint HTML') {
            steps {
                // Install htmlhint globally (assuming Node.js/npm is available)
                sh 'npm install -g htmlhint'
                // Run htmlhint on index.html file
                sh 'htmlhint index.html'
            }
        }
        
        stage('Deploy to GitHub Pages') {
            steps {
                script {
                    // Ensure Git is installed
                    tool name: 'Git', type: 'git'
                    
                    // Set up Git credentials (GitHub SSH key or username/password)
                    withCredentials([usernamePassword(credentialsId: 'c391c726-fb09-4c59-88ff-4216e34c8f8c', usernameVariable: 'honeyy02', passwordVariable: 'Honey@2402')]) {
                        // Clone the repository (assuming the 'gh-pages' branch exists)
                        git credentialsId: 'c391c726-fb09-4c59-88ff-4216e34c8f8c', url: 'https://github.com/honeyy02/Jenkins.git', branch: 'gh-pages'
                        
                        // Copy the built artifact to the repository
                        sh 'cp -r index.html ./'
                        
                        // Commit and push changes to GitHub Pages
                        sh '''
                            git config --global user.email "honeysharma0224@gmail.com"
                            git config --global user.name "honeyy02"
                            git add .
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
