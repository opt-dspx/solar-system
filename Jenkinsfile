pipeline {
    agent any
    
    stages {

        stage('Installing Dependencies') {
            steps {
                sh '''
                    npm install --no-audit
                    npm fund
                '''
            }
        }

        stage('Security Checks') {
            parallel {

                stage('NPM Audit') {
                    steps {
                        sh '''
                            npm audit --audit-level=critical
                            echo $?
                        '''
                    }
                }

            }
        }
    }
}
