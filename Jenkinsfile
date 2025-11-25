pipeline {
    agent any
    
   triggers {
        GenericTrigger(
            genericVariables: [
                [key: 'ref', value: '$.ref'],
                [key: 'repo', value: '$.repository.full_name']
            ],
            causeString: 'Triggered by GitHub Webhook',
            token: 'yakisik-token',
            printPostContent: true
        )
    }
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
