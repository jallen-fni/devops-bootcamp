pipeline {
    agent any
    tools{
        nodejs 'NodeJS 12.16.1'
    }

    stages {
        stage('NPM Install') {
            steps {
                sh 'npm install'
            }
        }
    }
}
