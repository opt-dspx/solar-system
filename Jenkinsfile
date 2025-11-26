pipeline {
    agent any
    
    stages {
        stage('Instaling Dependencies') {
            steps {
               sh '''
               npm install --no-audit 
               npm fund 
               '''

            }
           
        }
        stage('NPM Dependencies Audit') {
            steps {
               sh '''
               npm audit --audit-level=critical
               echo $?
               '''

            }
           
        stage('OWASP Dependency Check') {
            steps {
              dependencyCheck additionalArguments: '''
               --scan \'./\'
               --out \'./\'
              --format \'ALL\'
              --prettyPrint ''', odcInstallation: 'OWASP-DepCheck-10'
    }
}
    }
}
