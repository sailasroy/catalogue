pipeline {
    agent { node { label 'AGENT-1' } }
    options {
        ansiColor('xterm')
    }

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
                    nexusUrl: '54.209.245.39:8081/',
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

    // here i need to configure downstream job i have to pass packge version for deployment
        stage('Deployment') {
            steps {
                script{
                    echo "Deployment"
                        def params = [
                            string(name: 'version', value: "$packageVersion")
                        ]
                        
                        build job: "../catalogue-deploy", wait: true, parameters: params
            }
        }
        }
    }
        stage('Approve') {
            input {
                message "Should we continue?"
                ok "Yes, we should."
                submitter "alice,bob"
                parameters {
                    string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
                }
            }
            steps {
                echo "Hello, ${PERSON}, nice to meet you."
            }
        }

        stage('Apply'){
            steps{
                sh """
                cd terraform
                terraform apply -var="app_version=${params.version}" -auto-approve
                """
            }
        }
    }   
    post{
        always{
            echo 'cleaning up workspace'
           // deleteDir()
        }
    }

}