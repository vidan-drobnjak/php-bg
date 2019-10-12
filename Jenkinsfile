def eb_env
def eb_env_id

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
                    if (!("${params.ENV}" == "dev" || "${params.ENV}" == "test")) {
                        error('Aborted beacause of parameter value')
                    }
                }
                
            }
        }
        stage('Get Environment Name') {
            steps {
                //sh script: 'aws elasticbeanstalk describe-environments --application-name blue-green --region us-east-1'
                script {
                    eb_env = sh(returnStdout: true, script: "aws elasticbeanstalk describe-environments \
                                --application-name blue-green \
                                --region us-east-1 \
                                 | grep -o 'bg-${params.ENV}-[0-9]*[0-9]' | sort -u")
                }
                echo "${eb_env}"
            }
        }
        stage('zip') {
            steps {
                sh label: 'zip file', script: 'zip src.zip index.php'
                sh label: 'list files', script: 'ls -l'
            }
        }
        stage('create-version') {
            steps {
                script {
                    eb_env_id = sh(returnStdout: true, script: "aws elasticbeanstalk describe-environments \
                                --application-name blue-green \
                                --region us-east-1 \
                                --environment-names ${eb_env}|jq -r '.Environments[0] .EnvironmentId'")
                }
                echo "${eb_env_id}"
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
