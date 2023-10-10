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
                sh 'zip -r catalogue.zip ./* --exclude=.git --exclude=.zip'
            }
        }

    //     stage('Publish Artifact') {
    //         steps {
    //             nexusArtifactUploader(
    //                 nexusVersion: 'nexus3',
    //                 protocol: 'http',
    //                 nexusUrl: '34.226.247.162:8081/',
    //                 groupId: 'com.roboshop',
    //                 version: '1.0.0',
    //                 repository: 'catalogue',
    //                 credentialsId: 'nexus-auth',
    //                 artifacts: [
    //                     [artifactId: 'catalogue',
    //                     classifier: '',
    //                     file: 'catalogue.zip',
    //                     type: 'zip']
    //                 ]
    //             )    

    //     }
    // }
   
    //     // sonar-scanner expets sonar-project.properties avilable or not
    //   stage('Sonar Scan') {
    //         steps {
    //             sh 'ls -ltr'
    //             sh 'sonar-scanner'
    //         }
    //     }
}
    // post{
    //     always{
    //         echo 'cleaning up workspace'
    //         deleteDir()
    //     }
    // }

}