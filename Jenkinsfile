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
        stage('Descargar Build Wrapper ') {
            steps {
                sh '''
                  mkdir -p .sonar
                  curl -sSLo .sonar/build-wrapper-linux-x86.zip https://sonarcloud.io/static/cpp/build-wrapper-linux-x86.zip 
                  unzip -o .sonar/build-wrapper-linux-x86.zip -d .sonar/
                '''
            }
        }
        stage('Build archivos c++') {
            steps {
                sh '.sonar/build-wrapper-linux-x86/build-wrapper-linux-x86-64 --out-dir bw-output ./compile.sh' 
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