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
        stage('Dockerize') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'ECRAccess', passwordVariable: 'AWS_SECRET_ACCESS_KEY', usernameVariable: 'AWS_ACCESS_KEY_ID')]) {
                    // some block
                   sh '''
                        wget https://download.docker.com/linux/ubuntu/dists/bionic/pool/stable/amd64/docker-ce-cli_18.09.9~3-0~ubuntu-bionic_amd64.deb
                        dpkg -i ./docker-ce-cli_18.09.9~3-0~ubuntu-bionic_amd64.deb
                        apt-get update
                        apt-get install -y awscli
                        docker build -t workshopuser5:latest .
                        docker tag workshopuser5:latest workshopuser5:${BUILD_NUMBER}
                        docker tag workshopuser5:latest 686567993080.dkr.ecr.us-east-1.amazonaws.com/devopsbootcampuser5:latest
                        $(aws ecr get-login --region us-east-1 | sed 's/-e none//g')
                        docker push 686567993080.dkr.ecr.us-east-1.amazonaws.com/devopsbootcampuser5:latest
                    '''
                }
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
