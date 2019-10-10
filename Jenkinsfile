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
                sh label: 'list files', script: 'ls -l'
            }
        }
        stage('clone-wait') {
            steps {

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
        }
    }
    post { 
        always { 
            cleanWs()
        }
    }
}
