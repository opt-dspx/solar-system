pipeline {
    agent any
    
    stages {
        stage('Instaling Dependencies') {
            steps {
               sh ''
               npm install --no-audit 
               npm fund 
               ''

            }
           
        }
    }
}
