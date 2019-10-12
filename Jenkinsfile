
def number = 'UNKNOWN'
def environment = 'UNKNOWN'
//grep -ow 'my-env-[0-9]*[0-9]' ebenv.json | sort -u

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
                        error('Aborted beacause value of parameter')
                    }
                }
                
            }
        }
        stage('ls') {
            steps {
                echo "${params.ENV}"
                //sh label: 'list files', script: 'ls -l'
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
