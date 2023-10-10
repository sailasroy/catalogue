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
        // sonar-scanner expets sonar-project.properties avilable or not
      stage('Sonar Scan') {
            steps {
                sh 'ls -ltr'
                sh 'sonar-scanner'
            }
        }
}


}