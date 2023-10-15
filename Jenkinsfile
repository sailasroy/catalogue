pipeline {
    agent { node { label 'AGENT-1' } }

    //here you create any variable you will have global access

    environment{
        
        packageVersion = ''
    }

    stages {
        stage('Version'){
            steps {
                script{
                    def packageJson = readJSON(file: 'package.json')
                    packageVersion = packageJson.version
                    echo "version: ${packageVersion}"

                }

            }
        }

        stage('Install dependencies') {
            steps {
                sh 'ls -ltr'
                sh 'npm install'
            }
        }
        stage('Unit test') {
            steps {
                echo "unit testing is done here"
                echo "package version : $packageVersion"
            }
        }
        //sonar-scanner command expect sonar-project.properties should be available
        // stage('Sonar Scan') {
        //     steps {
        //         sh 'ls -ltr'
        //         sh 'sonar-scanner'
        //     }
        // }
        stage('Build') {
            steps {
                sh 'ls -ltr'
                sh 'zip -r catalogue.zip ./* --exclude=.git --exclude=.zip'
                
            }
        }

        stage('Publish Artifact') {
            steps {
                nexusArtifactUploader(
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    nexusUrl: '18.232.110.38:8081/',
                    groupId: 'com.roboshop',
                    version: "$packageVersion",
                    repository: 'catalogue',
                    credentialsId: 'nexus-auth',
                    artifacts: [
                        [artifactId: 'catalogue',
                        classifier: '',
                        file: 'catalogue.zip',
                        type: 'zip']
                    ]
                )    

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
    // here i need to configure downstream job i have to pass packge version for deployment
        stage('Deployment') {
            steps {
                echo "Deployment"
                build job: "../catalogue-deply", wait=true
            }
        }

    post{
        always{
            echo 'cleaning up workspace'
            deleteDir()
        }
    }

}