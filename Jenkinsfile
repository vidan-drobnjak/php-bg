
def number = 'UNKNOWN'
// \b\w*\my-app-\d*\b

pipeline {
    agent any
    parameters {
        text(name: 'ENV', defaultValue: '', description: 'Which environment?')
    }
    stages { 
        stage("Check Parameter Value") {
            script {
                if(${params.ENV} != "dev") {
                    error('Aborted beacause value of parameter')
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
