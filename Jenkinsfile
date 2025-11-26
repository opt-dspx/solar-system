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

        stage('Security Checks in Parallel') {
            parallel {

                NPM_Audit: {
                    stage('NPM Dependencies Audit') {
                        steps {
                            sh '''
                                npm audit --audit-level=critical
                                echo $?
                            '''
                        }
                    }
                }

                OWASP_Check: {
                    stage('OWASP Dependency Check') {
                        steps {
                            dependencyCheck additionalArguments: '''
                                --scan ./
                                --out ./
                                --format ALL
                                --prettyPrint
                            ''',
                            odcInstallation: 'OWASP-DepCheck-10'
                        }
                    }
                }
            }
        }
    }
}
