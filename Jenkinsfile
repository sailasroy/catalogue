pipeline {
    agent { node { label 'AGENT-1' } }

    stages {
        stage('Install dependencies') {
            steps {
                sh 'npm install'
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