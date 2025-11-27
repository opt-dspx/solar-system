pipeline {
    agent any

    environment {
        SONAR_SCANNER_HOME = tool 'sonraqube-scanner-730'
        SONAR_TOKEN = credentials('sonar-token')
    }

    stages {

        stage('Security Checks') {
            parallel {
                stage('NPM Audit') {
                    steps {
                        sh 'npm audit --audit-level=critical || true'
                    }
                }
            }
        }

        stage('SAST - SonarQube') {
            steps {
                sh '''
                    $SONAR_SCANNER_HOME/bin/sonar-scanner \
                      -Dsonar.projectKey=12312d31123123 \
                      -Dsonar.sources=. \
                      -Dsonar.host.url=http://109.207.175.65:9000 \
                      -Dsonar.javascript.lcov.reportPaths=./coverage/lcov.info \
                      -Dsonar.token=$SONAR_TOKEN
                '''
            }
        }

    }
}
