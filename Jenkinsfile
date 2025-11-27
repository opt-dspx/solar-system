pipeline {
    agent any

    environment {
        SONAR_SCANNER_HOME = TOOL 'sonraqube-scanner-730'
        
    }
    
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
        stage('SAST - SonraQube') {
            steps {
                sh 'echo $SONAR_SCANNER_HOME'
                sh '''
                    $SONAR_SCANNER_HOME/bin/sonar-scanner \
                      -Dsonar.projectKey=Solar-System-Project \
                      -Dsonar.sources=. \
                      -Dsonar.host.url=http://109.207.175.65:9000 \
                      -Dsonar.token=sqp_4aad086848c884e8eb1b3bd5b1a8083eaaabd410
                    
                '''
            }
        }
    }
}
