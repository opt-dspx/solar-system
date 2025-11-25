pipeline {
    agent any
    
    tools {
        nodejs 'NodeJS-22' // Ensure this matches the name of your NodeJS installation in Jenkins
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
