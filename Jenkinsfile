pipeline {
    agent any
    
    tools {
        nodejs 'nodejs-25-2-1' // Ensure this matches the name of your NodeJS installation in Jenkins
    }
    stages {
        stage('VM Node Version') {
            steps {
                sh '''
                    node -v
                    npm -v
                '''
            }
        }
    }
}
