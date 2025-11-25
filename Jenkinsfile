pipeline {
    agent any
    
   triggers {
    GenericTrigger(
        genericVariables: [
            [key: 'ref', value: '$.ref'],
            [key: 'repo', value: '$.repository.name']
        ],
        causeString: 'Triggered by GitHub Webhook',
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
