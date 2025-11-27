pipeline {
    agent any

    environment {
        SONAR_SCANNER_HOME = tool 'sonraqube-scanner-730'
    }

    stages {

        stage('Security Checks') {
            parallel {

                stage('NPM Audit') {
                    steps {
                        sh '''
                            npm audit --audit-level=critical || true
                        '''
                    }
                }

            }
        }

        stage('Code Coverage') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'mongo-db-credentials',
                    usernameVariable: 'MONGO_USERNAME',
                    passwordVariable: 'MONGO_PASSWORD'
                )]) {
                    catchError(buildResult: 'SUCCESS', stageResult: 'UNSTABLE') {
                        sh 'npm run coverage'
                    }
                }

                publishHTML([
                    allowMissing: true,
                    alwaysLinkToLastBuild: true,
                    keepAll: true,
                    reportDir: 'coverage/lcov-report',
                    reportFiles: 'index.html',
                    reportName: 'Code Coverage HTML Report'
                ])
            }
        }

        stage('SAST - SonarQube') {
            steps {
                sh 'echo $SONAR_SCANNER_HOME'
                sh '''
                    $SONAR_SCANNER_HOME/bin/sonar-scanner \
                      -Dsonar.projectKey=Solar-System-Project \
                      -Dsonar.sources=. \
                      -Dsonar.host.url=http://109.207.175.65:9000 \
                      -Dsonar.token=$SONAR_TOKEN
                '''
            }
        }

    }
}
