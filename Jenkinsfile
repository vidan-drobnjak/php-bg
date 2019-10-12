
def info = 'UNKNOWN'
def environment = 'UNKNOWN'
//cat ebenv.json | grep -o 'my-env-[0-9]*[0-9]' | sort -u

pipeline {
    agent any
    parameters {
        string(name: 'ENV', defaultValue: '', description: 'Which environment?')
    }
    stages { 
        stage("Check Parameter Value") {
            steps {
                echo "Checking parameter value: ${params.ENV}"
                script {
                    //Parameter validation
                    if (!("${params.ENV}" =="dev" || "${params.ENV}" == "test")) {
                        error('Aborted beacause of parameter value')
                    }
                }
                
            }
        }
        stage('ls') {
            steps {
                info = sh(returnStdout: true, script: 'aws elasticbeanstalk describe-environments \
                            --application-name blue-green \
                            --region us-east-1')
                sh label: '', script: 'cat info'
            }
        }
        /*stage('zip') {
            steps {
                sh label: 'zip file', script: 'zip src.zip index.php'
                
            }
        }
        stage('clone-wait') {
            steps {
                sh label: 'list files', script: 'ls -l'
            }
        }
        stage('create-version') {
            steps {

            }
        }
        stage('upload-wait') {
            steps {

            }
        }
        stage('swap-url-wait') {
            steps {

            }
        }
        stage('delete-old') {
            steps {
            }
        } */
    }
    post { 
        always { 
            cleanWs()
        }
    }
}
