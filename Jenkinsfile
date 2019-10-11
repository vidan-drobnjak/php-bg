
def number = 'UNKNOWN'
// \b\w*\my-app-\d*\b

pipeline {
    agent any
    parameters {
        text(name: 'env', defaultValue: '', description: 'Which environment?')
    }
    stages { 
        stage('ls') {
            steps {
                sh label: 'list files', script: 'ls -l'
            }
        }
        stage('zip') {
            steps {
                sh label: 'zip file', script: 'zip src.zip index.php'
                
            }
        }
        stage('clone-wait') {
            steps {
                sh label: 'list files', script: 'ls -l'
            }
        }
        /*stage('create-version') {
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
