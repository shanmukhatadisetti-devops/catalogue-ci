pipeline {
    agent {
        label 'agent-1'
    }
    environment {
        appVersion = ""
        REGION = "us-east-1"
        ACC_ID = "430774481266"
        PROJECT = "roboshop"
        COMPONENT = "catalogue"

    }
    options{
        timeout(time: 10, unit: 'MINUTES')
        disableConcurrentBuilds()
    }
    stages {
        stage('read Package.Json'){
            steps{
                script{
                    def packageJson = readJSON file: 'package.json'
                    def appVersion = packageJson.version
                    echo "The current version is: ${appVersion}"
                }
            }
        }
        stage('Install Dependancies'){
            steps{
                script{
                    sh """
                        npm install
                    """
                }
            }
        }
        stage('Docker Build'){
            steps{
                script{
                        withAWS(credentials: 'aws-creds', region: 'us-east-1') {
                            sh"""
                                aws ecr get-login-password --region ${REGION} | docker login --username AWS --password-stdin ${ACC_ID}.dkr.ecr.${REGION}.amazonaws.com
                                docker build -t ${ACC_ID}.dkr.ecr.${REGION}.amazonaws.com/${PROJECT}/${COMPONENT}:${appVersion}
                                docker push ${ACC_ID}.dkr.ecr.${REGION}.amazonaws.com/${PROJECT}/${COMPONENT}:${appVersion}
                            """    
                        }
                }
            }
        }
    }
} 