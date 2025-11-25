pipeline {
    agent any
    
   
    stages {
        stage('VM Node Version') {
            steps {
                sh '''
                    echo "Checking Node.js and npm versions on the VM node...."
                    node -v
                    npm -v
                '''
            }
        }
    }
}
