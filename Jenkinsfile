pipeline {
    agent any
    tools{
        nodejs 'NodeJS 12.16.1'
    }

    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh 'npm test'
            }
        }
        /* stage('Scanner') {
            steps {
                script {
                    def scannerHome = tool 'SonarQube Scanner';
                    withSonarQubeEnv("SonarQube Electric Boogaloo") {
                        sh "${tool("SonarQube Scanner")}/bin/sonar-scanner"
                    }
                }
            }
        } */
    }
}
