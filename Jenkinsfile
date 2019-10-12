def eb_env
def eb_env_id

pipeline {
    agent any
    parameters {
        string(name: 'ENV', defaultValue: '', description: 'Which environment?')
    }
    stages { 
        stage("Parameter validation") {
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
        stage('Get environment name') {
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
        stage('Create configuration template') {
            steps {
                //Get environment ID
                sh label: '', script: 'aws elasticbeanstalk describe-environments \
                                --application-name blue-green \
                                --region us-east-1 \
                                --environment-names ${eb_env} > eb_info.json'
                script {
                    eb_env_id = sh(returnStdout: true, script: "jq -r '.Environments[0] .EnvironmentId' eb_info.json")
                }
                //echo "${eb_env_id}"
                //Create configuration template
                sh label: 'create conf template', script: "'aws elasticbeanstalk create-configuration-template \
                                 --application-name blue-green --environment-id ${eb_env_id} --region us-east-1 --template-name ${eb_env}-${BUILD_NUMBER}'"           
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
