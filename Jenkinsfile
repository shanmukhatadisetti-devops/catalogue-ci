pipeline {
    agent {
        label 'agent-1'
    }
    environment {
        appVersion = ""

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
    }
} 