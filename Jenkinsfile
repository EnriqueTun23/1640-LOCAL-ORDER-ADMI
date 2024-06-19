pipeline {
    agent any
    environment {
        scannerHome = tool name: 'sonar-scanner'
        SONAR_TOKEN = credentials('jenkins-sonar')
    }
    stages {
        stage('Obtener el proyecto') {
            steps {
                git branch: 'main', poll: false, url: 'https://github.com/EnriqueTun23/1640-LOCAL-ORDER-ADMI.git'
            }
        }
        stage('Liga del scanner') {
            steps {
                withSonarQubeEnv('sc1') {
                    sh """
                        ${scannerHome}/bin/sonar-scanner \
                        -Dsonar.login=${SONAR_TOKEN} \
                        -X
                    """
                }
            }
        }
    }
}