pipeline {
    agent any
    stages { 
        stage('ls') {
            steps {
                sh label: 'list files', script: 'ls -l'
            }
        }
        stage('zip') {
            steps {
                zip dir: '', glob: '', zipFile: 'src.zip'
                
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
