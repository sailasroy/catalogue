pipeline {
    agent { node { label 'AGENT-1' } }

    stages {
        stage('Install dependencies') {
            steps {
                sh 'npm install'
            }
        }

    stage('Unit test') {
            steps {
                sh 'unit test is sucessfull'
            }
        }
}


}