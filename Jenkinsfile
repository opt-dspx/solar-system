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

        stage('Code Coverage') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'mongo-db-credentials',
                    passwordVariable: 'MONGO_PASSWORD',
                    usernameVariable: 'MONGO_USERNAME'
                )]) {
                    catchError(
                        buildResult: 'SUCCESS',
                        message: 'Oops! it will be fixed in future releases',
                        stageResult: 'UNSTABLE'
                    ) {
                        sh 'npm run coverage'
                    }
                }

                publishHTML([
                    allowMissing: true,
                    alwaysLinkToLastBuild: true,
                    keepAll: true,
                    reportDir: 'coverage/lcov-report',
                    reportFiles: 'index.html',
                    reportName: 'Code Coverage HTML Report',
                    reportTitles: '',
                    useWrapperFileDirectly: true
                ])
            }
        }

    }
}
