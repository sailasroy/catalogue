pipeline {
    agent { node { label 'AGENT-1' } }

    stages {
        stage('Install dependencies') {
            steps {
                sh 'npm install'
            }
        }
    stage('Build') {
            steps {
                sh 'ls -ltr'
                sh 'zip -r ./* --exclude=.git --exclude=.zip'
            }
        }
   
    //     // sonar-scanner expets sonar-project.properties avilable or not
    //   stage('Sonar Scan') {
    //         steps {
    //             sh 'ls -ltr'
    //             sh 'sonar-scanner'
    //         }
    //     }
}
    post{
        always{
            echo 'cleaning up workspace'
            deleteDir()
        }
    }

}